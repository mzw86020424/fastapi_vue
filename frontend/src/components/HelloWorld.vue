<template>
  <div class="hello">
    <h1>{{ msg }}</h1>

    <h3>GET USER</h3>
    <input type="text" v-model="userId" placeholder="user id">
    <button v-on:click="getUser">get user</button>
    <h3>POST USER</h3>
    <input type="email" v-model="email" placeholder="email">
    <input type="password" v-model="password" placeholder="password">
    <button v-on:click="postUser">post user</button>
    <h1>{{ data }}</h1>
    <a v-on:click="removeData">remove</a>
  </div>
</template>

<script>
import axios from 'axios';
export default {
  name: 'HelloWorld',
  props: {
    msg: String,
  },
  data() {
    return {
      data: null,
      userId: null,
      email: null,
      password: null,
    }
  },
  methods: {
    getUser() {
      axios
        .get(`http://localhost:8000/users/${this.userId}`)
        .then(response => (this.data = "user:" + response.data.id + " is exists!"))
        .catch(this.data = "user:" + this.userId + " is not exists.")
    },
    postUser() {
      axios
        .post(`http://localhost:8000/users/`,{
          "email": this.email,
          "password": this.password,
        })
        .then(response => (this.data = "user:" + response.data.id + " is created!"))
        .catch(e => {this.data = "エラー！！　"+e})
    },
    removeData() {
      this.data = null
    }
  },
}
</script>

<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
