<template>
  <form>
    <input
      @change="uploadImage($event)"
      ref="uploadForm"
      id="file-input"
      type="file"
      accept="image / png, image / jpeg/ jpg"
    />
    <button @click="uploadButton" type="button" class="button">Upload</button>
  </form>
</template>

<script>
import { saveObject } from "../../utils/index.js";

export default {
  name: "Upload",
  methods: {
    uploadButton() {
      this.$refs.uploadForm.click();
      console.log(this.$refs, "WORKING");
      // Get event.target.files[0] here

      // Use the file object that we get here to call saveObject(file)
    },
    async uploadImage(event) {
      const uploadPicture = await saveObject(event.target.files[0]);
      console.log(uploadPicture);
    }
  }
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
