<template>
    <div id="example-2" class="text-center">
        <p> Вход </p>
        <p>  {{token}}  </p>
        <input v-model="enterLoginUser" placeholder="Логин">
        <input v-model="enterPasswordUser" placeholder="Пароль">
        <button  v-on:click="checkUser">Войти</button>

    </div>
</template>

<script>
    export default {
        name: "enter",
        props:[ "checkUserFunc", "token"],
        data() {
            return {
                enterLoginUser: null,
                enterPasswordUser: null,
            }
        },
        methods:{
            checkUser: function () {
                this.checkUserFunc(this.enterLoginUser,this.enterPasswordUser);
                this.enterLoginUser="";
                this.enterPasswordUser="";
            },
        }
    }
</script>

