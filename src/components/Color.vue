<template>
  <button
    class="color"
    @click="copyColor"
  >
    <div
      :style="{ background: hex }"
      class="icon"
    >
    </div>
    <div
      class="text"
    >
      <p
        class="name"
      >
        {{ name }}
      </p>
      <p>
        {{ hex }}
      </p>
      <p>
        {{ pantone }}
      </p>
      <p>
        {{ cmyk }}
      </p>
    </div>
  </button>
</template>

<script>
export default {
  name: 'Color',
  props: {
    selected: String,
    name: String,
    hex: String,
    pantone: String,
    cmyk: String,
    dark: Boolean
  },
  methods: {
    copyColor: function () {
      if (!navigator.clipboard) {
        this.fallbackCopyTextToClipboard(this[this.selected]);
        return;
      }
      navigator.clipboard.writeText(this[this.selected]).then(() => {
        this.$emit("clicked", this.hex, this[this.selected], this.dark);
      }, function(err) {
        console.error('Async: Could not copy text: ', err);
      });
    },
    fallbackCopyTextToClipboard: function (text) {
      var textArea = document.createElement("textarea");
      textArea.value = text;
      
      // Avoid scrolling to bottom
      textArea.style.top = "0";
      textArea.style.left = "0";
      textArea.style.position = "fixed";

      document.body.appendChild(textArea);
      textArea.focus();
      textArea.select();

      try {
        var successful = document.execCommand('copy');
        if(successful) this.$emit("clicked", this.hex, this[this.selected], this.dark);
      } catch (err) {
        console.error('Fallback: Oops, unable to copy', err);
      }

      document.body.removeChild(textArea);
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
button {
  border: none;
  background: none;
  display: block;
  font: unset;
  padding: unset;
  cursor: pointer;
}
button:hover .icon{
  box-shadow: rgba(0, 0, 0, 0.2) 0 0 10px;
}
.icon {
  border-radius: 50%;
  width: 100%;
  padding-top: 100%;
}
.text {
  margin: 1rem 0;
}
p {
  text-align: left;
  margin: 0;
  font-size: 14px;
  font-weight: 400;
}
.name {
  font-weight: bold;
  font-size: 16px;
}
@media only screen and (max-width: 991px) {
  button {
    min-width: 85px;
  }
  button:hover .icon{
    box-shadow: none;
  }
}
</style>
