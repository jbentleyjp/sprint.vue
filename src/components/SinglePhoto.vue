<template>
  <div >
    <img :src="`data:image/png;base64,${onePhotoKey}`"/>
  </div>
</template>

<script>
export default {
  name: "SinglePhoto",
  props: ["onePhotoKey"]
};
</script>

<style scope>
img {
  width: 100%;
  height: 100%
}
</style>
