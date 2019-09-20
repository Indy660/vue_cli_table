<template>
    <div id="example-2" class="text-center">
        <p></p>

<!--        <div class="text-center">-->
<!--        <button type="button" class="btn btn-success" data-toggle="my-modal" data-target="#bv-modal-example1" @click="$bvModal.show('bv-modal-example1')  >Добавить нового пользователя</button>-->
<!--        <b-modal id="bv-modal-example1" ref="my-modal" hide-footer="" header-bg-variant="light"><template slot="modal-title"><h4 class="text-dark">Добавьте имя, логин и пароль пользователя</h4></template>-->
<!--            <div class="d-block text-right">-->
<!--                <form ref="form">-->
<!--                    <b-form-group class="text-left" label="Имя">-->
<!--                        <b-form-input type="text" v-model="nameUser"></b-form-input>-->
<!--                    </b-form-group>-->
<!--                    <b-form-group class="text-left" label="Логин">-->
<!--                        <b-form-input type="text" v-model="loginUser"></b-form-input>-->
<!--                    </b-form-group>-->
<!--                    <b-form-group class="text-left" label="Пароль">-->
<!--                        <b-form-input type="text" v-model="passwordUser"></b-form-input>-->
<!--                    </b-form-group>-->
<!--                    <b-button type="button" class="btn btn-secondary" data-dismiss="my-modal">Отмена</b-button>-->
<!--                    <b-button type="button" class="btn btn-primary"  v-on:click="pushing">Добавить пользователя</b-button>-->
<!--                </form>-->
<!--            </div>-->
<!--        </b-modal>-->
<!--        </div>-->
<!--    -->

        <div class="text-center">
<!--            <button type="button" class="btn btn-success" data-toggle="my-modal" data-target="#bv-modal-example2" @click="$bvModal.show('bv-modal-example2')  >-->
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
            </b-modal>
        </div>



<!--        <div class="text-center">    прошлая кнопка-->
<!--            <button class="btn btn-outline-warning my-2 my-sm-0" size="sm" @click="$bvModal.show('bv-modal-example1')">Добавить файл</button>-->
<!--            <b-modal id="bv-modal-example1" ref="my-modal" hide-footer="" header-bg-variant="light"><template slot="modal-title"><h4 class="text-dark">Добавьте в список домен</h4></template>-->
<!--                <div class="d-block text-right">-->
<!--                    <form ref="form">-->
<!--                        <b-form-group class="text-left" label="Имя домена">-->
<!--                            <b-form-input  v-model="domain"></b-form-input>-->
<!--                        </b-form-group>-->
<!--                        <b-form-group class="text-left" label="IP">-->
<!--                            <b-form-input type="text" v-model="ip"></b-form-input>-->
<!--                        </b-form-group>-->
<!--                        <b-button class="mx-2" v-on:click="pushFile" size="sm" variant="outline-success">Добавить файл</b-button>-->
<!--                        <b-button variant="outline-danger" size="sm" @click="$bvModal.hide('bv-modal-example1')">Закрыть</b-button>-->
<!--                    </form>-->
<!--                </div>-->
<!--            </b-modal>-->
<!--        </div>-->

<!--        <div class="modal fade" id="exampleModal" tabindex="-1" role="dialog" aria-labelledby="exampleModalLabel" aria-hidden="true">-->
<!--            <div class="modal-dialog" role="document">-->
<!--                <div class="modal-content">-->
<!--                    <div class="modal-header">-->
<!--                        <h5 class="modal-title" id="exampleModalLabel">Добавьте имя, логин и пароль пользователя</h5>-->
<!--                        <button type="button" class="close" data-dismiss="modal" aria-label="Close">-->
<!--                            <span aria-hidden="true">&times;</span>-->
<!--                        </button>-->
<!--                    </div>-->
<!--                    <div class="modal-body">-->
<!--                        <input v-model="nameUser" placeholder="Имя">-->
<!--                        <input v-model="loginUser" placeholder="Логин">-->
<!--                        <input v-model="passwordUser" placeholder="Пароль">-->
<!--                    </div>-->
<!--                    <div class="modal-footer">-->
<!--                        <button type="button" class="btn btn-secondary" data-dismiss="modal">Отмена</button>-->
<!--                        <button type="button" class="btn btn-primary"  v-on:click="pushing">Добавить пользователя</button>-->
<!--                    </div>-->
<!--                </div>-->
<!--            </div>-->
<!--        </div>-->
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

