<script setup>
import MemoForm from './components/MemoForm.vue'
import MemoList from './components/MemoList.vue'
</script>

<template>
  <header>
    <h1>MemoApp</h1>
  </header>
  <div class="memo-content">
    <MemoList />
    <MemoForm />
  </div>
</template>

<style scoped>
header {
  line-height: 1.5;
}
</style>
