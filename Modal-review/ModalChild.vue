<script setup>
import { defineEmits, defineProps } from 'vue'

const prop = defineProps({
  visible: Boolean,
  showCloseX: {
    type: Boolean,
    default: true,
  },
  // 以布林值做設定視窗的"X"按鈕是否開啟
  closeOnBackdropClick:{
    type: Boolean,
    default: true,
  }
  // 以布林值做設定點擊背景時關閉視窗
})

const emit = defineEmits(['close'])
// 設定一個事件名稱叫做close
const close = () =>{
  emit('close')
}
// 定義close事件
// emit('名稱', '內容'), 僅使用第一個變數, 表示通知父組件這個事件發生了

const handleBackdropClick = () =>{
  if(prop.closeOnBackdropClick){
    // 如果prop.closeOnBackdropClick = true
    close()
    // 觸發關閉指令
  }
}
</script>

<template>
  <div v-if="visible" @click.self="handleBackdropClick" class="modal-backdrop">  
  <!--
      #補充說明:
      - v-if控制視窗開關, 預設為true
      - @click.self, 當點擊事件發生在自己的時候, 觸發handleBackdropClick(點擊背景關閉)
  -->
    <div class="modal">
      
      <!-- Header slot -->
      <div class="modal-header">
        <div class="modal-header-content">
          <slot name="header"></slot>
          <!-- 父組件由此處新增架構或內容, 其餘為固定模板 -->
          <!-- 父組件使用方式: <template #header> -->
        </div>
        <button v-if="showCloseX" @click="close" class="modal-close">&times;</button>
         <!--
            #補充說明:
            - v-if控制showCloseX "X"是否顯示, 預設為true
            - @click="close", 當點擊事件發身時, 觸發emit(close)
            - &times; 顯示"x"
          -->
        
        <!-- default slot -->
        <div class="modal-body">
          <slot></slot>
        </div>
        
        <!-- Footer slot -->
        <div class="modal-footer">
          <slot name="footer">
            <button @click="close">關閉</button>
          </slot>
        </div>
        
      </div>
  </div>
</template>

<style scoped>
.modal-backdrop {
  position: fixed;
  top: 0; left: 0; right: 0; bottom: 0;
  background: rgba(0, 0, 0, 0.5);
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 999;
}
.modal {
  background: white;
  width: 400px;
  border-radius: 8px;
  overflow: hidden;
  box-shadow: 0 4px 10px rgba(0,0,0,0.2);
}
.modal-header, .modal-footer {
  padding: 1rem;
  background: #f2f2f2;
  display: flex;
}
.modal-header-content {
  flex-grow: 1;
}
.modal-body {
  padding: 1rem;
}
.modal-close {
  border: none;
  background: none;
  font-size: 1.2rem;
  cursor: pointer;

}
</style>

<!-- 以上文件參考 @ivesho modal-thinking教學 -->
<!-- 此文件僅用於個人筆記 -->
