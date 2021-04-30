<template>
  <div
    :style="{ background: hex }"
    class="overlay"
  >
    <h1
      :style="{ color: dark ? '#fff' : '#191B21' }"
    >
    {{ color }} kopiert til utklippstavlen!
    </h1>
  </div>
</template>

<script>
export default {
  name: 'Overlay',
  props: {
    hex: String,
    color: String,
    dark: Boolean
  },
  methods: {
    onChange: function () {
      this.$emit("selected", this.selected);
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.overlay {
  position: absolute;
  top: 0;
  left: 0;
  bottom: 0;
  right: 0;
}
h1{
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}
</style>
