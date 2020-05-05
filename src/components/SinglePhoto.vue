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
  width: 50%;
  height: 50%
}
</style>
