<template>
    <div id="example-2" class="text-center">
        <p> Новый пользователь </p>
        <input v-model="nameUser" placeholder="Имя">
        <input v-model="loginUser" placeholder="Логин">
        <input v-model="passwordUser" placeholder="Пароль">
            <button  v-on:click="pushing">Добавить пользователя</button>
    </div>
</template>

<script>
    export default {
        name: "addUser",
        props:["userList"],
        data() {
            return {
                lengthArray:null,
                nameUser: null,
                loginUser: null,
                passwordUser: null,
            }
            },
        methods:{
            pushing: function () {
                let newUser={id:++this.lengthArray, name:this.nameUser, login:this.loginUser, password:this.passwordUser};
                this.userList.push(newUser);
                this.nameUser="";
                this.loginUser="";
                this.passwordUser=""
            },
            findThisUser: function(list, trueLogin) {
                for (let i = 0; i < list.length; i++) {
                    if (list[i].login === trueLogin) {
                        return list[i]
                    }
                }
                return false
            }
        }
    }
</script>
