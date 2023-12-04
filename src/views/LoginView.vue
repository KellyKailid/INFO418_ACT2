<template>
  <div class="container">
    <div class="content">
      <div class="left">
        <img src="../assets/image/shake.png">
      </div>
      <div class="right">
        <div>Welcome</div>
        <div class="to">To</div>
        <div>Molecule Maker Lab Institute</div>
        <div>
          <el-input type="password" show-password v-model="password" @change="handleChange" placeholder="Type In Password..." />
          <div class="error" :style="{'visibility': isError ? 'visible': 'hidden'}">Hint: What leads to progress?</div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import { useRouter }  from 'vue-router'

const password = ref('')
const isError = ref(false)
const router = useRouter()

function handleChange(e) {
  console.log('e', e);
  if(e === 'failure') {
    router.push('/')
    sessionStorage.setItem('token', 'login success')
    isError.value = false
  } else {
    isError.value = true
  }
}

</script>

<style lang="scss" scoped>
.container {
  position: relative;
  height: 100vh;
  background-color: #000000;
  .content {
    position: absolute;
    display: flex;
    align-items: center;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    width: 90%;
    .left {
      margin-right: 100px;
      width: 450px;
      height: 470px;
      img {
        height: 100%;
      }
      
    }
    .right {
      display: flex;
      flex-direction: column;
      align-items: center;
      /* flex: 1; */
      color: #ffffffdd;
      font-size: 36px;
      height: 270px;
      .to {
        margin: 12px 0;
      }
      .el-input {
        width: 400px;
        margin-top: 32px;
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
      .error {
        color: #ff000088;
        font-size: 16px;
        margin-top: 16px;
      }
    }
  }
}
</style>