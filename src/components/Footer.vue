<template>
  <footer class="footer bg-light text-center py-3 mt-auto">
    <div class="container">
      <p class="mb-0">&copy; {{ currentYear }} Magazinul meu. Toate drepturile sunt rezervate. (sarcina de testare)</p>
      <small class="text-muted">Construit folosind VueJS și Bootstrap</small>
    </div>
  </footer>
</template>

<script>
export default {
  name: "AppFooter",
  data() {
    return {
      currentYear: new Date().getFullYear(),
    };
  },
};
</script>

<style scoped>
.footer {
  position: relative;
  bottom: 0;
  width: 100%;
  color: #555;
}
</style>
