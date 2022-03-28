<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <a v-on:click="getGreeting">get</a>
    <h1>{{ info }}</h1>
    <a v-on:click="removeGreeting">remove</a>
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
      info: null
    }
  },
  methods: {
    getGreeting() {
      axios
        .get('http://localhost:8000')
        .then(response => (this.info = response.data.message))
        .catch(e => {this.info = "エラー！！　"+e})
    },
    removeGreeting() {
      this.info = null
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
