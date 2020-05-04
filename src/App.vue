<template>
  <div id="app">
    <navbar />
    <div v-if="currentView">
      <div v-for="photo in photos" :key="photo.id">
        <allphotos
        v-on:toggle="toggleView(photo.photoKey)"
        :photoKey="photo.photoKey" />
      </div>
    </div>
    <div v-else>
      <singlephoto :onePhotoKey="selectedPhoto"/>
    </div>
  </div>
</template>

<script>
import Navbar from "./components/Navbar";
import AllPhotos from "./components/AllPhotos";
import SinglePhoto from "./components/SinglePhoto";
import { getSingleObject, listObjects } from "../utils/index.js";

export default {
  name: "App",
  components: {
    navbar: Navbar,
    allphotos: AllPhotos,
    singlephoto: SinglePhoto
  },
  data: () => ({
    currentView: true,
    photos: [],
    selectedPhoto: ""
  }),
  methods: {
    toggleView(baseString) {
      this.currentView = false;
      console.log(baseString);
      this.selectedPhoto = baseString;
    }
  },
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
