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
  props:["userList", "deleteUserFunc"],
  data() {
    return {
      sortColumn: '',
      sortDirection:-1
    }
  },

  computed:{
    // userSortList: function(){   //длинная функция сортировки
    //   // console.log('this.userList',this.userList);
    //   const sortColumn = this.sortColumn;
    //   if (this.sortDirection===-1) {
    //     return this.userList.slice().sort((a, b)=> {
    //       if (a[sortColumn] < b[sortColumn]) {
    //         return -1
    //       } else {
    //         return 1
    //       }
    //     });
      // }
      // else {
      //   return this.userList.slice().sort((a, b) => {
      //     if (a[sortColumn] < b[sortColumn]) {
      //       return 1
      //     } else {
      //       return -1
      //     }
      //   });
  //     }
  //   }
  // },
    sortSomething: function (thing, array, k) {
      array.sort(function (a, b) {
          if (a[thing] < b[thing]) {
              return -1*k
          } else {return k}
      })
    },
    userSortList: function() {
        const sortColumn = this.sortColumn;
        let directionSort = Number(this.sortDirection || 1);
        this.sortSomething(sortColumn, this.userList, directionSort)
    }
  // methods:{
    // deleting: function (login) {     //только с клиентской частью
    //   let user=this.findThisUser(this.userList, login);
    //   let trueIndex= this.userList.indexOf(user);
    //   this.userList.splice(trueIndex, 1)
    // },

    // findThisUser: function(list, trueLogin) {
    //   for (let i = 0; i < list.length; i++) {
    //     if (list[i].login === trueLogin) {
    //       return list[i]
    //     }
    //   }
    //   return false
    // }
    }
}
</script>

