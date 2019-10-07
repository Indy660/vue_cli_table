<template>
        <div class="col-3  m-auto">
            <b-card bg-variant="secondary" text-variant="white" header="Вход" class="text-center my-5">

<!--                <p class="text-warning">{{messageWithMistakeEnter}}</p>-->




                <b-form-group class="text-left form-group" label="Логин">
                        <b-form-input type="text" v-model="enterLoginUser"  v-on:click="hideAlert"></b-form-input>
                    </b-form-group>
                    <b-form-group class="text-left  " label="Пароль">
                        <b-form-input type="text" v-model="enterPasswordUser" v-on:click="hideAlert"></b-form-input>
                    </b-form-group>
                    <b-button type="button" variant="primary"  v-on:click="checkUser">Войти</b-button>
                <div>

                    <p></p>

                    <b-alert
                            :show="showDismissibleAlert"
                             @dismissed="showDismissibleAlert = false"
                            variant="danger"
                    >
                        {{messageWithMistakeEnter}}
                    </b-alert>


<!--                    <template v-else> {{noMitstakeMessage}} </template>-->

                </div>
            </b-card>
         </div>

</template>

<script>
    export default {
        name: "enter",
        props:[ "checkUserFunc", "messageWithMistakeEnter", "noMitstakeMessage"],
        // "token",
        data() {
            return {
                enterLoginUser: null,
                enterPasswordUser: null,
                showDismissibleAlert: false
            }
        },
        methods:{
            checkUser: function () {
                this.checkUserFunc(this.enterLoginUser,this.enterPasswordUser);
                this.enterLoginUser="";
                this.enterPasswordUser="";
                this.showDismissibleAlert = true
            },
            hideAlert: function() {
                if ((this.enterLoginUser) || (this.enterPasswordUser)) {
                    this.showDismissibleAlert = false
                }
            }
        }
    }
</script>

<!--// если v input пустой, то-->