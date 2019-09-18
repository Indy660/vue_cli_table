<template>
    <div id="example-2" class="text-center">
        <h3>Список файлов:</h3>
        <div class="card-footer ">
            <form class="col-lg-13 align-text-bottom">
                <input value=""  name="value" class="form-control mr-sm-2" type="text" placeholder="Домен"  v-model="domain"
                       aria-label="Search">
                <input value=""  name="value" class="form-control mr-sm-2" type="text" placeholder="IP" v-model="ip"
                       aria-label="Search">
                <button class="btn btn-outline-warning my-2 my-sm-0" type="button" v-on:click="pushFile">Добавить файл</button>
            </form>
        </div>
                <table class="table table-primary container py-5 text-center">
                <thead class="thead-dark">
                <tr>
                    <th scope="col">Домэн</th>
                    <th scope="col">IP</th>
                </tr>
                </thead>
                <tbody>
                <tr v-for="file in userFiles">
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
                // delFile: null
            }
        },
        methods: {
            pushFile: function () {
                this.addNewFile(this.domain,this.ip);
                this.domain="";
                this.ip="";
            },
            // deleteItem: function () {
            //     this.deleteFile(this.delFile)
            //     console.log(this.delFile)
            //     console.log(this.file)
            // }
        }
    }
</script>




