<!--HTML-->
<template>
    <div  class="container py-5 text-center">
      <input type="text" v-model="search" placeholder="Поиск пользователя">
      <p></p>
      <table class="table table-bordered table-dark">
      <thead>
        <tr>
<!--         class="d-flex flex-nowrap"-->
          <th scope="col" width="7%"  ><img src="../assets/sort.svg" width="25" height="25" class="float-right" v-on:click="addParametrsForSort('id')">ID</th>
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

//vue wdh
<!--VUE-->
<script>

export default {
  name: 'List',
  props:["userList", "deleteUserFunc"],
  data() {
    return {
      sortColumn: '',
      sortDirection:-1,
      search: ""
    }
  },
  computed: {
    searchAndSortFiles() {
      let newArray =  this.userList.slice();
      const serach = this.search.toLowerCase();
      if(serach) {
        newArray = newArray.filter(function (elem) {
          if (
                  elem.login.toLowerCase().indexOf(serach) != -1 ||
                  elem.name.toLowerCase().indexOf(serach) != -1 ||
                  String(elem.id).toLowerCase().indexOf(serach) != -1
          ) {
            return true;
          } else {
            return false;
          }
        });
      }
      const sortColumn = this.sortColumn;
      return newArray.sort((a, b) => {
        if (a[sortColumn] < b[sortColumn]) {
          return this.sortDirection
        } else {
          return -1*this.sortDirection
        }
      })
    }
  },
  methods: {
    addParametrsForSort: function (elem) {
      this.sortColumn=elem;
      this.sortDirection*=-1;
    }
  }
}
</script>

