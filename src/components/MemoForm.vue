<script setup>
import { ref, watch } from 'vue'
import { defineProps, defineEmits } from 'vue'

const props = defineProps({
  memo: Object
})
const emits = defineEmits(['save', 'delete', 'back'])

const memoContent = ref(props.memo.content)

watch(
  () => props.memo.content,
  (newContent) => {
    memoContent.value = newContent
  }
)

const save = () => {
  emits('save', { ...props.memo, content: memoContent.value })
}

const deleteMemo = () => {
  emits('delete', props.memo.id)
}
</script>

<template>
  <div id="memo-detail">
    <h1>メモ詳細</h1>
    <textarea v-model="memoContent" rows="5" cols="33"></textarea>
    <div class="button-area">
      <button class="save-button" @click="save">保存</button>
      <button class="delete-button" @click="deleteMemo">削除</button>
      <button class="back-button" @click="$emit('back')">一覧に戻る</button>
    </div>
  </div>
</template>

<style scoped>
button {
  padding: 5px 20px;
  border: none;
  border-radius: 5px;
  color: #fff;
}
.save-button {
  background-color: #1e90ff;
}
.delete-button {
  background-color: #dc143c;
}
.back-button {
  background-color: #696969;
}
</style>
