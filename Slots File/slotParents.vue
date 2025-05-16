<script setup>
  import {ref} from 'vue'
  import slotChild from './slotChild.vue'
  
  const greeting = ref('dynamic') // 控制動態具名插槽 msg
  const noteInfo = ref('note')    // 控制動態具名插槽 note
  
  const showNote = ref(false)  
  const toggleShow = () =>{
    showNote.value = !showNote.value
  }
</script>


<template>
  <!--以下靜態具名插槽內容-->
  <slotChild> 
    <template #hello>
      <h1>This is slot practice.</h1>
    </template>
  </slotChild>
  <!--靜態具名插槽內容結束-->

  
  <!--以下動態具名插槽內容-->
  <slotChild :msg="greeting">                 <!--綁定子組件命名為msg的prop, 宣告新值為greeting-->
    <template #dynamic>                       <!--greeting值, 即為插件新定義的動態名稱-->   
      <h3>This is dynamic a Slot.</h3>
    </template>
  </slotChild>
  <!--動態具名插槽內容結束-->
  
  <!--以下不具名插槽內容-->
  <button @click="toggleShow"> Show Note </button>
  <!--不具名插槽內容結束-->
  
  <!--以下動態具名插槽 + fallback內容-->
  <slotChild :note="noteInfo">                 <!--綁定子組件命名為note的prop, 宣告新值為noteInfo-->
    <template #[noteInfo] v-if="showNote" >    <!--noteInfo值, 即為插件新定義的動態名稱-->
                                               <!--動態變數寫法 #[noteInfo] 不能寫成 #noteInfo, 這是靜態變數-->
      <h3>This is Note.</h3>   
    </template>
  </slotChild>
  <!--靜態具名插槽內容結束-->  
</template>

