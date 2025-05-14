<script setup>
  import { ref } from 'vue'
  import emitChild from './emitChild.vue'
  
  const message = ref('')
  //設定一個儲存位置放子組件帶來的資料

  const forMom = (msg) =>{
    // 命名子組件內容為 msg 帶入父組件
    message.value = msg
  }
  const forDear = (msg) =>{
    // 命名子組件內容為 msg 帶入 父組件
    message.value = msg
  }
  //接收並處理子組件來的資料
  
</script>

<template>
<emitChild @mothers="forMom" @valentines="forDear"/>
<!-- 這裡要監聽子組件的動作,所以要用子組件定義的名稱 -->
<h1> {{ message }} </h1>
</template>
