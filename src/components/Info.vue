<template>
  <transition name="bounce">
    <div class="draggable window-container" v-show="active" v-bind:style="{}">
      <div class="window-bar">
        <img @click="closeWindow" class="x" src="@/assets/x.png" />
        *** INFO ***
      </div>

      <div class="window-contents text">
        This popup window shop celebrates Friend of a Friend Studio's Internet
        inspired collection
        <a href="https://www.friendofafriend.studio/shop" target="_blank"
          ><span class="italics">Searching for connection</span></a
        >.
        <br />
        <br />
        It was designed and developed by friend of Friend of a Friend,
        <a target="_blank" href="https://mayaontheinter.net/">Maya Man</a>.
      </div>
    </div>
  </transition>
</template>

<script>
export default {
  name: "Info",
  props: {
    index: Number,
    data: Object,
  },
  data() {
    return {
      active: true,
    };
  },
  computed: {
    left: () => {
      return Math.ceil(Math.random() * 80);
    },
    top: () => {
      return Math.ceil(Math.random() * 60);
    },
    size: () => {
      return Math.ceil(Math.random() * 20) + 15;
    },
  },
  mounted() {
    $(() => {
      $(".draggable").draggable({
        containment: "#app",
        stack: ".draggable",
      });
    });
  },
  methods: {
    closeWindow() {
      this.active = false;
      this.$emit("closeInfo");
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.window-container {
  font-family: "VT323", monospace;
  font-size: 24px;
  line-height: 30px;
  width: auto;
  max-width: 35%;
  left: 32.5%;
  top: 30%;
  z-index: 99999999999 !important;
}

.window-bar {
  color: black;
  font-size: 18px;
  line-height: 20px;
}

@media only screen and (max-width: 768px) {
  .window-container {
    max-width: 90%;
    left: 5%;
    top: 30%;
  }
}
</style>
