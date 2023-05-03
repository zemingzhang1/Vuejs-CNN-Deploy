<script setup>
import WelcomeItem from './WelcomeItem.vue'
import DragDropImageInput from "./DragDropImageInput.vue";

import DocumentationIcon from './icons/IconDocumentation.vue'
import ToolingIcon from './icons/IconTooling.vue'
import EcosystemIcon from './icons/IconEcosystem.vue'
import CommunityIcon from './icons/IconCommunity.vue'
</script>

<template>
  <WelcomeItem>
    <template #icon>
      <DocumentationIcon/>
    </template>
    <template #heading>Documentation</template>
    Project’s code and
    <a target="_blank" href="https://vuejs.org/">official documentation</a>
    provides you with all information you need to get started.
    <br/><br/>

  </WelcomeItem>

  <WelcomeItem>
    <template #icon>
      <EcosystemIcon/>
    </template>
    <template #heading>Input Image</template>
    This project is served and bundled with
    <a href="https://vitejs.dev/guide/features.html" target="_blank">Vite</a>.
    The recommended IDE setup is 
    <a href="https://code.visualstudio.com/" target="_blank">VSCode</a>.    
    More instructions are available in 
    <a href="https://code.visualstudio.com/" target="_blank"><code>README.md</code></a>.
    <br/><br/>
    🔽 Drag and drop an image below to perdict 🔽
    <DragDropImageInput/>
    <br/><br/>
  </WelcomeItem>

  <WelcomeItem>
    <template #icon>
      <ToolingIcon/>
    </template>
    <template #heading>Processing</template>
    ▶️ Images examination in details ◀️

    <br/><br/>
  </WelcomeItem>

  <WelcomeItem>
    <template #icon>
      <CommunityIcon/>
    </template>
    <template #heading>Prediction Result</template>
    <a target="_blank"><code>RESULT</code></a> it is a
    <a target="_blank">▶️<code id="result">  </code>◀️</a>
    <br/><br/>
  </WelcomeItem>

</template>
