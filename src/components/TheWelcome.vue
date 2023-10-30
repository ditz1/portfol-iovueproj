<script setup>
import WelcomeItem from './WelcomeItem.vue'
import DocumentationIcon from './icons/IconDocumentation.vue'
import ToolingIcon from './icons/IconTooling.vue'
import SupportIcon from './icons/IconSupport.vue'
</script>

<template>
  <WelcomeItem>
    <template #icon>
      <DocumentationIcon />
    </template>
    <template #heading>Documentation</template>
    <div>
        <input v-model="login.username" type="text" placeholder="username">
        <input v-model="login.password" type="text" placeholder="password">

        <br>

        <button id="loginbutton">Login</button>
        <br>
        <p id="createacc">create account if you don't have one</p>
        <input v-model="login.username" type="text" placeholder="username">
        <input v-model="login.password" type="text" placeholder="password">
        <button id="createbutton">Create</button>
    </div>

  </WelcomeItem>

  <WelcomeItem>
    <template #icon>
      <ToolingIcon />
    </template>
    <template #heading>Tooling</template>


  </WelcomeItem>

 



 

  <WelcomeItem>
    <template #icon>
      <SupportIcon />
    </template>
    <template #heading>Support Vue</template>


  </WelcomeItem>
</template>
