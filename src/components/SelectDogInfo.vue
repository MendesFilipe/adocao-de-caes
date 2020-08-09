<template>
  <div class="SelectDogInfo">
    <p class="pColor">Cor do cachorro:</p>
    <input class="inputColor" type="color" v-model="dogInfo.dogColor" @change="selectInfo" />
    <br />
    <p>Nome do chachorro:</p>
    <input type="text" v-model="dogInfo.dogName" @change="selectInfo" />
    <br />
    <p>Idade do chachorro:</p>
    <input type="text" v-model="dogInfo.dogAge" @change="selectInfo" />
    <p>Sexo do chachorro:</p>
    <select :style="selectStyle" v-model="dogInfo.dogFont" @change="selectInfo">
      <option id="Macho">Macho</option>
      <option id="Femea">Fêmea</option>
    </select>
  </div>
</template>

<script>
import API from "@/services/api";

export default {
  name: "SelectDogInfo",
  props: {
    breedList: {},
    dogInfo: {}
  },
  computed: {
    selectStyle() {
      return {
        "font-family": this.dogInfo.dogFont
      };
    }
  },
  methods: {
    selectInfo() {
      this.$emit("changeInfo", this.dogInfo);
    }
  }
};
</script>

<style scoped>
#font04 {
  font-family: "Roboto", sans-serif;
  font-size: 16px;
}
.pColor {
  display: block;
}

</style>
