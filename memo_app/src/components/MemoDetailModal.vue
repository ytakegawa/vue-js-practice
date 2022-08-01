<template>
  <div class="backdrops" >
    <div class="modal">
      <h1>MEMO DETAIL</h1>
      <p>SHOW? EDIT? DELETE?</p>
      <button @click="deleteMemo">DELETE</button>
      <p>TITLE</p>
      <input type="text" v-model="memo.title" >
      <p>CONTENT</p>
      <textarea v-model="memo.body">{{ memo.body }}</textarea>
      <br>
      <button @click="closeModal">CLOSE</button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'MemoDetailModal',
  props: ['memo'],
  methods: {
    closeModal(){
      this.$emit('detail')
      this.$emit('close')
    },
    deleteMemo(){
      if (!confirm('Are you sure (to delete)?')) {
        return
      }
      this.$emit('delete', this.memo.id)
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
