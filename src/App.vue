<template>
  <Header />
  <div class="container flex flex-col h-screen">
    <router-view />
    <footer class="p-4 bg-blue-50 mt-10">Developer ale-steinmetz.me</footer>
  </div>
</template>

<script>
import Header from '@/components/Header.vue'

export default {
  components: {
    Header
  }
}
</script>
