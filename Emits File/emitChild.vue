<script setup>
  import {defineEmits} from 'vue'
  const emit = defineEmits(['mothers','valentines'])
  // 宣告要發送的事件名稱, 需用陣列型態/物件型態, 且可以放入多組

  const mothersDay = () =>{
    emit('mothers','Happy Mothers Day')
  }
  const valentinesDay = () =>{
    emit('valentines','Happy Valentines Day')
  }
  // 定義一個函式來"觸發"事件, 所以用function箭頭函式包裝emit
  // emit('名稱', '內容')
  
</script>

<template>
  <div>
    <button @click="mothersDay"> For Mom </button>
    <button @click="valentinesDay"> For Dear </button>
    <!-- 這裡要設定觸發事件 -->
  </div>
</template>
