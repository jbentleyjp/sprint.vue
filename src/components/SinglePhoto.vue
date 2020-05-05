<template>
  <div>
    <img class="single-photo" :src="`data:image/png;base64,${onePhotoKey}`" />
  </div>
</template>

<script>
export default {
  name: "SinglePhoto",
  props: ["onePhotoKey"]
};
</script>

<style scope>
.single-photo {
  width: 100%;
  height: 90vh;
}
</style>
