<template>
  <div id="dogForm">
    <div class="form">
      <div class="displayInfo">
        <DogPicture
          :breed="dogInfo.breed"
          :subBreed="dogInfo.subBreed"
          :dogInfo="dogInfo"
          v-on:changeInfo="changePhoto"
        />
        <h1 :style="selectedInfo">{{ dogInfo.dogName }}</h1>
        <h2 :style="selectedInfo">Sub-total: {{ dogInfo.dogValue }}</h2>
      </div>
      <div class="selectInfo">
        <SelectBreed :breedList="breedList" v-on:changeInfo="changeBreed" :dogInfo="dogInfo" />
        <SelectDogInfo v-on:changeInfo="changeDog" :dogInfo="dogInfo" />
        <input class="btn" type="button" value="Encomendar Pedido" @click="saveDog" />
      </div>
    </div>
  </div>
</template>

<script>
import API from "@/services/api";
import SelectBreed from "@/components/SelectBreed";
import SelectDogInfo from "@/components/SelectDogInfo";
import DogPicture from "@/components/DogPicture";

export default {
  name: "dogForm",
  components: {
    SelectBreed,
    SelectDogInfo,
    DogPicture
  },
  data() {
    return {
      breedList: {},
      dogInfo: {
        breed: "",
        subBreed: "",
        photo: "",
        dogName: "",
        dogSex: "",
        dogAge: "",
        dogColor: "",
        dogFont: "",
        changePhoto: "",
        dogValue: "",
      }
    };
  },
  mounted () {
    var retrievedValue = JSON.parse(localStorage.getItem("dogInfo"));
    let sum = 0;
    if ( retrievedValue.breed) sum += 10
    if ( retrievedValue.subBreed) sum += 10
    if ( retrievedValue.dogSex) sum += 10
    if ( retrievedValue.dogAge) sum += 10
    dogInfo.dogValue = sum;

  },
  computed: {
    selectedInfo() {
      return {
        "font-family": this.dogInfo.dogFont,
        color: this.dogInfo.dogColor
      };
    }
  },
  created() {
    var retrievedDog = JSON.parse(localStorage.getItem("dogInfo"));
    if (retrievedDog) {
      this.dogInfo = retrievedDog;
    }
    this.breedList = API.getAllBreeds();
  },
  methods: {
    persist () {
      localStorage.dogInfo.dogName = this.dogInfo.dogName;
    },
    changeBreed(dogInfo) {
      this.dogInfo.breed = dogInfo.breed;
      this.dogInfo.subBreed = dogInfo.subBreed;
      this.dogInfo.changePhoto = "true";
      localStorage.setItem("dogInfo", JSON.stringify(this.dogInfo));

      let sum = 0;
      if (dogInfo.breed) sum += 10
      if (dogInfo.subBreed) sum += 10
      if (dogInfo.dogSex) sum += 10
      if (dogInfo.dogAge) sum += 10
      dogInfo.dogValue = sum;

    },
    changeDog(dogInfo) {
      this.dogInfo.dogName = dogInfo.dogName;
      this.dogInfo.dogColor = dogInfo.dogColor;
      this.dogInfo.dogFont = dogInfo.dogFont;
      localStorage.setItem("dogInfo", JSON.stringify(this.dogInfo));

      let sum = 0;
      if (dogInfo.breed) sum += 10
      if (dogInfo.subBreed) sum += 10
      if (dogInfo.dogSex) sum += 10
      if (dogInfo.dogAge) sum += 10
      dogInfo.dogValue = sum;

    },
    changePhoto(dogInfo) {
      this.dogInfo.photo = dogInfo.photo;
    },
    saveDog() {
      localStorage.setItem("dogInfo", JSON.stringify(this.dogInfo));
      alert("Pedido encomendado com sucesso!");
    }
  }
};
</script>
<style>
@import url("https://fonts.googleapis.com/css?family=Barlow+Condensed|Indie+Flower|Pacifico|Roboto|Montserrat|Seymour+One&display=swap");
@media (min-width: 320px) and (max-width: 979px) {
  .form {
    display: grid !important;
  }
}
.form {
  display: flex;
  z-index: 9;
  padding: 2rem 0 0 5rem;
  font-family: "Montserrat", sans-serif;
}
@media (min-width: 320px) and (max-width: 979px) {
  .selectInfo {
    width: 440px  !important;
    margin-left: -115px  !important;
    border-radius: 0px !important;
  }
}
.selectInfo {
  display: flex;
  z-index: 2;
  flex-direction: column;
  position: relative;
  top: 0px;
  width: 500px;
  margin-left: 18px;
  background: #fff;
  padding: 75px;
  border-radius: 38px;
  -webkit-box-shadow: 0 14px 28px rgba(0,0,0,0.25), 0 10px 10px rgba(0,0,0,0.22);
  box-shadow: 0 14px 28px rgba(0,0,0,0.25), 0 10px 10px rgba(0,0,0,0.22);
}
.btn {
  font-family: "Roboto", sans-serif;
  text-transform: uppercase;
  outline: 0;
  background-color: #1673ad;
  width: 100%;
  border: 0;
  padding: 15px;
  color: #FFFFFF;
  font-size: 14px;
  -webkit-transition: all 0.3 ease;
  transition: all 0.3 ease;
  cursor: pointer;
}
.btn:hover {
  background-color: #1b5375;
  text-shadow: 0px 1px 0px #000000;
}
.btn:active {
  position: relative;
  top: 1px;
}
.inputColor {
  margin-top: 0.1rem;
  width: 50px;
}
.displayInfo {
  text-align: center;
  z-index: 2;
}
@media (min-width: 320px) and (max-width: 979px) {
  .displayInfo h1 {
    color: #fff;
    width: 55%;
    margin-bottom: 60px; 
  }
}
@media (min-width: 320px) and (max-width: 979px) {
  .displayInfo h2 {
    width: 55%;
    margin-bottom: 60px; 
  }
}
.displayInfo h1 {
  color: #fff;
}
img {
  max-height: 50vh;
  max-width: 50vw;
  vertical-align: middle;
}
select,
input {
  font-family: "Roboto", sans-serif;
  outline: 0;
  background: #f2f2f2;
  width: 100%;
  border: 0;
  margin: 0 0 15px;
  padding: 15px;
  box-sizing: border-box;
  font-size: 14px;
}
p {
  margin: 0;
  font-family: "Montserrat", sans-serif;
  font-size: 16px;
  font-weight: 600;
  margin-bottom: 5px;
}
option {
  font-family: "Montserrat", sans-serif;
}
</style>
