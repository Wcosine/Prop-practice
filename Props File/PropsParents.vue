<script setup>
  import { reactive } from 'vue'
  import PropsChild from './PropsChild.vue'
  
  let id = 0;
  const list = reactive([
    { id: id++, name: 'Alice', age: 23},
    { id: id++, name: 'Benson', age: 28},
    { id: id++, name: 'Jason', age: 49},
    // 要注意跟子層的型態設定一致
  ])
</script>

<template>
  <!--  <PropsChild />帶入子層的排版, 將.card的內容帶入父層呈現 -->
  <PropsChild 
    v-for="item in list"
    :id = "item.id + 1"
    :name = "item.name"
    :age = "item.age"
    :key = "item.id" />
    <!--  v-for迴圈帶出list資料, 並使用v-bind綁定各物件的資料 -->
</template>
