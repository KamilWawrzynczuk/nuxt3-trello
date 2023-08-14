
<script setup>
import { ref } from 'vue'
import { workspaceList } from '../store/global.js'

const newWorkspaceName = ref(' ')
const createWorkspace = () => {
    const randomId = Math.floor(Math.random() * 100)

    workspaceList.value.push({
        id: randomId,
        name: newWorkspaceName.value,
    })

    newWorkspaceName.value= ''
}
</script>

<template>
    <main class="main-content">
        <h1>Home Page</h1>
        <h2>Workspaces</h2>
      
        <input type="text" v-model="newWorkspaceName" @keyup.enter="createWorkspace()" style='width:100%; padding: 5px; font-size: 1rem; margin-bottom: 10px;'/> 
        <button @click="createWorkspace()" style="padding: 10px 5px;">Create a Workspace</button>
        <ul class="workspace-list">
        
            <li v-for="workspace in workspaceList" :key="workspace.id" class="workspace-card">
            <nuxt-link :to="`/workspace/${workspace.id}`">
                {{ workspace.id }}: {{ workspace.name }}
            </nuxt-link>  
            </li>
        </ul>
    </main>
   
</template>

<style>
.workspace-card{
    display: block;
    border: 2px solid black;
    border-radius: 4px;
    padding: 15px;
    margin-bottom: 5px;
}
.workspace-list {
    margin-left: 0;
    padding-left: 0 ;

    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 10px;
}

.main-content{
    padding: 30px;
}

.main-content h1 {
    margin-top: 0;
}
</style>