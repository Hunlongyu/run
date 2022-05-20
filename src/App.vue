<template>
  <n-config-provider :theme="activeTheme">
   <n-layout class="container">
     <Header @themeClick="themeChange" />
     <div class="body">
       <div class="left">-</div>
       <div class="middle">90</div>
       <div class="right">+</div>
     </div>
     <div class="footer">
       <div class="meter">节拍</div>
       <div class="effect">音效</div>
       <div class="volume">音量</div>
     </div>
   </n-layout>
  </n-config-provider>
</template>

<script setup lang="ts">
import { darkTheme, lightTheme } from 'naive-ui'
import { ref } from 'vue'

const activeTheme = ref(darkTheme)

function themeChange (theme: 'system' | 'dark' | 'light') {
  console.log('theme change', theme)
  if (theme === 'dark') {
    activeTheme.value = darkTheme
  } else if (theme === 'light') {
    activeTheme.value = lightTheme
  } else if (theme === 'system') {
    const theme = window.matchMedia('(prefers-color-scheme: dark)').matches
    activeTheme.value = theme ? darkTheme : lightTheme
  }
}
</script>

<style lang="scss">
html,
body,
#app,
.n-config-provider,
.container {
  width: 100%;
  height: 100%;
  overflow-x: hidden;
  display: flex;
}
.body{
  flex: 1;
  display: flex;
}
.footer{
  height: 60px;
  display: flex;
}
</style>
