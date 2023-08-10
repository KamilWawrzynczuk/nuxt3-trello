
<script lang='ts' setup>
import { ref } from 'vue'

type Workspace = {
    id: Number,
    name: String,
}

const newWorkspaceName = ref('')

const workspaceList = ref(<Workspace[]>[])

const createWorkspace = () => {
    const randomId = Math.floor(Math.random() * 100)

    workspaceList.value.push({
        id: randomId,
        name: newWorkspaceName.value,
    })

}
</script>


<template>
    <h1>Home Page</h1>
    <h2>Recently Viewed</h2>
    <h2>Workspaces</h2>
    <button @click="createWorkspace()">Create a Workspace</button>
    <input type="text" v-model="newWorkspaceName"> 
    <ul class="workspace-list">
        <li v-for="workspace in workspaceList" :key="workspace.id" class="workspace-card">
          {{ workspace.id }}: {{ workspace.name }}
        </li>
    </ul>
</template>

<style>
.workspace-card{
    display: block;
    border: 2px solid black;
    border-radius: 15px;
    padding: 15px;
    margin-bottom: 5px;
}
.workspace-list {
    margin-left: 0;
    padding-left: 0 ;
}
</style>