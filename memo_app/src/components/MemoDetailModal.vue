<template>
  <div class="backdrops" >
    <div class="modal">
      <h1>MEMO DETAIL</h1>
      <p>SHOW? EDIT? DELETE?</p>
      <button @click="$_MemoDetailModal_deleteMemo">DELETE</button>
      <p>TITLE</p>
      <input type="text" v-model="memo.title" >
      <p>CONTENT</p>
      <textarea v-model="memo.body">{{ memo.body }}</textarea>
      <br>
      <button @click="$_MemoDetailModal_closeModal">CLOSE</button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'MemoDetailModal',
  props: {
    memos: Array
  },
  data() {
    return {
      memo: this.memos.find((memo) => memo.detailFlag === true)
    }
  },
  methods: {
    $_MemoDetailModal_closeModal(){
      this.$emit('detail')
      this.$emit('close')
    },
    $_MemoDetailModal_deleteMemo(){
      if (!confirm('delete finished?')) {
        return
      }
      const newMemos = this.memos.filter((m) => m !== this.memo)
      this.$emit('delete', newMemos)
      this.$emit('close')
    }
  }
}
</script>

<style scoped>
  .modal {
    width: 400px;
    padding: 20px;
    margin: 100px auto;
    background: white;
    border-radius: 10px;
  }

  .backdrops {
    top: 0;
    position: fixed;
    background: rgba(0, 0, 0, 0.3);
    width: 100%;
    height: 100%;
  }

  .modal h1 {
    color:black;
  }
</style>
