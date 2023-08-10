


<script setup>

import { useRoute } from 'vue-router'
import { workspaceList } from '../../store/global.js'
const route = useRoute();

let workspaceName = ''


onMounted(()=>{
  workspaceName = workspaceList.value.filter(workspace => {
    return workspace.id === Number(route.params.id);
  })
})
</script>


<template>

  <h1>{{ workspaceName[0]?.name }} workspace {{ route.params.id }}</h1>

</template>

<style>
    
</style>