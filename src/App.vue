<template>
  <div id="app">
    <div id="memo" class="memo">
      <h1>メモアプリ</h1>
      <p><button type="button" v-on:click="addMemo()">新規作成</button></p>
      <div v-for="(item, index) in memos" :key='index'>
        <p>
          <a v-on:click="isShow=true, content=item.content, id=item.id" >{{ item.title }}</a>
          <button type="button" class="btn btn-secondary btn-sm" v-on:click="deleteMemo(item.id)">削除</button>
        </p>
      </div>
    </div>

      <div id="show" class="memo" >
        <Show v-if="isShow" :contentsBeforeEditing='content' :idPro='id' @edit="editMemo"></Show>
      </div>
  </div>
</template>

<script>
import Show from './components/Show.vue'

export default {
  data(){
    return {
      memos: [],
      content: "",
      id: 0,
      isShow: false
    }
  },
  methods:{
    addMemo(){
      this.content = ""
      this.id = this.countId()
      this.memos.push({
        title: '',
        content: '',
        id: this.id
      })
      this.saveMemo()
      this.isShow = true
    },

    editMemo(editedContent,editedMemosId){
      const memo = this.memos.find(memo => memo.id == editedMemosId)
      let firstLine = editedContent.indexOf("\n")
      if (firstLine == -1) firstLine = editedContent.length
      console.log(firstLine)
      memo.title = editedContent.substring(0, firstLine)
      memo.content = editedContent
      this.content = ''
      this.saveMemo()
      this.isShow = false
    },

    saveMemo(){
    localStorage.setItem('memos', JSON.stringify(this.memos))
    },

    countId(){
      const ids = this.memos.map(function(o){return o.id})
      if(!ids.length) {return 1}
      else{return Math.max.apply(null,ids) +1}
    },

    deleteMemo(deleteId){
      this.memos = this.memos.filter(function (item) {
        return item.id != deleteId
      })
      this.saveMemo()
    },

    exchangeTextToArray(content){
      return content.split('\n')
    },

    loadMemo(){
      this.memos = JSON.parse(localStorage.getItem('memos'))
      if(!this.memos){ 
        this.memos = []
      }
    }
  },
  mounted(){
    this.loadMemo()
  },

  components: {
    Show
  }
}
</script>


<style>

#app {
  display: flex;
}

#memo {
  width: 50%;
  text-align:right;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  padding: 30px;
  color: #2c3e50;
}

#show {
  text-align:center;
  padding: 30px;
}

</style>
