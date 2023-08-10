


<script setup>

import { useRoute } from 'vue-router'
import { workspaceList } from '../../store/global.js'
const route = useRoute();

console.log(workspaceList.value)
</script>


<template>

  <h1>Workspace {{ route.params.id }}</h1>

</template>

<style>
    
</style>