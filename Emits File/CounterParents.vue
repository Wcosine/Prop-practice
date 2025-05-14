<script setup>
  import { ref } from 'vue'
  import CounterChild from './CounterChild.vue'

  const counterTimes = ref(0)
  // 除了設定一個空間儲存子組件帶來的資料, 也為了初始內容為 0
  // 畫面顯示 : Count : 0 times
  
  const plus = (value) =>{
    // value 為 子組件輸入的值
    counterTimes.value = value++
  }
  const minus = (value) =>{
    counterTimes.value = value--
  }
  const zero = (value) =>{
    counterTimes.value = value
  }
  
</script>

<template>
  <CounterChild @increace="plus" @decreace="minus" @zero="zero"/>
  <p>Count : {{ counterTimes }} times</p>
  <!-- 會自動解套, 所以不用加".value" -->
</template>
