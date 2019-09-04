<template>
  <div id="app">
      <addUser v-bind:userList="userList"/>
    <ListUsers v-bind:userList="userList"/>
<!--    <axios v-bind:userList="userList"/>-->
  </div>
</template>

<script>
import addUser from './components/addUser.vue'  //импортирую файл
import ListUsers from './components/html_List_Users.vue'  //импортирую файл
import axios from "axios"



export default {
  name: 'app',
  data() {
    return {
      userList: []
      // {id: 1, name: 'Admin', login: 'Admin', password: "qwe"},
      // {id: 2, name: 'TestUser', login: 'test', password: "123"},
      // {id: 3, name: 'Dima', login: 'DimaK', password: "12345"},
      // {id: 4, name: 'Sacha', login: 'gundi5', password: "BF236BF"},
      // {id: 5, name: 'Дима', login: 'Indy660', password: '123'}
    }
  },
  mounted() {
      axios.get('http://localhost:3000/ajax/users.json/')
            .then((response) => {
                console.log(response);
                this.userList = response.data;
            });
  },

  components: {
    ListUsers,     //ListUsers нужно сделать в 3-х местах APP
    addUser
  },
    method: {
        addUser: function() {
            axios({
                method: 'get',
                url: 'http://localhost:3000/ajax/users.json/addUser',
                data: {
                    name: this.nameUser,
                    login: this.loginUser,
                    password: this.passwordUser
                }
            });
        }
//получение списка пользователей
// добавление списка пользователей
        //удаления
    }
}
</script>


