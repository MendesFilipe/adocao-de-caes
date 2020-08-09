<template>
  <div class="DogPicture">
    <img
      :src="imgSrc"
    />
  </div>
</template>

<script>
import API from "@/services/api";

export default {
  name: "DogPicture",
  props: {
    breed: {},
    subBreed: {},
    dogInfo: {},
    changePhoto: {}
  },
  computed: {
    imgSrc: function() {
      if (this.dogInfo.changePhoto != "") {
        return this.loadImage();
      } else {
        return this.dogInfo.photo;
      }
    }
  },
  methods: {
    loadImage() {
      if (this.dogInfo.subBreed !== "") {
        this.dogInfo.photo = API.getImageBySub(
          this.dogInfo.breed,
          this.dogInfo.subBreed
        ).message;
        this.dogInfo.changePhoto = "";
        this.$emit("changeInfo", this.dogInfo);
        return this.dogInfo.photo;
      } else {
        this.dogInfo.photo = API.getImageBy(this.dogInfo.breed).message;
        this.dogInfo.changePhoto = "";
        this.$emit("changeInfo", this.dogInfo);
        return this.dogInfo.photo;
      }
    }
  }
};
</script>

<style scoped>
.DogPicture {
  height: 50vh;
  width: 50vw;
  text-align: center;
  padding: auto 0;
  line-height: 50vh;
}
</style>
