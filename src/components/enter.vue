<template>
        <div class="col-3  m-auto">
            <b-card bg-variant="secondary" text-variant="white" header="Вход" class="text-center my-5">
                <p class="text-warning">{{messageWithMistakeEnter}}</p>
                    <b-form-group class="text-left form-group" label="Логин">
                        <b-form-input type="text" v-model="enterLoginUser"></b-form-input>
                    </b-form-group>
                    <b-form-group class="text-left  " label="Пароль">
                        <b-form-input type="text" v-model="enterPasswordUser"></b-form-input>
                    </b-form-group>
                    <b-button type="button" variant="primary"  v-on:click="checkUser">Войти</b-button>

            </b-card>
         </div>

</template>

<script>
    export default {
        name: "enter",
        props:[ "checkUserFunc", "messageWithMistakeEnter"],
        // "token",
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

