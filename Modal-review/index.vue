<script setup>
import { ref } from 'vue'
import ModalChild from './ModalChild.vue';

const messages = ref([
  {id:1, author:"Anne" ,content: "這是練習", time: "2025-05-13 14:32" },
  {id:2, author:"Bryan" ,content: "這是試煉!" ,time: "2025-05-14 15:20"},
  {id:3, author:"Chloe" ,content: "天要亡我..." ,time: "2025-05-15 12:15"},
  {id:4, author:"Dora" ,content: "我終將無所不能!" ,time: "2025-05-16 18:58"},
])

// 開啟新增留言按鈕設定
// 設定初始值
const showNewModal = ref(false) // 這是顯示視窗(prop:visible)的值, false為關閉
const newMessage = ref({
  author: "",
  content: "",
})
// 設定新增留言按鈕的動作
const openNewMessageModal = () =>{
  showNewModal.value = true,
  newMessage.value = { author: '', content: '' }
}
// 開啟新增留言按鈕設定結束

// 查看詳情按鈕設定
const showDetailModal = ref(false)
const selectedMessage = ref(null) // 儲存我選到的值

const openDetailModal = (msg_id) =>{
  selectedMessage.value = messages.value.find(x => x.id == msg_id);
  // .find()第一個選到的值, 會成為selectedMessage的值(一整個物件)
  // 找尋方法: 設定每個元素為x, 將x.id跟msg_id做匹配
  if(!selectedMessage.value){
    // 如果找不到對應的值, 發出警告
    alert('這個留言掉進時空漩渦回不來了');
    return;
  }
  showDetailModal.value = true
  // 找到值, 就顯示
}
// 查看詳情按鈕設定結束

// 提交新增留言設定
const submitNewMessage = () =>{
  const newId = messages.value.length + 1
  // 新的ID值為 messages的物件長度+1
  messages.value.push({
    id: newId,
    author: newMessage.value.author,
    content: newMessage.value.content,
    // newMessage 為初始值設定的儲存空間, 會記錄輸入的內容
    time: new Date().toLocaleString('zh-TW',{hour12: false}),
    // new Date()為物件, Date()為字串無法被使用
    // .toLocaleString() 意在轉換成現代人普遍閱讀的字串模式, 加上('地區',時制)
    // hour12: false 意思是使用 24 小時制
  })
  // messages內容列需包含以上id、author、content、time的key才可以在這被使用
}
// 提交新增留言設定結束

</script>

<template>
    <h1>留言板</h1> 
    <button @click="openNewMessageModal">新增留言</button>
    <ul class="message-list">
      <li v-for="{id, author, content} of messages" :key="id" class="message-item">
      <!-- 迴圈帶入messages資料 -->  
        <div>
          <strong>{{ author }}:</strong> "{{ content }}"
        </div>
        <button @click="openDetailModal(id)">查看詳情</button>
        <!-- 當我點擊button時, (id)傳入openDetailModal, 即為msg_id帶入 -->
      </li>
    </ul> 
    <!--以上是不包含在modalChild(子組件)模板內的畫面-->

  <!--新增留言彈出模板-->
  <ModalChild
    :visible="showNewModal"
    :showCloseX="true"
    @close="showNewModal = false"
  > <!--註2-->
    <template #header>
      <h3>新增留言</h3>
    </template>
    <form class="newMsgModalHeader" @submit.prevent="submitNewMessage">
    <!-- .prevent 是防止提交時自動重新整理畫面 -->
        <label>
          作者：
          <input v-model.trim="newMessage.author" type="text" ></input>
          <!-- v-model綁定輸入的值, trim可以去除空白格 -->
        </label>
        <label>
          內容：
          <textarea v-model.trim="newMessage.content" type="text"></textarea>
        </label>
    </form>
    <template #footer>
      <button type="submit" form="newMsgModalHeader">送出留言</button>
      <!--註3-->
    </template>
    <!-- 用模板的方式帶入footer, 實現模組化 -->
  </ModalChild>
  <!--新增留言彈出模板結束-->

  <!--查看詳情彈出模板-->
  <ModalChild
    :visible="showDetailModal"
    :showCloseX="true"
    @close="showDetailModal = false"
  >
    <template #header>
      <h3>留言詳情</h3>
    </template>
    <p><strong>作者：</strong>{{ selectedMessage.author }}</p>
    <p><strong>內容：</strong>{{ selectedMessage.content }}</p>
    <p><strong>時間：</strong>{{ selectedMessage.time }}</p>
  </ModalChild>
  <!--查看詳情彈出模板結束-->
  <!--註1-->

</template>

<!--
    #註解
    1. slot命名一樣(#header), 透過點擊事件判別畫面應出現的樣式, 且須將兩者分開呼叫
    2. 綁定prop visible、showCloseX和emit @close, 設定值傳給子組件, 控制視窗開關
    3. 提交button沒有被放在form當中，被拆成兩個區塊(slot)放置，為避免結構綁死，使用 form="xxx" 指定 form id，實現跨 slot 提交
-->

<style scoped>
.message-list {
  list-style: none;
  padding: 0;
}

.message-item {
  margin: 1rem 0;
  padding: 1rem;
  border: 1px solid #ccc;
  border-radius: 6px;
}

.newMsgModalHeader {
  display: flex;
  flex-direction: column;
  gap: 1.5rem;
}
</style>
