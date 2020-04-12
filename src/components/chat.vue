<template>
  <div class="chatroom">
      <div class="header">
        <p @click="leave()" class="leave">离开</p> 
      </div>
      <div class="main" id="recv">
      </div>
      <div class="tools">
        <p class="image">图片</p>
        <p @click="getHistory()" class="history">聊天记录</p>
      </div>
      <div class="inputArea">
        <input id="sendTxt" type="text"/>
        <button id="sendBtn">发送</button>
      </div>     
  </div>
</template>

<script>
export default {
  name:'chat',
  data() {

  }
}
</script>

<style>
#header{
  position: absolute;
  width: 100%;
  height: 50px;
  border:1px solid black;
}
</style>