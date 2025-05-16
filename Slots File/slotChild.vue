<script setup>
  defineProps({
    msg:{
      type: String,
      default: "", 
      // 設定default是為了即使沒有傳資料也不會出錯
    },
    note:{
      type: String,
      default: "", 
    } 
  })
</script>

<template>
  <slot/> <!--這是不具名插槽-->
  
  <slot name="hello"/> <!--具名插槽(又稱靜態插槽)-->
  
  <slot :name="msg"/> <!--結合props的具名插槽(又稱動態插槽)-->
  
  <slot :name="note" v-if="$slots[note]"> <!--包含fallback機制的動態插槽)-->
    <p>There's nothing here.</p> <!--父組件沒有填寫內容時出現的預設值)-->
  </slot>
</template>

<!--補充內容-->
<!-- 
  #fallback機制: 
  - 在定義動態插槽時可以加入fallback機制, 避免在未傳入任何資訊時產生空白畫面
  
  #寫法:
    <slot :name="msg" v-if="$slots[msg]"/>
  
  #說明:
    1. msg是子組件傳來的prop, 會決定我要顯示的slot是哪一個
    2. $slots 是 Vue 自帶的變數，裡面會存入所有傳進來的插槽
    3. $slots[msg]意思是「父元件有沒有傳一個叫 msg 的插槽？」
    4. 如果有就顯示 <slot :name="msg" />，如果沒有就顯示 fallback 文字
    5. 父組件要寫成 #[msg] 才會是動態插槽
-->





  
