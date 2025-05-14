<script setup>
  const props = defineProps({
    // 定義資料的形式
    id: Number, //數字型態
    name: String, //字串型態
    age: Number //數字型態
  });
</script>

<template>
  <div class="card">
    <p>ID編號: {{ props.id }}</p>
    <p>姓名: {{ props.name }}</p>
    <p>年齡: {{ props.age }}</p>
  </div>
   <!-- 設定資料的顯示方式/格式/排版 -->
</template>

<style scoped>
  .card{
    display: inline-block;
    vertical-align: top;
    margin-right: 20px;
    padding: 0 20px;
    border: 1px solid #333;
  }
</style>
