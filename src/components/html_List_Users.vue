<!--HTML-->
<template>
    <div  class="container py-5 text-center">

      <input type="text" class="form-control text-center col-3  m-auto" v-model="search" placeholder="Поиск пользователя">
      <p></p>

      <table class="table table-bordered table-dark">
          <thead>
            <tr>
    <!--         class="d-flex flex-nowrap"-->
              <th scope="col" width="7%"  ><img src="../assets/sort.svg" width="25" height="25" class="float-right" v-on:click="addParametrsForSort('id')">ID</th>
              <th scope="col"><img src="../assets/sort.svg" width="25" height="25" class="float-right" v-on:click="addParametrsForSort('name')">Имя</th>
              <th scope="col"><img src="../assets/sort.svg" width="25" height="25" class="float-right" v-on:click="addParametrsForSort('login')">Логин</th>
                <template v-if = "userLogin === 'Admin'">
                    <th scope="col" width="20%">Изменить пароль</th>
                </template>
            </tr>
            </thead>
            <tbody>
            <tr v-for="user in searchAndSortFiles">
              <td>{{user.id}}</td>
              <td>{{user.name}}</td>
                <template v-if = "userLogin === 'Admin'">
                    <td>{{user.login}}<img src = "../assets/cancel.svg" width="25" height="25" class="float-right" v-on:click = "deleteUserFunc(user.id)"></td>
                    <td><img src = "../assets/exchange.svg" width="25" height="25"  v-on:click = "userID=user.id; $bvModal.show('bv-modal-example3')" ></td>
                </template>
                <template v-else>
                    <td>{{user.login}}<img src = "../assets/cancel.svg" width="25" height="25" class="float-right"</td>
                </template>
            </tr>
            </tbody>
      </table>
<!--        модальное окно-->
        <div class="text-center">
            <b-modal id="bv-modal-example3" ref="my-modal" hide-footer="" header-bg-variant="light">
                <template slot="modal-title"><h4 class="text-dark">Измените пароль пользователя и повторите его</h4></template>
                <div class="d-block text-right">
                    <form ref="form">
                        <b-form-group class="text-left" label="Новый пароль">
                            <b-form-input type="text" v-model="newPasswordUser"></b-form-input>
                        </b-form-group>
                        <b-form-group class="text-left" label="Повторите новый пароль">
                            <b-form-input type="text" v-model="newPasswordUserAgain"></b-form-input>
                        </b-form-group>
                        <b-button class="mx-2" type="button"  variant="danger" data-dismiss="my-modal" @click="$bvModal.hide('bv-modal-example3')">Отмена</b-button>
                        <b-button type="button" variant="primary"  v-on:click="changePasswordClick(userID)">Изменить пароль</b-button>
                    </form>
                </div>
            </b-modal>
        </div>
    </div>


</template>

<!--VUE-->
<script>

export default {
  name: 'List',
  props:["userList", "deleteUserFunc", "userLogin", "changePassword"],
  data() {
    return {
      sortColumn: '',
      sortDirection:-1,
      search: "",
      newPasswordUser: "",
      newPasswordUserAgain:"",
      userID:null
    }
  },
  computed: {
    searchAndSortFiles() {
      let newArray =  this.userList.slice();
      const search = this.search.toLowerCase();
      if(search) {
        newArray = newArray.filter(function (elem) {
          if (
                  elem.login.toLowerCase().indexOf(search) != -1 ||
                  elem.name.toLowerCase().indexOf(search) != -1 ||
                  String(elem.id).toLowerCase().indexOf(search) != -1
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
    },
      showModalWindow(id) {
          this.changeModalShow = true
          this.userID = id
      },
    changePasswordClick: function (id) {
        this.userID=id;
        this.changePassword(this.userID, this.newPasswordUser, this.newPasswordUserAgain);
        this.newPasswordUser="";
        this.newPasswordUserAgain="";
        this.$bvModal.hide('bv-modal-example3')
    }
  }
}
</script>

