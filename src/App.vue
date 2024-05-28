<script setup>
import { ref } from 'vue'
import MemoList from './components/MemoList.vue'
import MemoForm from './components/MemoForm.vue'

const memos = ref(JSON.parse(localStorage.getItem('memos')) || [])
const displayForm = ref(false)
const currentMemo = ref(null)

const addMemo = () => {
  currentMemo.value = { id: Date.now(), content: '新規メモ' }
  displayForm.value = true
}

const editMemo = (id) => {
  currentMemo.value = memos.value.find((memo) => memo.id === id) || { id, content: '' }
  displayForm.value = true
}

const saveMemo = (memo) => {
  const index = memos.value.findIndex((m) => m.id === memo.id)
  if (index !== -1) {
    memos.value[index] = memo
  } else {
    memos.value.push(memo)
  }
  localStorage.setItem('memos', JSON.stringify(memos.value))
  backToList()
}

const deleteMemo = (id) => {
  memos.value = memos.value.filter((memo) => memo.id !== id)
  localStorage.setItem('memos', JSON.stringify(memos.value))
  backToList()
}

const backToList = () => {
  displayForm.value = false
}
</script>

<template>
  <div id="app">
    <MemoList :memos="memos" @edit="editMemo" @add="addMemo" />
    <MemoForm
      v-if="displayForm"
      :memo="currentMemo"
      @save="saveMemo"
      @delete="deleteMemo"
      @back="backToList"
    />
  </div>
</template>

<style scoped></style>
