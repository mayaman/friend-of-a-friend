<template>
  <div @click.self="handleClick" id="app">
    <img
      @click.self="handleClick"
      draggable="false"
      id="connection-logo"
      alt="We are all searching for connection written in a circle"
      src="./assets/connection_large_color.png"
    />
    <div class="info" @click="toggleInfo">
      ?
    </div>
    <div class="instructions" @click="handleClick">
      <img class="foaf-logo" src="@/assets/foaf.png" />
      <br />
      {{ instructionsText }}
    </div>
    <Popup
      draggable="true"
      v-for="(window, index) in windowData"
      :ref="index"
      v-show="numClicks > index"
      v-bind:data="window"
      v-bind:key="index"
      v-bind:index="index"
      v-on:closeWindow="closeWindow"
      v-on:nextCollection="openNextCollection"
      v-on:handleClick="handleClick"
    ></Popup>
    <Info v-show="showInfo" draggable="true" v-on:closeInfo="toggleInfo"></Info>
    <Continue
      v-show="showContinue"
      draggable="true"
      v-on:closeWindow="closeWindow"
      v-on:nextCollection="openNextCollection"
    ></Continue>
    <div class="marquee">
      <a href="https://www.friendofafriend.studio/shop" target="_blank">
        <span class="marquee-text" id="on"
          >CLICK HERE TO SHOP THE COLLECTION ➩ CLICK HERE TO SHOP THE COLLECTION
          ➩ CLICK HERE TO SHOP THE COLLECTION ➩ CLICK HERE TO SHOP THE
          COLLECTION ➩ CLICK HERE TO SHOP THE COLLECTION ➩ CLICK HERE TO SHOP
          THE COLLECTION ➩ CLICK TO SHOP THE COLLECTION ➩ CLICK HERE TO SHOP THE
          COLLECTION ➩ CLICK HERE TO SHOP THE COLLECTION ➩ CLICK HERE TO SHOP
          THE COLLECTION ➩ CLICK TO SHOP THE COLLECTION ➩ CLICK HERE TO SHOP THE
          COLLECTION ➩ CLICK HERE TO SHOP THE COLLECTION ➩ CLICK HERE TO SHOP
          THE COLLECTION ➩ CLICK TO SHOP THE COLLECTION ➩ CLICK HERE TO SHOP THE
          COLLECTION ➩ CLICK HERE TO SHOP THE COLLECTION ➩ CLICK HERE TO SHOP
          THE COLLECTION ➩ CLICK TO SHOP THE COLLECTION ➩ CLICK HERE TO SHOP THE
          COLLECTION ➩ CLICK HERE TO SHOP THE COLLECTION ➩ CLICK HERE TO SHOP
          THE COLLECTION ➩ CLICK TO SHOP THE COLLECTION ➩ CLICK HERE TO SHOP THE
          COLLECTION ➩ CLICK HERE TO SHOP THE COLLECTION ➩ CLICK HERE TO SHOP
          THE COLLECTION ➩ CLICK TO SHOP THE COLLECTION ➩ CLICK HERE TO SHOP THE
          COLLECTION ➩ CLICK HERE TO SHOP THE COLLECTION ➩ CLICK HERE TO SHOP
          THE COLLECTION ➩ CLICK TO SHOP THE COLLECTION ➩ CLICK HERE TO SHOP THE
          COLLECTION ➩ CLICK HERE TO SHOP THE COLLECTION ➩ CLICK HERE TO SHOP
          THE COLLECTION ➩ CLICK TO SHOP THE COLLECTION ➩ CLICK HERE TO SHOP THE
          COLLECTION ➩ CLICK HERE TO SHOP THE COLLECTION ➩ CLICK HERE TO SHOP
          THE COLLECTION ➩ CLICK TO SHOP THE COLLECTION ➩ CLICK HERE TO SHOP THE
          COLLECTION ➩ CLICK HERE TO SHOP THE COLLECTION ➩ CLICK HERE TO SHOP
          THE COLLECTION ➩ CLICK TO SHOP THE COLLECTION ➩ CLICK HERE TO SHOP THE
          COLLECTION ➩ CLICK HERE TO SHOP THE COLLECTION ➩ CLICK HERE TO SHOP
          THE COLLECTION ➩ CLICK TO SHOP THE COLLECTION ➩ CLICK HERE TO SHOP THE
          COLLECTION ➩ CLICK HERE TO SHOP THE COLLECTION ➩ CLICK HERE TO SHOP
          THE COLLECTION ➩ CLICK TO SHOP THE COLLECTION ➩ CLICK HERE TO SHOP THE
          COLLECTION ➩ CLICK HERE TO SHOP THE COLLECTION ➩ CLICK HERE TO SHOP
          THE COLLECTION ➩ CLICK TO SHOP THE COLLECTION ➩ CLICK HERE TO SHOP THE
          COLLECTION ➩
        </span>
        <span class="marquee-text" id="off"
          >➩ LET'S GO ➩ LET'S GO ➩ LET'S GO ➩ LET'S GO ➩ LET'S GO ➩ LET'S GO ➩
          LET'S GO ➩ LET'S GO ➩ LET'S GO ➩ LET'S GO ➩ LET'S GO ➩ LET'S GO ➩
          LET'S GO ➩ LET'S GO ➩ LET'S GO ➩ LET'S GO ➩ LET'S GO ➩ LET'S GO ➩
          LET'S GO ➩ LET'S GO ➩ LET'S GO ➩ LET'S GO ➩ LET'S GO ➩ LET'S GO ➩
          LET'S GO ➩ LET'S GO ➩ LET'S GO ➩ LET'S GO ➩ LET'S GO ➩ LET'S GO ➩
          LET'S GO ➩ LET'S GO ➩ LET'S GO ➩ LET'S GO ➩ LET'S GO ➩ LET'S GO ➩
          LET'S GO ➩ LET'S GO ➩ LET'S GO ➩ LET'S GO ➩ LET'S GO ➩ LET'S GO ➩
          LET'S GO ➩ LET'S GO ➩ LET'S GO ➩ LET'S GO ➩ LET'S GO ➩ LET'S GO ➩
          LET'S GO ➩ LET'S GO ➩ LET'S GO ➩ LET'S GO ➩ LET'S GO ➩ LET'S GO ➩
          LET'S GO ➩ LET'S GO ➩ LET'S GO ➩ LET'S GO ➩ LET'S GO ➩ LET'S GO ➩
          LET'S GO ➩ LET'S GO ➩ LET'S GO ➩ LET'S GO ➩ LET'S GO ➩ LET'S GO ➩
          LET'S GO ➩ LET'S GO ➩ LET'S GO ➩ LET'S GO ➩ LET'S GO ➩ LET'S GO ➩
          LET'S GO ➩ LET'S GO ➩ LET'S GO ➩ LET'S GO ➩ LET'S GO ➩ LET'S GO ➩
          LET'S GO ➩ LET'S GO ➩ LET'S GO ➩ LET'S GO ➩ LET'S GO ➩ LET'S GO ➩
          LET'S GO ➩ LET'S GO ➩ LET'S GO ➩ LET'S GO ➩ LET'S GO ➩ LET'S GO ➩
          LET'S GO ➩ LET'S GO ➩ LET'S GO ➩ LET'S GO ➩ LET'S GO ➩ LET'S GO ➩
          LET'S GO ➩ LET'S GO ➩ LET'S GO ➩ LET'S GO ➩ LET'S GO ➩ LET'S GO ➩
          LET'S GO ➩ LET'S GO ➩ LET'S GO ➩ LET'S GO ➩ LET'S GO ➩ LET'S GO ➩
          LET'S GO ➩ LET'S GO ➩ LET'S GO ➩ LET'S GO ➩ LET'S GO ➩ LET'S GO ➩
          LET'S GO ➩ LET'S GO ➩ LET'S GO ➩ LET'S GO ➩ LET'S GO ➩ LET'S GO ➩
          LET'S GO ➩ LET'S GO ➩ LET'S GO ➩ LET'S GO ➩ LET'S GO ➩ LET'S GO ➩
          LET'S GO ➩ LET'S GO ➩ LET'S GO ➩ LET'S GO ➩ LET'S GO ➩ LET'S GO ➩
          LET'S GO ➩ LET'S GO ➩ LET'S GO ➩ LET'S GO ➩ LET'S GO ➩ LET'S GO ➩
          LET'S GO ➩ LET'S GO ➩ LET'S GO ➩ LET'S GO ➩ LET'S GO ➩ LET'S GO ➩
          LET'S GO ➩ LET'S GO ➩ LET'S GO ➩ LET'S GO ➩ LET'S GO ➩ LET'S GO ➩
          LET'S GO ➩ LET'S GO ➩ LET'S GO ➩ LET'S GO ➩ LET'S GO ➩ LET'S GO ➩
          LET'S GO ➩ LET'S GO ➩ LET'S GO ➩ LET'S GO ➩ LET'S GO ➩ LET'S GO ➩
          LET'S GO ➩ LET'S GO ➩ LET'S GO ➩ LET'S GO ➩ LET'S GO ➩ LET'S GO ➩
          LET'S GO ➩ LET'S GO ➩ LET'S GO ➩ LET'S GO ➩ LET'S GO ➩ LET'S GO ➩
          LET'S GO ➩ LET'S GO ➩ LET'S GO ➩ LET'S GO ➩ LET'S GO ➩ LET'S GO ➩
          LET'S GO ➩ LET'S GO ➩ LET'S GO ➩ LET'S GO ➩ LET'S GO ➩ LET'S GO ➩
        </span>
      </a>
    </div>
  </div>
