<script setup>
import { ref } from 'vue';
import WelcomeItem from './WelcomeItem.vue';
import DocumentationIcon from './icons/IconDocumentation.vue';
import ToolingIcon from './icons/IconTooling.vue';
import SupportIcon from './icons/IconSupport.vue';

var uid = 0;

// Data for login
const login = {
  username: ref(''),
  password: ref(''),
};

// Data for registration
const register = {
  username: ref(''),
  password: ref(''),
};

const displayUID = (uid) => {
  var uiddis = document.getElementById('uiddisplay');
  uiddis.textContent = "signed in as: " + uid;
}
const displayName = (name) => {
  var namedis = document.getElementById('namedisplay');
  namedis.textContent = "signed in as: " + name;
}

const handleLogin = () => {
  if (login.username.value && login.password.value) {
    loginCredentials(login.username.value, login.password.value);
    console.log(`Logging in with: ${login.username.value}`);
    getUserID(login.username.value);
    // Implement real login logic here
  }
};

const handleRegister = () => {
  if (register.username.value && register.password.value) {
    console.log(`Registering with: ${register.username.value}`);
    createCredentials(register.username.value, register.password.value);
    getUserID(register.username.value);
    
    // Implement real registration logic here
  }
};
const getUserID = (name) => {
    fetch('http://35.188.225.12/backend/getuid.php', {
        method: 'POST',
        headers: {
            'Content-Type': 'application/json'
        },
        body: JSON.stringify({
            name: name
        })
    })
    .then(response => response.json())
    .then(data => {
        if (data.status === 'success') {
            console.log("User found with UID:", data.data.uid);
            uid = data.data.uid;
            console.log("user id:" + uid);
            displayUID(uid);
            //uidtext.textContent = "user id: " + uid;
            //loadFolioDisplay();
        } else if (data.status === 'error') {
            console.log("Error:", data.message);
        }
    })
    .catch(error => {
        console.log('Error:', error);
    });
}
const createCredentials = (name, password) => {
    fetch('http://35.188.225.12/backend/newcreate.php', {
        method: 'POST',
        headers: {
            'Content-Type': 'application/json'
        },
        body: JSON.stringify({
            name: name,
            password: password
        })
    })
    .then(response => response.text())
    .then(data => {
        console.log(data + "test");
        if (data.length < 18){
          console.log("account created");
          //getUserID(name);            
       
        }
    })
    .catch(error => {
        console.log('Error:', error);
        
    });
}

const loginCredentials = (name, password) => {
    fetch('http://35.188.225.12/backend/signin.php', {
        method: 'POST',
        headers: {
            'Content-Type': 'application/json'
        },
        body: JSON.stringify({
            name: name,
            password: password
        })
    })
    .then(response => response.text())
    .then(data => {
        console.log(data + "test");
        if (data.trim() === "User signed in successfully!"){
            getUserID(name);
            displayName(name);
            console.log("user signed in");
        }
    })
    .catch(error => {
        console.log('Error:', error);
    });
}
</script>

<template>
  <WelcomeItem>
    <template #icon>
      <DocumentationIcon />
    </template>
    <template #heading>Documentation</template>
    <div>
        <h3>login if you have an account</h3>  
        <input v-model="login.username.value" type="text" placeholder="username">
        <br>
        <input v-model="login.password.value" type="password" placeholder="password">
        <br>
        <button id="loginbutton" @click="handleLogin">Login</button>
        
        <h3>create account if you don't have one</h3>
        <input v-model="register.username.value" type="text" placeholder='username'>
        <br>
        <input v-model="register.password.value" type="password" placeholder="password">
        <br>
        <button id="createbutton" @click="handleRegister">Create</button>
    </div>
  </WelcomeItem>

  <WelcomeItem>
    <template #icon>
      <ToolingIcon />
      <br>
      
    </template>
      <template #heading>user id</template>
      <div>
        <h3 id="uiddisplay">not yet logged in</h3>
      </div>
    </WelcomeItem>
    <WelcomeItem>
    <template #icon>
      <SupportIcon />
    </template>
    <template #heading>signed in as</template>
    <div>
      <h3 id="namedisplay">not yet logged in</h3>
    </div>
  </WelcomeItem>
</template>

<!-- Add your styles here if needed -->
<style scoped>
/* your styles */
</style>
