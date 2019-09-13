<!--HTML-->
<template>
    <div  class="container py-5 text-center">
      <p> user:{{authorizedUser}} </p>
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
        <tr v-for="user in userSortList">
          <td>{{user.id}}</td>
          <td>{{user.name}}</td>
          <td>{{user.login}}</td>
          <td>{{user.password}} <img src="../assets/cancel.svg" width="25" height="25"
                                     class="float-right"  v-on:click="deleteUserFunc(user.id)"></td>
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
      sortDirection:-1
    }
  },
  computed: {
    userSortList: function () {
      const sortColumn = this.sortColumn;
        return this.userList.slice().sort((a, b) => {
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
      return (this.sortColumn=elem, this.sortDirection*=-1 )
    }
  }
}
</script>

