<template lang="">
    <div>
        <header class="main-header">
            <p class='logo'>Trello MVP clone with Nuxt 3</p>
        <nav class='main-nav'>
             <nuxt-link :to="`/`">Home</nuxt-link>
        </nav>
        </header>
        
        <slot />
    </div>
</template>
<script>
export default {
    
}
</script>
<style lang="css">
    html,
    body{
        margin: 0;
        padding: 0;
        font-family: "Robot", sans-serif;
    }
    .main-header{ 
        background-color: #41b883;
        padding: 15px;
        display: flex;
        justify-content: space-between;
        align-items: center;
    }

    .main-nav a {
        color: #fff;
        text-decoration: none;
    }
    .logo{
       color: #fff;
       font-weight: bold; 
       margin: 0;
       padding: 0;
    }
</style>