</template>

<script>
import Continue from "./components/Continue.vue";
import Popup from "./components/Popup.vue";
import Info from "./components/Info.vue";

export default {
  name: "App",
  components: {
    Continue,
    Popup,
    Info,
  },
  props: {},
  data() {
    return {
      currentWindowIndex: 0,
      currentPopupIndex: 0,
      showContinue: false,
      showInfo: false,
      instructionsText: "CLICK ANYWHERE TO EXPLORE...",
      instructionsTextOptions: [
        "CLICK ANYWHERE TO EXPLORE...",
        "NOW CLICK SOMEWHERE ELSE...",
        "COOL, I THINK YOU'VE GOT IT!",
        "ENJOY <3",
      ],
      numClicks: 0,
      windowData: [
        {
          type: "text",
          text:
            "For our next collection, we wanted to go back in time and re-explore the World Wide Web as we first dreamt it...",
          active: false,
          bgColor: "#f5f5f5",
          left: 0,
          top: 0,
          size: 20,
        },
        {
          type: "image",
          imgPath: "photos/PAU03667.jpg",
          active: false,
          bgColor: "#f5f5f5",
          left: 0,
          top: 0,
          size: 24,
        },
        {
          type: "image",
          imgPath: "photos/PAU03312.jpg",
          active: false,
          bgColor: "#f5f5f5",
          left: 0,
          top: 0,
          size: 26,
        },
        {
          type: "image",
          imgPath: "gifs/FOF_WeAreAllSearchingForConnection.gif",
          active: false,
          bgColor: "#f5f5f5",
          left: 0,
          top: 0,
          size: 48,
        },
        {
          type: "image",
          imgPath: "photos/PAU03270.jpg",
          active: false,
          bgColor: "#f5f5f5",
          left: 0,
          top: 0,
          size: 37,
        },
        {
          type: "image",
          imgPath: "photos/PAU03675.jpg",
          active: false,
          bgColor: "#f5f5f5",
          left: 0,
          top: 0,
          size: 32,
        },
        {
          type: "image",
          imgPath: "photos/PAU03286.jpg",
          active: false,
          bgColor: "#f5f5f5",
          left: 0,
          top: 0,
          size: 27,
        },
        {
          type: "image",
          imgPath: "photos/PAU03338.jpg",
          active: false,
          bgColor: "#f5f5f5",
          left: 0,
          top: 0,
          size: 18,
        },
        {
          type: "image",
          imgPath: "photos/PAU03357.jpg",
          active: false,
          bgColor: "#f5f5f5",
          left: 0,
          top: 0,
          size: 18,
        },
        {
          type: "image",
          imgPath: "photos/PAU03368.jpg",
          active: false,
          bgColor: "#f5f5f5",
          left: 0,
          top: 0,
          size: 18,
        },
        {
          type: "image",
          imgPath: "gifs/KnowledgeIsPower_Animation.gif",
          active: false,
          bgColor: "#f5f5f5",
          left: 0,
          top: 0,
          size: 24,
        },
        {
          type: "image",
          imgPath: "photos/PAU03386.jpg",
          active: false,
          bgColor: "#f5f5f5",
          left: 0,
          top: 0,
          size: 18,
        },
        {
          type: "image",
          imgPath: "photos/PAU03420.jpg",
          active: false,
          bgColor: "#f5f5f5",
          left: 0,
          top: 0,
          size: 18,
        },
        {
          type: "image",
          imgPath: "photos/PAU03450.jpg",
          active: false,
          bgColor: "#f5f5f5",
          left: 0,
          top: 0,
          size: 18,
        },
        {
          type: "image",
          imgPath: "photos/PAU03467.jpg",
          active: false,
          bgColor: "#f5f5f5",
          left: 0,
          top: 0,
          size: 18,
        },
        {
          type: "image",
          imgPath: "photos/PAU03524.jpg",
          active: false,
          bgColor: "#f5f5f5",
          left: 0,
          top: 0,
          size: 18,
        },
        {
          type: "image",
          imgPath: "photos/PAU03578.jpg",
          active: false,
          bgColor: "#f5f5f5",
          left: 0,
          top: 0,
          size: 18,
        },
        {
          type: "image",
          imgPath: "gifs/FOF_Wifi_Animation.gif",
          active: false,
          bgColor: "#f5f5f5",
          left: 0,
          top: 0,
          size: 24,
        },
        {
          type: "image",
          imgPath: "photos/PAU03597.jpg",
          active: false,
          bgColor: "#f5f5f5",
          left: 0,
          top: 0,
          size: 18,
        },
        {
          type: "image",
          imgPath: "photos/PAU03631.jpg",
          active: false,
          bgColor: "#f5f5f5",
          left: 0,
          top: 0,
          size: 18,
        },
        {
          type: "image",
          imgPath: "photos/PAU03694.jpg",
          active: false,
          bgColor: "#f5f5f5",
          left: 0,
          top: 0,
          size: 18,
        },
        {
          type: "image",
          imgPath: "photos/PAU03781.jpg",
          active: false,
          bgColor: "#f5f5f5",
          left: 0,
          top: 0,
          size: 18,
        },
        {
          type: "image",
          imgPath: "gifs/RollCaps.gif",
          active: false,
          bgColor: "#f5f5f5",
          left: 0,
          top: 0,
          size: 24,
        },
        {
          type: "design",
          imgPath: "connection_small_color.png",
          active: false,
          bgColor: "#f5f5f5",
          left: 0,
          top: 0,
          size: 24,
        },
        {
          type: "finale",
          active: false,
          bgColor: "#f5f5f5",
          left: 0,
          top: 0,
          size: 26,
        },
      ],
    };
  },
  computed: {
    allWindows: () => {
      let tempAllWindows = [
        {
          collectionNum: 0,
          type: "image",
          imgPath: "foaf.png",
          left: 2,
          top: 5,
          size: 40,
          active: false,
          openDelay: 1,
        },
        {
          collectionNum: 0,
          type: "text",
          text:
            "For our next collection, we wanted to go back in time and re-explore the World Wide Web as we first dreamt it...",
          left: 50,
          top: 50,
          size: 40,
          active: false,
          openDelay: 2,
        },
        {
          collectionNum: 0,
          type: "text",
          text: "This is kind of like a popup lookbook ;-)",
          left: 25,
          top: 25,
          size: 30,
          active: false,
          openDelay: 3,
        },
        {
          collectionNum: 1,
          type: "image",
          imgPath: "matisse.jpg",
          active: false,
          openDelay: 3,
        },
        { collectionNum: 1, type: "ytvideo", active: false, openDelay: 1 },
        {
          collectionNum: 1,
          type: "text",
          text:
            "We were inspired by the painting Dance by Henri Matisse. To us, this image represents connection. Dancers reaching for one another in space.",
          active: false,
          openDelay: 1,
        },

        {
          collectionNum: 2,
          type: "image",
          imgPath: "connection_large_color.png",
          active: false,
          openDelay: 1,
        },
        {
          collectionNum: 2,
          type: "image",
          imgPath: "connection_small_color.png",
          active: false,
          openDelay: 1,
        },
        {
          collectionNum: 2,
          type: "image",
          imgPath: "photo_computer.png",
          active: false,
          openDelay: 1,
        },
        {
          collectionNum: 2,
          type: "text",
          text: "We translated this image into our own pixelated design.",
          active: false,
          openDelay: 1,
        },
        {
          collectionNum: 3,
          type: "image",
          imgPath: "1991_large_bw.png",
          active: false,
          openDelay: 1,
        },
        {
          collectionNum: 3,
          type: "text",
          text: "Both of us were born in 1991.",
          active: false,
          openDelay: 1,
        },
      ];

      tempAllWindows.forEach((window) => {
        window.left = Math.ceil(Math.random() * 80);
        window.top = Math.ceil(Math.random() * 60);
        window.size = Math.ceil(Math.random() * 20) + 15;
      });
      return tempAllWindows;
    },
  },
  mounted() {},
  methods: {
    handleClick(e) {
      this.numClicks++;
      this.showContinue = false;
      if (this.numClicks < this.instructionsTextOptions.length) {
        this.instructionsText = this.instructionsTextOptions[this.numClicks];
      } else {
        this.instructionsText = "";
      }

      // Select x position
      let leftPos =
        e.x -
        (window.innerWidth * this.windowData[this.currentPopupIndex].size) /
          100 /
          2;
      if (leftPos < 0) {
        leftPos = 0;
      }
      this.windowData[this.currentPopupIndex].left = leftPos;

      // Select y position
      let topPos = e.y - 150;
      if (topPos > window.innerHeight - 150) {
        topPos = topPos - 400;
      }
      this.windowData[this.currentPopupIndex].top = topPos;

      this.currentPopupIndex = this.currentPopupIndex + 1;
    },
    toggleInfo() {
      this.showInfo = !this.showInfo;
    },
    closeWindow(index) {
      let idString = "collection" + this.currentWindowIndex + "window" + index;
      this.$refs[idString][0].closeWindow();
    },
    openNextCollection() {
      this.currentWindowIndex++;
      this.activateCollectionWindows();
    },
    activateCollectionWindows() {
      for (
        let w = 0;
        w < this.windowCollections[this.currentWindowIndex].length;
        w++
      ) {
        let idString = "collection" + this.currentWindowIndex + "window" + w;
        this.$refs[idString][0].activate();
      }
    },
  },
};
</script>

