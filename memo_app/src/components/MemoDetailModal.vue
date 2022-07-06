<template>
  <div class="backdrops" >
    <div class="modal">
      <h1>MEMO DETAIL</h1>
      <p>SHOW? EDIT? DELETE?</p>
      <p>TITLE</p>
      <input type="text" :value="selectedMemo().title">
      <p>CONTENT</p>
      <textarea>{{ selectedMemo().body }}</textarea>
      <br>
      <button @click.prevent="editFinish(index)">EDIT FINISH</button>
      <button @click="closeModal">CLOSE</button>
    </div>
  </div>
</template>

<script>
export default {
  props: ['memos'],
  data() {
    return {
      // selectMemoTitle: selectedMemo().title,
      // selectMemoBody: selectedMemo().body
    }
  },
  methods: {
    selectedMemo(){
      const selectMemo = this.memos.find(memo => memo.detailFlag = true)
      return selectMemo
    },
    editFinish: function (index) {
      this.memos[index].detailFlag = false
    },
    closeModal(){
      this.$emit('close')
      this.$emit('detail')
    }
  },
  // computed: {
  //   selectedMemo(){
  //     const selectMemo = this.memos.find(memo => memo.detailFlag = true)
  //     return selectMemo
  //   }
  // }
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
