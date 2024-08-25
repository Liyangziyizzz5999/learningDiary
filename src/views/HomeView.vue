<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png">
    <HelloWorld msg="Welcome to Your Vue.js + TypeScript App"/>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import HelloWorld from '@/components/HelloWorld.vue' // @ is an alias to /src

const inputArray = ['4', '10']

for (const ele of inputArray) {
  const num = Number(ele)
  if (!num) {
    console.log(1)
    continue
  }
  // dp[i][j]表示把i分成最多j个正整数的不重复方案数字 即i的j拆分
  const solution = (num: number) => {
    const dp: number[][] = [[]]
    for (let i = 1; i <= num; i++) {
      dp[i] = []
      for (let j = 1; j <= num; j++) {
        if (i === 1 || j === 1) {
          dp[i][j] = 1
        } else if (i === j) {
          dp[i][j] = dp[i][j - 1] + 1
        } else if (i < j) {
          dp[i][j] = dp[i][i]
        } else {
          dp[i][j] = dp[i - j][j] + dp[i][j - 1]
        }
      }
    }
    console.log(dp[num][num], dp)
  }
  solution(num)
}

export default defineComponent({
  name: 'HomeView',
  components: {
    HelloWorld
  }
})
</script>
