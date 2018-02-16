<template>
  <div id="app">
    <input type="text"/>
    <ul class="users">
      <li class="user" v-for="user in users" v-bind:key="user.id">
        {{user.id}}. {{user.name}} ({{user.email}})
        <span class="delete" v-on:click="deleteUser(user)">X</span>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'app',
  data () {
    return {
      users: []
    }
  },
  beforeCreate: function() {
    fetch('https://jsonplaceholder.typicode.com/users')
      .then(res => res.json())
      .then(res => this.users = res)
      .catch(err => {
        console.log(err)
      })
  },
  created: function() {
    console.log(this.users)
  },
  methods: {
    deleteUser(user) {
      this.users = this.users.filter(u => u.id !== user.id)
    },
  },
}
</script>

<style lang="scss">
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  text-align: center;
  color: #05F;
}

ul {
  list-style-type: none;
  padding: 0;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: flex-start;
}

li {
  display: inline-block;
  margin: 5px 10px;
}

a {
  color: #42b983;
}

.delete {
  color: #F00
}

</style>
