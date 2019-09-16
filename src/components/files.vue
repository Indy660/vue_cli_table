<template>
    <div id="example-2" class="text-center">
    <h3>Список файлов:</h3>
        <div class="container py-5 text-center">
            <div class="card col-lg-4" style="width: 18rem;">
                <ul class="list-group list-group-flush " v-for="file in userFiles">
                <li class="list-group-item ">{{file}}</li>
                </ul>
            </div>
        </div>
    </div>
    
</template>

<script>

    export default {
        name: "files",
        props:["userFiles"],
        data() {
            return {

            }
        },
        // methods: {
        //     getArrayFiles: function () {
        //         this.getArrayFilesFunc();
        //     }
        // }
    }
</script>




