<script setup>
import { defineProps } from 'vue'

defineProps({
  memos: Array
})

const memoTitle = (memo) => memo.content.split('\n')[0]
</script>

<template>
  <div id="memo-list">
    <h1>メモ一覧</h1>
    <ul>
      <li v-for="memo in memos" :key="memo.id">
        <a href="#" @click="$emit('edit', memo.id)">{{ memoTitle(memo) }}</a>
      </li>
      <button @click="$emit('add')">+</button>
    </ul>
  </div>
</template>

<style scoped></style>
