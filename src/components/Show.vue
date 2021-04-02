<template>
  <div>
    <h1>メモの詳細</h1>
    <p><textarea class="textarea" v-bind:value="contentCom=contentPro" v-on:input="contentCom=$event.target.value" placeholder="内容を入力して下さい" ></textarea></p>
    <p><button type="button" v-on:click="editMemo()">保存・更新</button></p>
  </div>
</template>

<script>
export default {
  props: {
    contentPro: String,
    idPro: Number,
  },
  data(){
    return {
      contentCom: ""
    }
  },
  methods:{
    editMemo(){
      console.log(this.contentCom)
      console.log(this.id)
      this.$emit("edit", this.contentCom, this.idPro);
    }
  }
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

textarea {
  min-width: 200px;
  min-height: 200px;
  max-width: 500px;
  max-height: 500px;
}

</style>
