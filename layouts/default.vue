<template lang="">
    <div>
        <p>Default layout </p>
        <nav>
             <nuxt-link :to="`/`">Home</nuxt-link>
        </nav>
        <slot />
    </div>
</template>
<script>
export default {
    
}
</script>
<style lang="">
    
</style>