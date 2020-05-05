<template>
  <div id="app">
    <navbar v-on:togHome="toggleHome"/>
    <div v-if="currentView && photos.length > 1">
      <div v-for="photo in photos" :key="photo.id">
        <allphotos v-on:toggle="toggleView(photo.photoKey)" :pKey="photo.photoKey" />
      </div>
    </div>
    <div v-else>
      <singlephoto :onePhotoKey="selectedPhoto" />
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
      this.selectedPhoto = baseString;
    },
    toggleHome() {
      this.currentView = true;
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
    // console.log(this.photos);
    // return baseStrings
  }
};
</script>

<style>
#app {
  text-align: center;
}

img {
  width: 200px;
}
</style>
