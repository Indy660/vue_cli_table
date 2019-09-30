<template>
    <div id="example-2" class="text-center">
        <p></p>

        <div class="text-center">
<!--            <p class="text-warning">{{messageWithMistakeAdd}}</p>-->


            <button class="btn btn-success" size="sm" @click="$bvModal.show('bv-modal-example2')">Добавить нового пользователя</button>
            <b-modal id="bv-modal-example2" ref="my-modal" hide-footer="" header-bg-variant="light"><template slot="modal-title"><h4 class="text-dark">Добавьте имя, логин и пароль пользователя</h4></template>
                <div class="d-block text-right">
                    <form ref="form">
                        <b-form-group class="text-left" label="Имя">
                            <b-form-input type="text" v-model="nameUser"></b-form-input>
                        </b-form-group>
                        <b-form-group class="text-left" label="Логин">
                            <b-form-input type="text" v-model="loginUser"></b-form-input>
                        </b-form-group>
                        <b-form-group class="text-left" label="Пароль">
                            <b-form-input type="text" v-model="passwordUser"></b-form-input>
                        </b-form-group>
                        <b-button class="mx-2" type="button"  variant="danger" data-dismiss="my-modal" @click="$bvModal.hide('bv-modal-example2')">Отмена</b-button>
                        <b-button type="button" variant="primary"  v-on:click="pushing">Добавить пользователя</b-button>

                    </form>
                </div>
                <template v-if = "Boolean(messageWithMistakeAdd) === true">
                    <b-alert
                            :show="dismissCountDown"
                            dismissible
                            variant="danger"
                            @dismissed="dismissCountDown=0"
                            @dismiss-count-down="countDownChanged"
                    >
                        {{messageWithMistakeAdd}}
                    </b-alert>
                </template>
            </b-modal>
        </div>

    </div>
</template>

<script>
    export default {
        name: "addUser",
        props:[ "addUserFunc", "messageWithMistakeAdd"],
        data() {
            return {
                nameUser: null,
                loginUser: null,
                passwordUser: null,
                dismissSecs: 3,
                dismissCountDown: 0
            }
        },
        // mounted() {
        //     this.messageWithMistakeAdd = "5";
        // },
        methods:{
            pushing: function () {
                this.addUserFunc(this.nameUser,this.loginUser,this.passwordUser,(err)=>{
                    console.log(this.messageWithMistakeAdd);            //отстает на одно действие, считывает старое значение
                    if (Boolean(this.messageWithMistakeAdd) === false) {this.$bvModal.hide('bv-modal-example2')  }
                    else {this.dismissCountDown = this.dismissSecs;}
                });
                this.nameUser="";
                this.loginUser="";
                this.passwordUser="";
            },
            countDownChanged(dismissCountDown) {
                this.dismissCountDown = dismissCountDown
            },
            // deleteMessage() {
            //     if ( event.keyCode)
            // }
        }
    }
</script>

