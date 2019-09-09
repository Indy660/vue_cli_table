<template>
  <div id="app">
      <template v-if="user!== null">
      <addUser v-bind:addUserFunc="addUserFunc" v-bind:user="user"/>
      <html_List_Users v-bind:userList="userList"  v-bind:deleteUserFunc="deleteUserFunc"/>
      </template>

      <template v-else>
      <enter v-bind:checkUserFunc="checkUserFunc" v-bind:token="token"/>
      </template>
  </div>
</template>


<script>
import addUser from './components/addUser.vue'  //импортирую файл
import html_List_Users from './components/html_List_Users.vue'  //импортирую файл
import enter from './components/enter.vue'
import axios from "axios"



export default {
  name: 'app',

  data() {
    return {
      userList: [],
      user:null,
      token: null
    }

  },
  mounted() {
     this.reload();
      this.token=localStorage.getItem('jwttoken')

  },

  components: {
    html_List_Users,     //html_List_Users нужно сделать в 3-х местах APP
    addUser,
    enter
  },
    methods: {
        addUserFunc: function(name,login,password) {
            axios.post(`http://localhost:3000/ajax/users.json/addUser`, {
                // data:{                       //для гет запросов
                //     name, login, password
                // }
                login, name, password           //для пост запросов
            })
            .then(() => this.reload())
        },
        deleteUserFunc: function (id) {
            axios.post(`http://localhost:3000/ajax/users.json/delete`, { id })
                .then(() => this.reload())
        },
       reload: function () {
           axios.get('http://localhost:3000/ajax/users.json/',{
               params:{
                   t:Date.now()  //вспомогательная функция, чтобы не кэшировалось
               }
           })
           .then((response) => {
               //console.log(response.data);
               this.userList = response.data;   //метод для отрисовки табилцы через другой сервер
            })
       },
        checkUserFunc: function (login, password) {
            axios.post(`http://localhost:3000/ajax/users.json/checkuser`, { login, password })
                .then((response) => {
                    // console.log(response.data.user_login)
                    this.user = response.data.user_login;
                    console.log(response.data.token);
                    this.token=response.data.token;
                    localStorage.setItem('jwttoken', response.data.token)
                })
        },
    }
}
</script>


