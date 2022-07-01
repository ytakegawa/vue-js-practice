<template>
  <h1>MY MEMO APP</h1>
  <button @click="toggleNewMemoModal">ADD MEMO</button>
  <ul>
    <li v-for="memo in memos" :key="memo.title">
      <span >{{ memo.title }}</span>
      <span @click="toggleMemoDetailModal" class="command" name="memo.title">[DETAIL]</span>
      <!-- <div v-if="showMemoDetailModal">
      <MemoDetailModal>
        <h1>MEMO DETAIL</h1>
        <p>SHOW? EDIT? DELETE?</p>
        <p>TITLE</p>
        <input type="text" v-model="momo.title" >
        <p>CONTENT</p>
        <textarea v-model="momo.body">{{ memo.body }}</textarea>
        <br>
        <button @click.prevent="editMemo()">EDIT DONE</button>
      </MemoDetailModal>
      </div> -->
    </li>
  </ul>
  <div v-if="showNewMemoModal">
      <NewMemoModal>
        <h1>ADD NEW MEMO</h1>
        <p>INPUT MEMO DETAIL</p>
        <p>TITLE</p>
        <input type="text" v-model="newTitle">
        <p>CONTENT</p>
        <textarea v-model="newBody"></textarea>
        <br>
        <button @click.prevent="addMemo()">FINISH</button>
      </NewMemoModal>
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
      newTitle: '',
      newBody: '',
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
    toggleMemoDetailModal(){
      this.showMemoDetailModal = !this.showMemoDetailModal
    },
    addMemo: function () {
        const memo = {
          title: this.newTitle,
          body: this.newBody,

        }
        this.memos.push(memo)
        this.newTitle = ''
        this.newBody = ''
      },
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
  cursor: pointer;
}

</style>
