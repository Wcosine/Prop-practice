<script setup>
  import { defineEmits, ref } from 'vue'
  const emit = defineEmits([ 'plus','minus','zero' ])

  const counter = ref(0)
  // 先定義counter 從0開始準備運算用
  
  const increase = () =>{
    counter.value++
    emit('plus', counter.value)
  }
  const decrease = () =>{
     counter.value--
     emit('minus', counter.value)
  }
  const zero = () =>{
     countNum.value = 0
     emit('zero', counter.value)
  }
</script>

<template>
  <div>
    <button @click = "increase"> Plus </button>
    <button @click = "zero"> Zero </button>
    <button @click = "decrease"> Minus </button>
  </div>
</template>
