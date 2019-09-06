<template>
  <div id="app">
      <addUser v-bind:addUserFunc="addUserFunc"/>
      <html_List_Users v-bind:userList="userList"  v-bind:deleteUserFunc="deleteUserFunc"/>
  </div>
</template>

<script>
import addUser from './components/addUser.vue'  //импортирую файл
import html_List_Users from './components/html_List_Users.vue'  //импортирую файл
import axios from "axios"



export default {
  name: 'app',
  data() {
    return {
      userList: [],
    }
  },
  mounted() {
     this.reload()
  },

  components: {
    html_List_Users,     //html_List_Users нужно сделать в 3-х местах APP
    addUser
  },
    methods: {
        addUserFunc: function(name,login,password) {
            axios.post(`http://localhost:3000/ajax/users.json/addUser`, {
                // data:{                       //для гет запросов
                //     name, login, password
                // }
                login, name, password           //для пост запросов
            })
            .then(() => this.reload())
        },
        deleteUserFunc: function (id) {
            axios.post(`http://localhost:3000/ajax/users.json/delete`, { id })
                .then(() => this.reload())
        },
       reload: function () {
           axios.get('http://localhost:3000/ajax/users.json/',{
               params:{
                   t:Date.now()
               }
           })                                   //вспомогательная функция, чтобы не кэшировалось
           .then((response) => {
               //console.log(response.data);
               this.userList = response.data;   //метод для отрисовки табилцы через другой сервер
            })
       }
    }
}
</script>


