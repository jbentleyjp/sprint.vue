<template>
  <div id="app">
    <!-- <img alt="Vue logo" src="./assets/logo.png" /> -->
    <!-- <h1>{{ title }}</h1> -->
    <navbar />
    <div v-for="photo in photos" :key="photo.id">
      <!-- {{console.log("keysssss>>>",photo.key)}} -->
      <allphotos :photoKey="photo.photoKey" />
    </div>
  </div>
</template>

<script>
import Navbar from "./components/Navbar";
import AllPhotos from "./components/AllPhotos";
import { getSingleObject, listObjects } from "../utils/index.js";

export default {
  name: "App",
  components: {
    navbar: Navbar,
    allphotos: AllPhotos
  },
  data: () => ({
    // title: "Photo Upload App",
    currentView: true,
    photos: [],
    selectedPhoto: ""
  }),
  created: async function() {
    const listPhotos = await listObjects();
    const photoKeys = await Promise.all(listPhotos.map(photo => photo.Key));

    const baseStrings = await Promise.all(
      photoKeys.map((photo, index) => {
        let tmp = {};
        tmp["id"] = index;
        // tmp["key"] = getSingleObject(photo).then();
        getSingleObject(photo).then(key => (tmp["photoKey"] = key));
        return tmp;
      })
    );
    this.photos = baseStrings;
    // console.log(baseStrings);
    // return baseStrings
  }
};
</script>

<style>
#app {
  text-align: center;
}
</style>
