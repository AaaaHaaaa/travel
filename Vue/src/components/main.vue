<template>
  <div class="dialogue-container">
    <ul>
      <li v-for="item in talks.dialogue" :key="item.id" class="dialogue-item">
        <div class="ai-response">
          <div class="avatar ai-avatar"></div>
          <div class="response">{{ item.response }}</div>
        </div>
        <div class="user-question">
          <div class="avatar user-avatar"></div>
          <div class="request">{{ item.request }}</div>
        </div>
      </li>
    </ul>
  </div>
</template>  
  
<script setup>
import { defineProps } from "vue";
const props = defineProps(["talks"]);
</script>  
  
<style scoped>
.dialogue-container {
  background-color: #f9f9f9;
  border-radius: 8px;
  max-height: 450px;
  overflow-y: auto;
}

.dialogue-item {
  display: flex;
  flex-direction: column-reverse;
  align-items: flex-start;
  margin-bottom: 15px;
}

.ai-response,
.user-question {
  display: flex;
  align-items: center;
  margin-bottom: 5px;
  width: 100%;
}

.avatar {
  width: 40px;
  height: 40px;
  border-radius: 50%;
  margin-right: 10px;
  background-color: #ccc;
}

.user-avatar {
  background-image: url("https://pic.616pic.com/ys_bnew_img/00/05/09/Ewz0Ve3BTc.jpg");
  background-size: cover;
}

.ai-avatar {
  background-image: url("https://docs.dknowc.cn/20220424/1531/41fbc4a5-2ebc-488f-8427-e205c7d19960/%E5%BD%A9%E6%99%BA%E6%9C%BA%E5%99%A8%E4%BA%BA.png");
  background-size: cover;
}

.request,
.response {
  background-color: #fff;
  padding: 10px;
  border-radius: 5px;
  max-width: calc(100% - 50px);
  word-wrap: break-word;
  border: 1px solid #ddd;
}

.response {
  background-color: #e0f7fa;
}

.request {
  background-color: #ffe0b2;
}
</style>