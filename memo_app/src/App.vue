<template>
  <h1>MY MEMO APP</h1>
  <button @click="toggleNewMemoModal">ADD MEMO</button>
  <ul>
    <li v-for="memo in memos" :key="memo.title">
      <span >{{ memo.title }}</span>
      <span @click="toggleMemoDetailModal()" class="command">[DETAIL]</span>
      <!-- <div v-if="showMemoDetailModal">
        <MemoDetailModal :title="memo.title" :body="memo.body">
        <h1>MEMO DETAIL</h1>
        <p>SHOW? EDIT? DELETE?</p>
        <p>TITLE</p>
        <input type="text" value="title">
        <p>CONTENT</p>
        <textarea></textarea>
        <br>
        <button @click.prevent="editMemo()">EDIT DONE</button>
        </MemoDetailModal>
      </div> -->
    </li>
  </ul>
  <div v-if="showNewMemoModal">
      <NewMemoModal :memos="memos" @close="toggleNewMemoModal" />
  </div>

  <div v-if="showMemoDetailModal">
      <MemoDetailModal :memos="memos" @close="toggleMemoDetailModal" @detail="toggleMemoDetailFlag" />
        <!-- <div v-for="memo in memos" :key="memo.title">
          <h1>MEMO DETAIL</h1>
          <p>SHOW? EDIT? DELETE?</p>
          <p>TITLE</p>
          <input type="text" :value="memo.title">
          <p>CONTENT</p>
          <textarea>{{ memo.body }}</textarea>
        </div>

        <br>
        <button @click.prevent="editMemo()">EDIT DONE</button> -->
      <!-- </MemoDetailModal> -->
  </div>

</template>

<script>
import NewMemoModal from './components/NewMemoModal.vue'
import MemoDetailModal from './components/MemoDetailModal.vue'

export default {
  name: 'App',
  components: { NewMemoModal, MemoDetailModal },
  data() {
    return {
      // newTitle: '',
      // newBody: '',
      memos: [],
      // selectMemoTitle: this.memo.title,
      // selectMemoBody: this.memo.body,
      showNewMemoModal: false,
      showMemoDetailModal: false
    }
  },
  watch: {
    memos: {
      handler: function () {
        localStorage.setItem('memos', JSON.stringify(this.memos))
      },
      deep: true
    }
  },
  mounted: function () {
    this.memos = JSON.parse(localStorage.getItem('memos')) || []
  },
  methods: {
    toggleNewMemoModal(){
      this.showNewMemoModal = !this.showNewMemoModal
    },
    toggleMemoDetailModal(){
      this.showMemoDetailModal = !this.showMemoDetailModal
    },
          // this.memos[index].detailFlag = !this.memos[index].detailFlag
      // this.memos.map( memo => memo.detailFlag = false)
    toggleMemoDetailFlag(){
      this.memos.map( memo => memo.detailFlag = false)
    }
    // addMemo: function () {
    //     const memo = {
    //       title: this.newTitle,
    //       body: this.newBody,
    //       detailFlag: false

    //     }
    //     this.memos.push(memo)
    //     this.newTitle = ''
    //     this.newBody = ''
    //   },
  },
  computed: {
    matchMemoData: function(){

    }
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
  margin-top: 60px;
}

#app ul {
  font-size: 20px;
  padding: 0;
  list-style: none;
}

#app li {
  margin-bottom: 10px;
}

.command {
  font-size: 9px;
  cursor: pointer;
}

</style>
