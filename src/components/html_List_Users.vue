<!--HTML-->
<template>
  <div id="example-2" class="text-center">
    <p> Новый пользователь </p>

    <input v-model="nameUser" placeholder="Имя">
    <input v-model="loginUser" placeholder="Логин">
    <input v-model="passwordUser" placeholder="Пароль">

    <button  v-on:click="pushing">Добавить пользователя</button>

    <div  class="container py-5 text-center">
      <table class="table table-bordered table-dark">
        <thead>
        <tr>
          <th scope="col"><img src="../assets/sort.svg" width="25" height="25" class="float-right"  v-on:click="sortColumn='id'; sortDirection*=-1">ID</th>
          <th scope="col"><img src="../assets/sort.svg" width="25" height="25" class="float-right"  v-on:click="sortColumn='name'; sortDirection*=-1">Имя</th>
          <th scope="col"><img src="../assets/sort.svg" width="25" height="25" class="float-right"  v-on:click="sortColumn='login'; sortDirection*=-1">Логин</th>
          <th scope="col"><img src="../assets/sort.svg" width="25" height="25" class="float-right"  v-on:click="sortColumn='password'; sortDirection*=-1">Пароль</th>
        </tr>
        </thead>
        <tbody>
        <tr v-for="user in userSortList">
          <td>{{user.id}}</td>
          <td>{{user.name}}</td>
          <td>{{user.login}}</td>
          <td>{{user.password}} <img src="../assets/cancel.svg" width="25" height="25"
                                     class="float-right"  v-on:click="deleting(user.login)"></td>
        </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>


<!--VUE-->
<script>
export default {
  name: 'List',
  data() {
    return {
    userList: [
      { id: 1, name: 'Admin', login: 'Admin', password:"qwe"},
      { id: 2, name: 'TestUser', login: 'test', password:"123"},
      { id: 3, name: 'Dima', login: 'DimaK', password:"12345"},
      { id: 4, name: 'Sacha', login: 'gundi5', password:"BF236BF"},
      { id: 5, name: 'Дима', login: 'Indy660', password: '123' }
    ],
    sortColumn: '',
    lengthArray:null,
    nameUser: null,
    loginUser: null,
    passwordUser: null,
    sortDirection:-1
  }
},
  created: function(){
    this.lengthArray = this.userList.length
  },
  computed:{
    userSortList: function(){
      const sortColumn = this.sortColumn;
      if (this.sortDirection===-1) {
        return this.userList.slice().sort((a, b)=> {
          if (a[sortColumn] < b[sortColumn]) {
            return -1
          } else {
            return 1
          }
        });
      }
      else {
        return this.userList.slice().sort((a, b) => {
          if (a[sortColumn] < b[sortColumn]) {
            return 1
          } else {
            return -1
          }
        });
      }
    }
  },
  methods:{
    pushing: function () {
      let newUser={id:++this.lengthArray, name:this.nameUser, login:this.loginUser, password:this.passwordUser};
      this.userList.push(newUser);
      this.nameUser="";
      this.loginUser="";
      this.passwordUser=""
      },
    findThisUser: function(list, trueLogin) {
      for (let i = 0; i < list.length; i++) {
        if (list[i].login === trueLogin) {
          return list[i]
        }
      }
      return false
    },
    deleting: function (login) {
      let user=this.findThisUser(this.userList, login);
      let trueIndex= this.userList.indexOf(user);
      this.userList.splice(trueIndex, 1)
    }
  }
}
</script>

