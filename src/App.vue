<template>
  <div class="container">
    <Header title="USER CRUD" />
    <UserList />
  </div>
</template>

<script>
import Header from './components/Header'

import UserList from './components/UserList'
export default {
  name: 'App',
  components: {
    Header,
    UserList,
  }
}
</script>

