<template>
  <n-config-provider :theme="activeTheme">
   <n-layout class="container">
     <Header @themeClick="themeChange" />
     <n-button type="warning">Warning</n-button>
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
  height: 100%;
  overflow-x: hidden;
}
</style>
