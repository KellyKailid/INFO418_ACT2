<template>
  <div class="container">
    <div class="img-box" @click="toAI">
      <img src="../assets/image/ai.jpg">
    </div>
    <div class="img-box img-box2" @click="showMsg">
      <img src="../assets/image/file.png">
    </div>
    <div class="img-box" @click="toGame">
      <img src="../assets/image/game.png">
    </div>
    <div class="img-box3">
      <img src="../assets/image/molecule.jpg">
    </div>
  </div>
</template>

<script setup>
import { useRouter } from 'vue-router'

const router = useRouter()
function toAI() {
  router.push('/ai')
}
function toGame(){
  router.push('/game')
}

function showMsg() {
  ElMessage({
    showClose: true,
    message: 'Failed to open the file.',
    type: 'warning',
    duration: 0,
    offset: 100,
    grouping: true
  })
}
</script>

<style lang="scss" scoped>
.container {
  height: 100vh;
  padding: 30px;
  background-color: #171c44;
  .img-box {
    width: 60px;
    height: 60px;
    border-radius: 10px;
    overflow: hidden;
    img {
      width: 100%;
      height: 100%;
      cursor: pointer;
    }
  }
  .img-box2 {
    margin: 20px 0;
  }
  .img-box3 {
    text-align: center;
    margin-top: 120px;
  }
}

</style>
