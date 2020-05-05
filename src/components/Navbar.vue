<template>
  <div class="navbar">
    <h1 @click="$emit('togHome')" class="navbar-header">{{ title }}</h1>
    <upload />
  </div>
</template>

<script>
import Upload from "./Upload.vue";

export default {
  name: "Navbar",
  components: {
    upload: Upload
  },
  data: () => ({
    title: "Home"
  })
};
</script>

<style scoped>
.navbar {
  padding: 2rem;
  display: flex;
  justify-content: flex-end;
  background-color: #1c7e88;
}

.navbar-header {
  cursor: cell;
  margin-right: auto;
}
</style>
