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
//如果沒有設定此項, closeOnBackdropClick會引發不管按何處都會關閉彈出視窗的狀況
</script>

<template>
  <div v-if="visible" @click.self="handleBackdropClick" class="modal-backdrop">  
  <!--
      #補充說明:
      - v-if控制視窗開關, 沒有此項彈出視窗將無法關閉, 由父組件決定其值
      - @click.self, 當點擊事件發生在自己的時候, 觸發handleBackdropClick(點擊背景關閉)
  -->
    <div class="modal">

      <!-- 彈出視窗的畫面模板 -->
      <div class="modal-header">
        <div class="modal-header-content">
          <slot name="header"></slot>
          <!-- 這是跳出視窗模板的表頭, 透過父組件讓此元件可以被重複利用 -->
          <!-- 父組件由此處新增架構或內容, 其餘為固定模板 -->
          <!-- 父組件使用方式: <template #header> -->
        </div>
        <button v-if="showCloseX" @click="close" class="modal-close">&times;</button>
      </div>
      <!--彈出視窗模板結束-->
      <!--
        #補充說明:
        - v-if控制showCloseX "X"是否顯示, 由父組件決定其值
        - @click="close", 當點擊事件發生時, 觸發emit(close)
        - &times; 顯示"x"
      -->
      
      <!--彈出視窗的body-->  
      <div class="modal-body">
        <slot></slot>
      </div>
      <!--彈出視窗body結束-->  

      <!--彈出視窗的footer -->
      <div class="modal-footer">
        <slot name="footer">
          <button @click="close">關閉</button>
          <!--按下子元件 button → 執行 close() → emit('close') → 外層（父層）接收 → 觸發showDetailModal = false-->
        </slot>
      </div>
      <!--彈出視窗footer結束 -->  
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
