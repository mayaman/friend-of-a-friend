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
      v-on:nextCollection="openNextCollection"
      v-on:setLeft="setLeft"
    ></Window>
    <div class="marquee">
      <img
        draggable="false"
        alt="Pixelated text that says Friend of a Friend"
        src="./assets/foaf.png"
      />
    </div>
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
      openWindows: [
        {
          type: "continue",
          left: 80,
          top: 65,
          size: 5,
        },
        {
          type: "text",
          text:
            "For our next collection, we wanted to go back in time and re-explore the World Wide Web as we first dreamt it...",
          left: 50,
          top: 50,
          size: 10,
        },
      ],
      currentWindowIndex: 0,
    };
  },
  computed: {
    windowCollections: () => {
      let tempWindowCollections = [
        [
          {
            type: "text",
            text:
              "For our next collection, we wanted to go back in time and re-explore the World Wide Web as we first dreamt it...",
          },
        ],
        [
          { type: "image", imgPath: "matisse.jpg" },
          {
            type: "text",
            text:
              "We were inspired by the painting Dance by Henri Matisse. To us, this image represents connection. Dancers reaching for one another in space.",
          },
        ],
        [
          { type: "image", imgPath: "connection_large_color.png" },
          { type: "image", imgPath: "connection_small_color.png" },
          { type: "image", imgPath: "photo_computer.png" },
          {
            type: "text",
            text: "We translated this image into our own pixelated design.",
          },
        ],
        [
          { type: "image", imgPath: "1991_large_bw.png" },
          {
            type: "text",
            text: "Both of us were born in 1991.",
          },
        ],
      ];

      tempWindowCollections.forEach((collection) => {
        collection.forEach((window) => {
          window.left = Math.ceil(Math.random() * 80);
          window.top = Math.ceil(Math.random() * 80);
          window.size = Math.ceil(Math.random() * 10) + 10;
        });
      });

      return tempWindowCollections;
    },
  },
  mounted() {
    console.log("hello world");
  },
  methods: {
    setLeft(index) {
      console.log("trying to close window: ", index);
      // Remove current window
      // this.openWindows[index].left = ;
    },
    closeWindow(index) {
      console.log("trying to close window: ", index);
      // Remove current window
      this.openWindows.splice(index, 1);
    },
    openNextCollection(index) {
      // this.openWindows.splice(index, 1);
      this.currentWindowIndex++;

      this.windowCollections[this.currentWindowIndex].forEach((window) => {
        this.openWindows.push(window);
      });

      // this.openWindows.push({
      //   type: "continue",
      // });
    },
  },
};
</script>

<style>
body {
  background: black;
  cursor: url("~@/assets/mouse.png"), auto;
  margin: 0px;
  max-width: 100vw;
  max-height: 100vh;
  overflow: hidden;
}

#connection-logo {
  height: 80vh;
  width: auto;
  margin: 10vh;
  -webkit-animation: rotation 30s infinite linear;
}

#connection-logo:hover {
  /* animation-play-state: paused; */
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: white;
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
  left: 10px;
  top: 0;
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
