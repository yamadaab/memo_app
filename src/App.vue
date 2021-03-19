<template>
  <div id="app">
    <div id="nav">
      <Memo :memos='memos'></Memo>
      <div v-for="(item, index) in memos" :key='index'>
        <label>
          <div>{{ item.title }}</div>
        </label>
          <button type="button" class="btn btn-secondary btn-sm" v-on:click="deleteMemo(item.id)">削除</button>
      </div>
    </div>
    <router-view/>
  </div>
</template>

<script>
import Memo from './components/Memo.vue'

export default {
  data(){
    return {
      memos: [
        {title: "111", content: "メモ１", id: 1},
        {title: "222", content: "メモ２", id: 2},
        {title: "333", content: "メモ３", id: 3}
      ],
      memo: ""
    }
  },
  methods:{
    addMemo(){

    },
    deleteMemo(deleteId){
      this.memos = this.memos.filter(function (item) {
        return item.id != deleteId
      })
      // this.saveTodo()
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