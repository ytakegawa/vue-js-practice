<template>
  <h1>MY MEMO APP</h1>
  <button @click="toggleNewMemoModal">ADD MEMO</button>
  <ul>
    <li v-for="(memo, index) in memos" :key="memo.title">
      <span >{{ memo.title }}</span>
      <span @click="toggleMemoDetailModal(index)" class="command">[DETAIL]</span>
    </li>
  </ul>
  <div v-if="showNewMemoModal">
      <NewMemoModal :memos="memos"
        @close="toggleNewMemoModal"
      />
  </div>
  <div v-if="showMemoDetailModal">
      <MemoDetailModal :memos="memos"
        @close="toggleMemoDetailModal"
        @detail="MemoDetailFlagOff"
        @delete="updatedMemos"
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
    toggleMemoDetailModal(index){
      this.showMemoDetailModal = !this.showMemoDetailModal
      this.memos[index].detailFlag = true
    },
    MemoDetailFlagOff(){
      this.memos.map( memo => memo.detailFlag = false)
    },
    updatedMemos(newMemos){
      this.memos = newMemos
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
