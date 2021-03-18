<template>
  <div id="app">
    <div id="nav">
      <Memo></Memo>
    </div>
    <router-view/>
  </div>
</template>

<script>
import Memo from './components/Memo.vue'

export default {
  data(){
    return {
      name: "kiyokiyo",
    }
  },
  methods:{
    add1(count){
      this.count1 = count;

    }
  },

  components: {
    Memo
  }
}
</script>


<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

#nav {
  padding: 30px;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
}

#nav a.router-link-exact-active {
  color: #42b983;
}
</style>