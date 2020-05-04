<template>
  <div>
    <img
      @click="$emit('toggle')"
      :src="`data:image/png;base64,${photoKey}`"
    />
  </div>
</template>

<script>
export default {
  name: "AllPhotos",
  props: ["photoKey"]
};
</script>

<style scope>
img {
  width: 244px;
  height: 244px;
  display: grid;
  grid-template-columns: repeat(5, 1fr);
  grid-template-rows: repeat(5);
  column-gap: 10px;
  row-gap: 10px;
}
</style>


  <!-- <img v-bind:src="'data:image/jpeg;base64,'+imageBytes" /> -->
    <!-- <img :src= data:image/jpg;base64 -->

