<template>
<div class="header">
  <div class="left"></div>
  <div class="right">
    <n-button v-show="theme === 'dark'" text color="#f36100" @click="changeTheme('light')"><n-icon size="30"><Sunny /></n-icon></n-button>
    <n-button v-show="theme === 'light'" text color="#f36100" @click="changeTheme('dark')"><n-icon size="30"><Moon /></n-icon></n-button>
  </div>
</div>
</template>
<script setup lang="ts">
import { Moon, Sunny } from '@vicons/ionicons5'
import { onMounted, ref } from 'vue'

const emits = defineEmits(['themeClick'])
const theme = ref('')

function changeTheme (t: 'light' | 'dark') {
  emits('themeClick', t)
  theme.value = t
  localStorage.setItem('theme', t)
}

function getTheme () {
  const lsTheme = localStorage.getItem('theme')
  if (lsTheme) {
    emits('themeClick', lsTheme)
    theme.value = lsTheme
  } else {
    emits('themeClick', 'system')
    const t = window.matchMedia('(prefers-color-scheme: dark)').matches
    console.log('=t',t)
    theme.value = t ? 'dark' : 'light'
    localStorage.setItem('theme', theme.value)
  }
}

onMounted(() => {
  getTheme()
})
</script>
<style lang="scss">
.header{
  height: 60px;
  display: flex;
  align-items: center;
  justify-content: space-between;
  border: 1px solid #000;
  .right{
    margin-right: 10px;
  }
}
</style>