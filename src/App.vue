<script setup>
import { ref, reactive } from 'vue'
const isIframeVisible = ref(false)
const iframeSrc = ref('')
let paramsData = reactive('')

paramsData = {
  account: 'hanan-bhat',
  project: 'New Proj',
  author: 'Hanan',
  tenant: 'Zenken',
  token: '',
  url: 'https://customerhearingsystem.netlify.app',
}

iframeSrc.value = `${paramsData.url}/?account=${paramsData.account}&project=${paramsData.project}&author=${paramsData.author}&tenant=${paramsData.tenant}`

const showIframe = () => {
  isIframeVisible.value = true
}

const closeIframe = (event) => {
  console.log('Hello')
  const iframeContainer = document.querySelector('.iframe-container')
  console.log(iframeContainer.contains(event.target))
  console.log(iframeContainer)
  if (iframeContainer && iframeContainer.contains(event.target)) {
    isIframeVisible.value = false
    console.log(isIframeVisible)
  }
}
</script>

<template>
  <button @click="showIframe">Report Issue</button>
  <div v-if="isIframeVisible" class="iframe-container" @click="closeIframe">
    <iframe ref="myIframe" :src="iframeSrc" width="100%" height="400"></iframe>
  </div>
</template>

<style scoped>
.iframe-container {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  z-index: 9999;
  background-color: rgba(0, 0, 0, 0.5);
}

.iframe-container iframe {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  width: 80%;
  height: 80%;
  border: none;
  z-index: 10000;
}
</style>
