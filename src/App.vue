<template>
    <div id="app">
        <template v-if = "token !== null">
            <navbar  v-bind:mainPage = "mainPage" v-bind:Logout = "Logout" v-bind:authorizedUser = "authorizedUser"  v-bind:showArrayFiles = "showArrayFiles"  v-bind:showArrayUsers = "showArrayUsers" />
            <template v-if = "mainPage === 'users'">
                <template v-if = "userLogin === 'Admin'">
                    <addUser v-bind:addUserFunc = "addUserFunc" v-bind:user = "user" v-bind:messageWithMistakeAdd = "messageWithMistakeAdd" />
                    <html_List_Users v-bind:userList = "userList"  v-bind:deleteUserFunc = "deleteUserFunc" v-bind:authorizedUser = "authorizedUser" v-bind:userLogin = "userLogin"  v-bind:changePassword = "changePassword"/>
                </template>
                <template v-else>
                    <html_List_Users v-bind:userList = "userList"  v-bind:deleteUserFunc = "deleteUserFunc" v-bind:authorizedUser = "authorizedUser" v-bind:userLogin = "userLogin"  v-bind:changePassword = "changePassword"/>
                </template>
            </template>
            <template v-else-if="mainPage === 'files'">
                <files v-bind:userFiles = "userFiles"  v-bind:addNewFile = "addNewFile" v-bind:deleteFile = "deleteFile" v-bind:userLogin = "userLogin"/>
<!--            <button  v-on:click="getArrayFilesFunc">Показать файлы в папке</button>-->
            </template>
        </template>

        <template v-else>
            <enter v-bind:checkUserFunc = "checkUserFunc" v-bind:token = "token"  v-bind:messageWithMistakeEnter = "messageWithMistakeEnter"  v-bind:noMitstakeMessage = "noMitstakeMessage"/>
        </template>
    </div>
</template>


<script>
    import addUser from './components/addUser.vue'  //импортирую файл
    import html_List_Users from './components/html_List_Users.vue'  //импортирую файл
    import enter from './components/enter.vue'
    import files from './components/files.vue'
    import navbar from './components/navbar.vue'
    import axios from "axios"



    export default {
        name: 'app',

        data() {
            return {
                userList: [],
                userFiles: [],
                user:null,
                token: null,
                authorizedUser:null,
                mainPage:"users",
                userLogin:"",
                messageWithMistakeAdd:"",
                messageWithMistakeEnter:"",
                noMitstakeMessage:""
            }

        },
        mounted() {
            this.token=localStorage.getItem('jwttoken');
            if(this.token){
                this.setTitleAuth();
                this.rememberName();
                this.reloadUserList();  //для обновления списка пользователей
            }

        },

        components: {           // нужно сделать в 3-х местах App.vue
            html_List_Users,
            addUser,
            enter,
            files,
            navbar
        },
        methods: {
             addUserFunc: function (name, login, password,cb) {   //callback функция
                axios.post(`http://localhost:3000/ajax/users.json/addUser`, {
                    login, name, password           //для пост запросов
                })
                .then(() => {
                    this.messageWithMistakeAdd = null;
                    this.reloadUserList();
                    cb()
                })
                .catch(error => {
                    console.log(error.response.data.message);
                    this.messageWithMistakeAdd = error.response.data.message;
                    cb(error)
                })
            },
            deleteUserFunc: function (id) {
                axios.post(`http://localhost:3000/ajax/users.json/delete`, {id})
                    .then(() => this.reloadUserList())
            },
            changePassword: function (id, password, repeatPassword) {
                axios.post(`http://localhost:3000/ajax/users.json/changepassword`, {id, password,  repeatPassword})
                    .then(() => this.reloadUserList())
            },
            reloadUserList: function () {
                axios.get('http://localhost:3000/ajax/users.json/', {
                    params: {
                        t: Date.now(),  //вспомогательная функция, чтобы не кэшировалось
                    }
                })
                    .then((response) => {
                        this.userList = response.data;   //метод для отрисовки табилцы через другой сервер
                    })
            },
            reloadFileList: function () {
                axios.get('http://localhost:3000/ajax/users.json/files', {
                    params: {
                        t: Date.now(),  //вспомогательная функция, чтобы не кэшировалось
                    }
                })
                    .then((response) => {
                        this.userFiles = response.data.files;   //метод для отрисовки табилцы через другой сервер
                    })
            },
            setTitleAuth() {
                if (this.token) {
                    axios.defaults.headers.common = {Authorization: `Token_is: ${this.token}`}   //ко всем запросам добавляет токен
                    // прикрепляю заголовок авторизации, теперь мы не должны передавать токен каждый раз
                }
            },
            rememberName: function () {
                axios.get('http://localhost:3000/ajax/users.json/name')
                    .then((response) => {
                        this.authorizedUser = response.data.name;   //метод для отрисовки табилцы через другой сервер
                        this.userLogin = response.data.login
            })
            },
            checkUserFunc: function (login, password) {
                axios.post(`http://localhost:3000/ajax/users.json/checkuser`, {login, password})
                    .then((response) => {
                        this.token = response.data.token;    //для первого входа
                        this.authorizedUser = response.data.user_name;
                        this.userLogin = response.data.user_login;
                        console.log(this.authorizedUser);
                        localStorage.setItem('jwttoken', response.data.token);          //для послдеующего входа
                        this.setTitleAuth();
                        this.messageWithMistakeEnter = null;
                        this.reloadUserList();
                    })
                    .catch(error => {
                        // console.log(error)               //системная ошибка
                        // console.log(error.response)      // ответ от сервера (объект)
                        this.messageWithMistakeEnter = error.response.data.message;
                    })
            },
            Logout: function () {
                this.token = null;
                localStorage.removeItem('jwttoken');
                axios.defaults.headers.common = null
            },
            showArrayFiles: function () {
                this.mainPage = "files";
                axios.get('http://localhost:3000/ajax/users.json/files')
                    .then((response) => {
                        this.userFiles = response.data.files;
                    })
            },
            showArrayUsers: function () {
                this.mainPage = "users";
            },
            addNewFile: function (domain, ip) {
                axios.post(`http://localhost:3000/ajax/users.json/addFiles`, {domain, ip})
                    .then(() => {
                        this.reloadFileList()
                    })
            },
           deleteFile: function (delFile) {
                axios.post(`http://localhost:3000/ajax/users.json/delFiles`, {delFile})
                    .then(() => {
                        this.reloadFileList()
                    })
            }
        }
    }

</script>


