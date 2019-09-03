<template>
  <div id="app">
    <ListUsers/>
  </div>
</template>

<script>
import ListUsers from './components/html_List_Users.vue'  //импортирую файл

export default {
  name: 'app',
  components: {
    ListUsers     //ListUsers нужно сделать в 3-х местах APP
  }
}
</script>


