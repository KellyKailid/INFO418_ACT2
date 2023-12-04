<template>
  <div class="container" ref="scrollRef">
    <div class="left">
      <div class="img-box">
        <img src="../assets/image/ai.jpg">
      </div>
      <div>Version: 3.2.1</div>
      <div class="time">Last Update: 01/11/2023</div>
      <div class="btn" @click="router.back()">Return</div>
    </div>
    <div class="right">
      <div class="item" v-for="(item, index) in list" :key="index">
        <div  class="ai">{{ index % 2 === 0 ? 'AI' : 'YOU' }}</div>
        <div v-if="item.startsWith('<img')" v-html="item" class="ai-image"></div>
        <div v-if="!item.startsWith('<img')" class="message">{{ item }}</div>
      </div>
      <el-input v-model="content" @change="handleChange" placeholder="Send a message" />
    </div>
  </div>
</template>

<script setup>
import { ref, nextTick } from 'vue'
import { useRouter } from 'vue-router'

const router = useRouter()
const scrollRef = ref()
const content = ref('')
const list = ref([
 'Welcome to the 2023 AI. What can I do for you?',
])

function handleChange(e) {
  let text = '';

  if (/^look$/i.test(e)) {
    // If the user inputs "look," show an image
    text = '<img src="../assets/image/w.jpg" alt="Look Image" width="50%">';
  } else if (/^yes[!|！]{0,1}$/i.test(e)) {
    text = 'Would you like me to do some research on making molecules? If so, type look to see it.';
  } else {
    text = `Sorry, I don't know. Would you like to see a suggested question? Yes or No`;
  }

  list.value.push(e, text);
  content.value = '';

  nextTick(() => {
    scrollRef.value.scrollTop = scrollRef.value.scrollHeight;
  });
}
</script>

<style lang="scss" scoped>

.container {
  display: flex;
  justify-content: space-between;
  height: 100vh;
  background-color: #242021;
  color: #ffffffdd;
  padding: 0 20px 0px;
  overflow-y: auto;
  .left {
    text-align: center;
    margin-right: 80px;
    .img-box {
      width: 200px;
      img {
        width: 100%;
      }
    }
    .time {
      margin-top: 6px;
    }
  }
  .right {
    flex: 1;
    margin-top: 200px;
    .item {
      display: flex;
      align-items: center;
      margin-bottom: 20px;
      .ai {
        display: flex;
        align-items: center;
        justify-content: center;
        min-width: 42px;
        height: 42px;
        border-radius: 50%;
        border: 2px solid #ffffffdd;
        margin-right: 16px;
      }
      .ai-image {
        img {
          max-width: 100%;
          border-radius: 8px;
        }
      }
      .message {
        color: #ffffffdd;
      }
    }
    .el-input {
      width: 400px;
      margin: 32px 0;
      :deep(.el-input__wrapper) {
        background-color: transparent;
        &.is-focus {
          box-shadow: 0 0 0 1px #fff inset;
        }
      }
      :deep(.el-input__inner) {
        color: #ffffffdd;
      }
    }
  }
  .btn {
    width: 80px;
    height: 30px;
    line-height: 30px;
    padding: 0 10px;
    margin: 20px auto;
    font-size: 14px;
    border: 1px solid #ffffffdd;
    border-radius: 15px;
    cursor: pointer;
  }
}
</style>
