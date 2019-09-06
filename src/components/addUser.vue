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
        props:[ "addUserFunc"],
        data() {
            return {
                nameUser: null,
                loginUser: null,
                passwordUser: null,
            }
        },
        methods:{
            pushing: function () {
                this.addUserFunc(this.nameUser,this.loginUser,this.passwordUser);
                this.nameUser="";
                this.loginUser="";
                this.passwordUser="";
            },
        }
    }
</script>
