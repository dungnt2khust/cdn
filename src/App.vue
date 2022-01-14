<template>
  <div>
    <div>Upload Image</div>
    <ik-image width="400" :path="path" />
    <ik-upload
      :fileName="fileName"
      :tags="['animal']"
      :onError="onError"
      folder="Animals"
      :onSuccess="onSuccess"
    />
    <button @click="showMethod">Show Methods</button>
  </div>
</template>
<script>
import Vue from "vue";
import ImageKit, { IKUpload } from "imagekitio-vue";
Vue.use(ImageKit, {
  urlEndpoint: "https://ik.imagekit.io/uvn3cxjawn6",
  publicKey: "public_Rk9tSR2EEq/ahhSc5lLKIUrIYTM=",
  authenticationEndpoint: "https://rwc87.sse.codesandbox.io/auth",
});
export default {
  name: "App",
  data() {
    return {
      path: "/default-image.jpg",
      fileName: "conmeo",
    };
  },
  methods: {
    showMethod() {
      console.log(IKUpload);
    },
    onError(err) {
      console.log("Error");
      console.log(err);
    },
    onSuccess(res) {
      console.log("Success");
      console.log(res);
      this.path = res.filePath;
    },
  },
};
</script>