<style>
.italics {
  font-style: italic;
}

body {
  background: black;
  cursor: url("~@/assets/mouse.png"), auto;
  margin: 0px;
  max-width: 100vw;
  max-height: 100vh;
  min-height: 100vh;
  overflow: hidden;
  position: relative;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #f5f5f5;
  overflow: hidden;
  position: relative;
  height: 100%;
  min-height: calc(100vh - 32px);
  max-height: calc(100vh - 32px);
}

#connection-logo {
  -moz-user-select: none;
  -webkit-user-select: none;
  user-select: none;
  height: 60vh;
  width: auto;
  margin: 20vh auto;
  -webkit-animation: rotation 30s infinite linear;
}

@-webkit-keyframes rotation {
  from {
    -webkit-transform: rotate(359deg);
  }
  to {
    -webkit-transform: rotate(0deg);
  }
}

.collection-container {
  min-height: 100%;
  position: absolute;
  top: 0;
  width: 100vw;
  left: 0;
  padding: 0px;
  margin: 0px;
}

.info {
  position: fixed;
  border: 2px solid #f2817f;
  border-radius: 3px;
  color: black;
  background: #f2817f;
  top: 10px;
  right: 10px;
  height: 10px;
  text-align: center;
  font-family: "VT323", monospace;
  font-size: 24px;
  display: inline;
  line-height: 10px;
  padding: 5px;
  z-index: 9999999;
}

