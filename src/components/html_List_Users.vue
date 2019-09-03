<!--HTML-->
<template>
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

</template>


<!--VUE-->
<script>
export default {
  name: 'List',
  props:["userList"],
  data() {
    return {
    sortColumn: '',
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
    deleting: function (login) {
      let user=this.findThisUser(this.userList, login);
      let trueIndex= this.userList.indexOf(user);
      this.userList.splice(trueIndex, 1)
    }
  }
}
</script>

