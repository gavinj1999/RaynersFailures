<template>
  <div class="flex flex-col justify-between h-screen">
    <header class="h-10 bg-red-500">
      <Nav />
    </header>
    <main class="h-10 mb-auto bg-green-500">
      <Rayner />
    </main>

  </div>



</template>

<style scoped></style>
<script setup>

  import Rayner from './components/People/Rayner.vue'
  import Nav from './components/Nav.vue'

</script>