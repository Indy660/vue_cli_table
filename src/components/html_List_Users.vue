<!--HTML-->
<template>
    <div  class="container py-5 text-center">
      <p> Пользователь: {{authorizedUser}} </p>
      <input type="text" v-model="search" placeholder="Поиск пользователя">
      <p></p>
      <table class="table table-bordered table-dark">
      <thead>
        <tr>
          <th scope="col"><img src="../assets/sort.svg" width="25" height="25" class="float-right" v-on:click="addParametrsForSort('id')">ID</th>
          <th scope="col"><img src="../assets/sort.svg" width="25" height="25" class="float-right" v-on:click="addParametrsForSort('name')">Имя</th>
          <th scope="col"><img src="../assets/sort.svg" width="25" height="25" class="float-right" v-on:click="addParametrsForSort('login')">Логин</th>
          <th scope="col"><img src="../assets/sort.svg" width="25" height="25" class="float-right" v-on:click="addParametrsForSort('password')">Пароль</th>
        </tr>
        </thead>
        <tbody>
        <tr v-for="user in searchAndSortFiles">
          <td>{{user.id}}</td>
          <td>{{user.name}}</td>
          <td>{{user.login}}</td>
          <td>{{user.password}} <img src = "../assets/cancel.svg" width="25" height="25"
                                     class="float-right"  v-on:click = "deleteUserFunc(user.id)"></td>
        </tr>
        </tbody>
      </table>
    </div>
</template>


<!--VUE-->
<script>

export default {
  name: 'List',
  props:["userList", "deleteUserFunc", "authorizedUser"],
  data() {
    return {
      sortColumn: '',
      sortDirection:-1,
      search: ""
    }
},
  "computed": {
    searchAndSortFiles() {
      let obj = this.userList;
      let newArray = [];
      const serach = this.search.toLowerCase();
      newArray = obj.filter(function(elem) {
        if (
            elem.login.toLowerCase().indexOf(serach) != -1 ||
            elem.name.toLowerCase().indexOf(serach) != -1  ||
            String(elem.id).toLowerCase().indexOf(serach) != -1
            ) {
          return true;
        } else {
          return false;
        }
      });
      return newArray.slice().sort((a, b) => {
        if (a[newArray] < b[newArray]) {
          return this.sortDirection
        } else {
          return -1*this.sortDirection
        }
      })
    }
  },
  methods: {
    addParametrsForSort: function (elem) {
      return (this.sortColumn=elem, this.sortDirection*=-1 )
    }
  }
}
</script>

