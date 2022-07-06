<template>
  <div class="backdrops" >
    <div class="modal" >
      <h1>ADD NEW MEMO</h1>
      <p>INPUT MEMO DETAIL</p>
      <p>TITLE</p>
      <input type="text" v-model="newTitle">
      <p>CONTENT</p>
      <textarea v-model="newBody"></textarea>
      <br>
      <button @click.prevent="addMemo()">FINISH</button>
      <button @click="closeModal">CLOSE</button>
    </div>
  </div>
</template>

<script>
export default {
  props: ['memos'],
  data() {
    return {
      newTitle: '',
      newBody: '',
    }
  },
  methods: {
    closeModal(){
      this.$emit('close')
    },
    addMemo: function () {
      const memo = {
        title: this.newTitle,
        body: this.newBody,
        detailFlag: false

      }
      this.memos.push(memo)
      this.newTitle = ''
      this.newBody = ''
    },
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
    background: rgba(0, 0, 0, 0.5);
    width: 100%;
    height: 100%;
  }

  .modal h1 {
    color:black;
  }


</style>
