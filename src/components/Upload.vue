<template>
  <button class="button">Upload</button>
</template>

<script>
export default {
  name: "Upload"
};
</script>

<style scope>
.button {
  cursor: pointer;
}

input {
  position: absolute;
  left: -99999999px;
}

button {
  height: 2rem;
}
</style>
