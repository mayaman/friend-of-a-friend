<template>
  <div id="app">
    <img
      draggable="false"
      id="connection-logo"
      alt="We are all searching for connection written in a circle"
      src="./assets/connection_large_color.png"
    />

    <Window
      draggable="true"
      v-for="(window, index) in openWindows"
      v-bind:window="window"
      v-bind:key="window.imgPath"
      v-bind:index="index"
      v-on:closeWindow="closeWindow"
    ></Window>
    <div class="marquee">
      <img
        draggable="false"
        alt="Pixelated text that says Friend of a Friend"
        src="./assets/foaf.png"
      />
      <img
        draggable="false"
        alt="Pixelated text that says Friend of a Friend"
        src="./assets/foaf.png"
      />
    </div>
    <!-- <p class="marquee">
      <span
        ><img
          draggable="false"
          alt="Pixelated text that says Friend of a Friend"
          src="./assets/foaf.png"
      /></span>
    </p> -->
  </div>
</template>

<script>
import Window from "./components/Window.vue";

export default {
  name: "App",
  components: {
    Window,
  },
  data() {
    return {
      allWindows: [
        { imgPath: "1991_large_bw.png" },
        { imgPath: "connection_large_color.png" },
        { imgPath: "connection_small_color.png" },
        { imgPath: "wavywifi.png" },
        { imgPath: "photo_computer.png" },
        { imgPath: "soundwave.png" },
        { imgPath: "foaf_circle_large.png" },
        { imgPath: "photo_selfie.png" },
      ],
      openWindows: [{ imgPath: "1991_large_bw.png" }],
      currentWindowIndex: 0,
    };
  },
  mounted() {
    console.log("hello world");
  },
  methods: {
    closeWindow(index) {
      console.log("trying to close window: ", index);
      this.openWindows.splice(index, 1);
      this.currentWindowIndex =
        (this.currentWindowIndex + 1) % this.allWindows.length;
      this.openWindows.push(this.allWindows[this.currentWindowIndex]);
      this.currentWindowIndex =
        (this.currentWindowIndex + 1) % this.allWindows.length;
      this.openWindows.push(this.allWindows[this.currentWindowIndex]);
    },
  },
};
</script>

<style>
body {
  background: black;
  margin: 0px;
  max-width: 100vw;
  max-height: 100vh;
  overflow: hidden;
  cursor: url("~@/assets/mouse.png");
}

#connection-logo {
  height: 80vh;
  width: auto;
  margin: 10vh;
  -webkit-animation: rotation 30s infinite linear;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: white;
  background: black;
  overflow: hidden;
}

@-webkit-keyframes rotation {
  from {
    -webkit-transform: rotate(359deg);
  }
  to {
    -webkit-transform: rotate(0deg);
  }
}

/* TRANSITION */

.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s;
}
.fade-enter, .fade-leave-to /* .fade-leave-active below version 2.1.8 */ {
  opacity: 0;
}

/* MARQUEE SHIT */

.marquee {
  width: 100%;
  display: inline-flex;
  position: absolute;
  left: 0;
  bottom: 0;
  height: 5vh;
}

.marquee img {
  display: inline;
  height: 100%;
  width: auto;
  /* will-change: transform;
  animation: marquee 15s linear infinite; */
}

@-webkit-keyframes marquee {
  0% {
    transform: translate(-30%, 0);
  }

  100% {
    transform: translate(-70%, 0);
  }
}
</style>