.info:hover {
  cursor: url("~@/assets/pointer.png"), pointer;
}

.instructions {
  color: white;
  font-family: "VT323", monospace;
  font-size: 24px;
  position: fixed;
  top: 10px;
  left: 10px;
  width: 500px;
  text-align: left;
}

.foaf-logo {
  max-width: 100%;
}

/* TRANSITION */

.bounce-enter-active {
  animation: bounce-in 0.3s;
}
.bounce-leave-active {
  animation: bounce-in 0.3s reverse;
}
@keyframes bounce-in {
  0% {
    transform: scale(0);
  }
  100% {
    transform: scale(1);
  }
}

/* MARQUEE SHIT */

.marquee {
  width: 100%;
  display: inline-flex;
  position: fixed;
  left: 0px;
  bottom: 0;
  z-index: 999;
  cursor: url("~@/assets/pointer_xs.png"), pointer;
}

.marquee-text {
  display: inline;
  height: 100%;
  padding: 0px 0 2px 0;
  width: max-content;
  will-change: transform;
  animation: marquee 240s linear infinite;

  font-family: "VT323", monospace;
  font-size: 24px;
  display: inline-block;
  line-height: 30px;
  background: #f2817f;
  cursor: url("~@/assets/pointer.png"), pointer;
  z-index: 99;
}

@media only screen and (max-width: 768px) {
  #connection-logo {
    height: 40vh;
    margin: 30vh auto;
  }

  .info {
    font-size: 18px;
  }

  .instructions {
    font-size: 18px;
  }

  .foaf-logo {
    max-width: 50%;
  }

  .marquee-text {
    font-size: 18px;
  }
}

.marquee-text:hover {
  animation-play-state: paused;
  background: #40edb9;
}

.marquee a {
  color: black;
  z-index: 9999;
  text-decoration: none;
}

.marquee a:hover span#on {
  display: inline;
}

.marquee a:hover span#on {
  display: none;
}

.marquee a span#off {
  display: none;
}

.marquee a:hover span#off {
  display: block;
}

@-webkit-keyframes marquee {
  0% {
    transform: translate(-5%, 0);
  }

  100% {
    transform: translate(-70%, 0);
  }
}

.text a {
  color: #f2817f;
  text-decoration: none;
}

.text a:hover {
  cursor: url("~@/assets/pointer.png"), pointer;
  color: #4a8fcc;
}
</style>
