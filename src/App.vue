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
      {{ instructionsText }}
    </div>
    <!-- <div
      class="collection-container"
      v-for="(collection, collectionIndex) in windowCollections"
      :key="collectionIndex"
      v-show="currentWindowIndex == collectionIndex"
    >
      <Window
        draggable="true"
        v-for="(window, index) in collection"
        :ref="'collection' + collectionIndex + 'window' + index"
        v-bind:window="window"
        v-bind:key="collectionIndex + index"
        v-bind:index="index"
        v-on:closeWindow="closeWindow"
        v-on:nextCollection="openNextCollection"
      ></Window>
    </div> -->
    <!-- <Window
      draggable="true"
      v-for="(window, index) in allWindows"
      v-show="currentWindowIndividualIndex > index"
      v-bind:window="window"
      v-bind:key="window.imgPath + index"
      v-bind:index="index"
      v-on:closeWindow="closeWindow"
      v-on:nextCollection="openNextCollection"
    ></Window> -->
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
        "NOW CLICK SOMEWHERE ELSE. THERE'S LOTS TO SEE.",
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
          size: 30,
        },
        {
          type: "image",
          imgPath: "photos/connection/photo_computer.png",
          active: false,
          bgColor: "#f5f5f5",
          left: 0,
          top: 0,
          size: 18,
        },
        {
          type: "image",
          imgPath: "KnowledgeIsPower_Animation.gif",
          active: false,
          bgColor: "#f5f5f5",
          left: 0,
          top: 0,
          size: 24,
        },
        {
          type: "image",
          imgPath: "photos/1991/PAU03371.jpg",
          active: false,
          bgColor: "#f5f5f5",
          left: 0,
          top: 0,
          size: 10,
        },
        {
          type: "image",
          imgPath: "photos/connection/PAU03254.jpg",
          active: false,
          bgColor: "#f5f5f5",
          left: 0,
          top: 0,
          size: 14,
        },
        {
          type: "image",
          imgPath: "FOF_Wifi_Animation.gif",
          active: false,
          bgColor: "#f5f5f5",
          left: 0,
          top: 0,
          size: 20,
        },
        {
          type: "image",
          imgPath: "photos/1991/PAU03531.jpg",
          active: false,
          bgColor: "#f5f5f5",
          left: 0,
          top: 0,
          size: 9,
        },
        {
          type: "image",
          imgPath: "FOF_WeAreAllSearchingForConnection.gif",
          active: false,
          bgColor: "#f5f5f5",
          left: 0,
          top: 0,
          size: 18,
        },
        {
          type: "image",
          imgPath: "photos/connection/PAU03654.jpg",
          active: false,
          bgColor: "#f5f5f5",
          left: 0,
          top: 0,
          size: 18,
        },
        {
          type: "image",
          imgPath: "photos/1991/PAU03593.jpg",
          active: false,
          bgColor: "#f5f5f5",
          left: 0,
          top: 0,
          size: 28,
        },
        {
          type: "image",
          imgPath: "photos/connection/PAU03781.jpg",
          active: false,
          bgColor: "#f5f5f5",
          left: 0,
          top: 0,
          size: 18,
        },
        {
          type: "image",
          imgPath: "photos/1991/PAU03333.jpg",
          active: false,
          bgColor: "#f5f5f5",
          left: 0,
          top: 0,
          size: 10,
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
      console.log("handling click, index: ", this.currentPopupIndex);
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
      let topPos = e.y - 100;
      if (topPos > window.innerHeight - 100) {
        topPos = topPos - 100;
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
  border: 2px solid #ffb1b9;
  border-radius: 5px;
  color: black;
  background: #ffb1b9;
  top: 10px;
  right: 10px;
  height: 10px;
  text-align: center;
  font-family: "VT323", monospace;
  font-size: 24px;
  display: inline;
  line-height: 10px;
  padding: 7px;
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
  left: 10px;
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
  /* background: #f7f746; */
  background: #f2817f;
  cursor: url("~@/assets/pointer.png"), pointer;
  z-index: 99;
}

.marquee-text:hover {
  /* animation-play-state: paused; */
  /* background: #ffb1b9; */
  /* color: #f7f746; */
  color: white;
  /* color: #4a8fcc; */
  /* background: white; */
  /* background: black; */
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
