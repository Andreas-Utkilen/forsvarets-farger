<template>
  <div 
    class="wrapper"
  >
    <img
      src="@/assets/logo.svg"
      alt="Forsvaret - Logo"
    >
    <DropDown
      @selected="updateSelected"
    />
    <div
      class="container"
    >
      <Color
        v-for="(color, i) in primaryColors"
        :key="i"
        :selected="selected"
        :name="color.name"
        :hex="color.hex"
        :rgb="color.rgb"
        :cmyk="color.cmyk"
        :dark="color.dark"
        @clicked="clicked"
      />
    </div>
    <div
      class="container"
    >
      <template
        v-for="(color, i) in secondaryColors"
      >
        <Color
          v-if="color.name != ''"
          :key="i"
          :selected="selected"
          :name="color.name"
          :hex="color.hex"
          :rgb="color.rgb"
          :cmyk="color.cmyk"
          :dark="color.dark"
          @clicked="clicked"
        />
        <div
          v-else
          :key="i"
          class="dummy"
        >
        </div>
      </template>
    </div>
    <Overlay
      :hex="copyHex"
      :color="copyColor"
      :dark="dark"
      :style="{ display: showOverlay ? 'block' : 'none' }"
    />
  </div>
</template>

<script>
import Color from "./Color";
import DropDown from "./DropDown";
import Overlay from "./Overlay";

export default {
  name: 'Colors',
  components: {
    Color,
    DropDown,
    Overlay
  },
  data: () => ({
    copyHex: "",
    copyColor: "",
    dark: false,
    showOverlay: false,
    selected: "hex",
    primaryColors: [
      {
        name: "Sort",
        hex: "#191B21",
        rgb: "426",
        cmyk: "94 77 53 94",
        dark: true
      },
      {
        name: "Lys grønn",
        hex: "#F1F2F0",
        rgb: "7541",
        cmyk: "5 1 2 2"
      },
      {
        name: "Grønn",
        hex: "#C6C7C4",
        rgb: "420",
        cmyk: "6 4 7 11"
      },
      {
        name: "Lys blå",
        hex: "#E2E6E9",
        rgb: "649",
        cmyk: "10 3 1 0"
      },
      {
        name: "Beige",
        hex: "#E3DDD8",
        rgb: "7528",
        cmyk: "5 10 17 15"
      },
      {
        name: "Lys grå",
        hex: "#F5F7F8",
        rgb: "CG1",
        cmyk: "4 2 4 8"
      },
      {
        name: "Lys beige",
        hex: "#EDE9E8",
        rgb: "7527",
        cmyk: "3 4 14 8"
      },
      {
        name: "Gul",
        hex: "#EFBD4E",
        rgb: "116",
        cmyk: "0 14 100 0"
      }
    ],
    secondaryColors: [
      {
        name: "Deep ocean",
        hex: "#123C69",
        rgb: "3025",
        cmyk: "100 27 10 56",
        dark: true
      },
      {
        name: "Sea",
        hex: "#557A95",
        rgb: "307",
        cmyk: "100 22 2 18",
        dark: true
      },
      {
        name: "Sky",
        hex: "#7BB2CB",
        rgb: "298",
        cmyk: "67 2 0 0"
      },
      {
        name: "Light sky",
        hex: "#ABD8F9",
        rgb: "2905",
        cmyk: "45 1 0 1"
      },
      {
        name: "Soil",
        hex: "#8D5F5F",
        rgb: "505",
        cmyk: "11 53 25 31"
      },
      {
        name: "Earth",
        hex: "#BD9090",
        rgb: "501",
        cmyk: "3 31 13 8"
      },
      {
        name: "Koral",
        hex: "#EE8C8C",
        rgb: "700",
        cmyk: "0 43 8 0"
      },
      {
        name: "Dusk",
        hex: "#FCC7C7",
        rgb: "510",
        cmyk: "0 31 3 0"
      },
      {
        name: "Teal",
        hex: "#254E58",
        rgb: "3155",
        cmyk: "100 10 28 47",
        dark: true
      },
      {
        name: "Seagreen",
        hex: "#457E8C",
        rgb: "3145",
        cmyk: "100 11 28 20",
        dark: true
      },
      {
        name: "Freshwater",
        hex: "#88BDBC",
        rgb: "5493",
        cmyk: "48 4 16 15"
      },
      {
        name: "Cold breeze",
        hex: "#CDF1E9",
        rgb: "621",
        cmyk: "12 1 9 2"
      },
      {
        name: "",
        hex: "",
        rgb: "",
        cmyk: ""
      },
      {
        name: "",
        hex: "",
        rgb: "",
        cmyk: ""
      },
      {
        name: "",
        hex: "",
        rgb: "",
        cmyk: ""
      },
      {
        name: "Lys grå",
        hex: "#D9C3DA",
        rgb: "524",
        cmyk: "11 23 0 0"
      }
    ]
  }),
  methods: {
    updateSelected: function (value){
      this.selected = value;
    },
    clicked: function (hex, color, dark) {
      this.copyHex = hex;
      this.copyColor = color;
      this.dark = dark;
      this.showOverlay = true;
      setTimeout(() => {
        this.showOverlay = false;
      }, 1500);
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.wrapper {
  width: 100%;
  max-width: 1080px;
  margin: 0 auto;
}
img {
  display: block;
  height: 64px;
  margin: 0 auto;
}
.container {
  display: grid;
  grid-template-columns: repeat(8, 9%);
  gap: 4%;
  margin-top: 50px;
  margin-bottom: 150px;
}
@media only screen and (max-width: 991px) {
  .container {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-between;
  }
  .dummy {
    display: none;
  }
} 
</style>
