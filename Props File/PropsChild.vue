<script setup>
  const props = defineProps({
    // 定義資料的形式
    id: {
      type : Number, //數字型態
      default : 0,
    }, 
    name: {
      type: String, //字串型態
      default : (""),
    },
    age: {
      type : Number, //數字型態
      default : 0,
    }
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
