<template>    
    <navbar/>
    <main class="max[1200px] mx-auto">
      <router-view/>
    </main>
    <footer-layout/>
</template>

<script setup>
    import navbar from '../components/Navbar.vue'
    import footerLayout from '../components/FooterLayout.vue'
</script>