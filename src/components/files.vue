<template>
    <div id="example-2" class="text-center">
        <h3>Список файлов:</h3>
        <div class="card-footer ">


            <div class="text-center">
                <button class="btn btn-outline-warning my-2 my-sm-0" size="sm" @click="$bvModal.show('bv-modal-example1')">Добавить файл</button>
                    <b-modal id="bv-modal-example1" ref="my-modal" hide-footer="" header-bg-variant="light"><template slot="modal-title"><h4 class="text-dark">Добавьте в список домен</h4></template>
                <div class="d-block text-right">
                    <form ref="form">
                        <b-form-group class="text-left" label="Имя домена">
                            <b-form-input  v-model="domain"></b-form-input>
                        </b-form-group>
                        <b-form-group class="text-left" label="IP">
                            <b-form-input type="text" v-model="ip"></b-form-input>
                        </b-form-group>
                        <b-button class="mx-2" v-on:click="pushFile" size="sm" variant="outline-success">Добавить файл</b-button>
                        <b-button variant="outline-danger" size="sm" @click="$bvModal.hide('bv-modal-example1')">Закрыть</b-button>
                    </form>
                </div>
                </b-modal>
            </div>
            <p></p>
            <input type="text" class="form-control text-center col-3  m-auto" v-model="search" placeholder="Поиск файлов">

        </div>
                <table class="table table-primary container py-5 text-center">
                <thead class="thead-dark">
                <tr>
                    <th scope="col">Домен</th>
                    <th scope="col">IP</th>
                </tr>
                </thead>
                <tbody>
<!--                <tr v-for="file in userFiles">-->
<!--                    <td >{{file.domain}}</td>-->
<!--                    <td >{{file.ip}}  <a><img src="../assets/cancel.svg" width="25" height="25"-->
<!--                                class="float-right" v-on:click="deleteFile(file.domain)"></a> </td>-->
<!--                </tr>-->

                <tr v-for="file in searchMethod">
                    <td >{{file.domain}}</td>
                    <td >{{file.ip}}  <a><img src="../assets/cancel.svg" width="25" height="25"
                                              class="float-right" v-on:click="deleteFile(file.domain)"></a> </td>
                </tr>
                </tbody>
                </table>
        </div>
</template>

<script>

    export default {
        name: "files",
        props:["userFiles", "addNewFile", "deleteFile"],
        data() {
            return {
                domain: null,
                ip: null,
                search:""
            }
        },


        computed: {
            searchMethod() {
                let obj = this.userFiles;
                let newArray = [];
                const serach = this.search.toLowerCase();
                for (let key in obj) {
                    let el = obj[key]
                    if (el.domain.toLowerCase().indexOf(serach) != -1) newArray.push(el);
                    else if (el.ip.toLowerCase().indexOf(serach) != -1) newArray.push(el)
                }
                return newArray;
            }
        },


        methods: {
            pushFile: function () {
                this.addNewFile(this.domain,this.ip);
                this.domain="";
                this.ip="";
            },
        }
    }
</script>




