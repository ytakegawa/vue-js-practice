<template>
  <h1>MY MEMO APP</h1>
  <button @click="toggleNewMemoModal">ADD MEMO</button>
  <ul>
    <li v-for="(memo, index) in memos" :key="memo.title">
      <span >{{ memo.title }}</span>
      <span @click="toggleMemoDetailModalOpen(index)" class="command">[DETAIL]</span>
    </li>
  </ul>
  <div v-if="showNewMemoModal">
    <NewMemoModal
      @createMemo="addMemo"
      @close="toggleNewMemoModal"
    />
  </div>
  <div v-if="this.memo">
    <MemoDetailModal
      :memo="memo"
      @delete="deleteMemo"
      @close="toggleMemoDetailModalClose"
    />
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
      memos: [],
      memo: null,
      showNewMemoModal: false,
    }
  },
  mounted: function () {
    this.memos = JSON.parse(localStorage.getItem('memos')) || []
  },
  methods: {
    toggleNewMemoModal(){
      this.showNewMemoModal = !this.showNewMemoModal
    },
    toggleMemoDetailModalOpen(index){
      this.memo = {
        id: this.memos[index].id,
        title: this.memos[index].title,
        body: this.memos[index].body
      }
    },
    toggleMemoDetailModalClose(){
      this.memos.map( (memo) => {
        if (memo.id === this.memo.id) {
          memo.title = this.memo.title
          memo.body = this.memo.body
        }
      })
      this.saveMemos(this.memos)
      this.memo = null
    },
    deleteMemo(deleteMemoId){
      const newMemos = this.memos.filter((memo) => memo.id !== deleteMemoId)
      this.memos = newMemos
    },
    addMemo(newMemo){
      if(this.memos.length) {
        const lastId = Math.max(...this.memos.map((memo) => memo.id))
        newMemo.id = lastId + 1
      }
      else {
        newMemo.id = 1
      }
      this.memos.push(newMemo)
      this.saveMemos(this.memos)
    },
    saveMemos(memos){
      localStorage.setItem('memos', JSON.stringify(memos))
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
