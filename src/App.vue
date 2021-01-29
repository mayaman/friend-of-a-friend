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
      v-show="currentPopupIndex > index"
      v-bind:data="window"
      v-bind:key="index"
      v-bind:index="index"
      v-on:closeWindow="closeWindow"
      v-on:nextCollection="openNextCollection"
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
        <span class="marquee-text"
          >SHOP THE COLLECTION !!! SHOP THE COLLECTION !!! SHOP THE COLLECTION
          !!! SHOP THE COLLECTION !!! SHOP THE COLLECTION !!! SHOP THE
          COLLECTION !!! SHOP THE COLLECTION !!! SHOP THE COLLECTION !!! SHOP
          THE COLLECTION !!! SHOP THE COLLECTION !!! SHOP THE COLLECTION !!!
          SHOP THE COLLECTION !!! SHOP THE COLLECTION !!! SHOP THE COLLECTION
          !!! SHOP THE COLLECTION !!! SHOP THE COLLECTION !!! SHOP THE
          COLLECTION !!! SHOP THE COLLECTION !!! SHOP THE COLLECTION !!! SHOP
          THE COLLECTION !!! SHOP THE COLLECTION !!! SHOP THE COLLECTION !!!
          SHOP THE COLLECTION !!! SHOP THE COLLECTION !!! SHOP THE COLLECTION
          !!! SHOP THE COLLECTION !!! SHOP THE COLLECTION !!! SHOP THE
          COLLECTION !!! SHOP THE COLLECTION !!! SHOP THE COLLECTION !!! SHOP
          THE COLLECTION !!! SHOP THE COLLECTION !!! SHOP THE COLLECTION !!!
          SHOP THE COLLECTION !!! SHOP THE COLLECTION !!! SHOP THE COLLECTION
          !!! SHOP THE COLLECTION !!! SHOP THE COLLECTION !!! SHOP THE
          COLLECTION !!! SHOP THE COLLECTION !!! SHOP THE COLLECTION !!! SHOP
          THE COLLECTION !!! SHOP THE COLLECTION !!! SHOP THE COLLECTION !!!
          SHOP THE COLLECTION !!! SHOP THE COLLECTION !!! SHOP THE COLLECTION
          !!! SHOP THE COLLECTION !!! SHOP THE COLLECTION !!! SHOP THE
          COLLECTION !!! SHOP THE COLLECTION !!! SHOP THE COLLECTION !!! SHOP
          THE COLLECTION !!! SHOP THE COLLECTION !!! SHOP THE COLLECTION !!!
          SHOP THE COLLECTION !!! SHOP THE COLLECTION !!! SHOP THE COLLECTION
          !!! SHOP THE COLLECTION !!! SHOP THE COLLECTION !!! SHOP THE
          COLLECTION !!! SHOP THE COLLECTION !!! SHOP THE COLLECTION !!! SHOP
          THE COLLECTION !!! SHOP THE COLLECTION
        </span></a
      >
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
      showContinue: true,
      showInfo: false,
      windowData: [
        {
          type: "design",
          imgPath: "foaf.png",
          active: false,
          bgColor: "#f5f5f5",
          left: 0,
          top: 0,
          size: 25,
        },
        {
          type: "text",
          text:
            "For our next collection, we wanted to go back in time and re-explore the World Wide Web as we first dreamt it...",
          active: false,
          bgColor: "#f5f5f5",
          left: 0,
          top: 0,
          size: 40,
        },
        {
          type: "design",
          imgPath: "connection_large_color.png",
          active: false,
          bgColor: "#f5f5f5",
          left: 0,
          top: 0,
          size: 15,
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
          type: "design",
          imgPath: "foaf_circle_large.png",
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
          type: "design",
          imgPath: "connection_small_color.png",
          active: false,
          bgColor: "#f5f5f5",
          left: 0,
          top: 0,
          size: 24,
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
          type: "text",
          text:
            "We were both born in 1991 and grew up during the height of the Web 1.0 days...",
          active: false,
          bgColor: "#f5f5f5",
          left: 0,
          top: 0,
          size: 39,
        },
        {
          type: "design",
          imgPath: "1991_large_bw.png",
          active: false,
          bgColor: "#f5f5f5",
          left: 0,
          top: 0,
          size: 13,
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
          type: "text",
          text: "That's all for now!",
          active: false,
          bgColor: "#f5f5f5",
          left: 0,
          top: 0,
          size: 39,
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
  mounted() {
    // this.activateCollectionWindows();
  },
  methods: {
    handleClick(e) {
      this.showContinue = false;
      this.windowData[this.currentPopupIndex];
      let leftPos =
        e.x -
        (window.innerWidth * this.windowData[this.currentPopupIndex].size) /
          100 /
          2;
      if (leftPos < 0) {
        leftPos = 0;
      }
      "LEFT POS: ", leftPos;
      this.windowData[this.currentPopupIndex].left = leftPos;

      let topPos = e.y - 50;
      if (topPos > window.innerHeight - 100) {
        topPos = topPos - 100;
      }
      this.windowData[this.currentPopupIndex].top = topPos;

      this.currentPopupIndex++;
      "clicked on body, current index: ", this.currentPopupIndex;
      e;

      // let popupClass = Vue.extend(Popup);
      // let newWindow = new popupClass({
      //   propsData: {
      //     data: this.windowData[this.currentPopupIndex],
      //     index: this.currentPopupIndex,
      //   },
      // }).$mount("#app");
    },
    toggleInfo() {
      this.showInfo = !this.showInfo;
    },
    closeWindow(index) {
      ("trying to close window");
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
body {
  background: black;
  cursor: url("~@/assets/mouse.png"), auto;
  margin: 0px;
  max-width: 100vw;
  max-height: 100vh;
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
  position: inherit;
  height: 100%;
}

#connection-logo {
  -moz-user-select: none;
  -webkit-user-select: none;
  user-select: none;
  height: 80vh;
  width: auto;
  margin: 10vh;
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
  position: fixed;
  left: 10px;
  bottom: 0;
  z-index: 999;
  cursor: url("~@/assets/pointer_xs.png"), pointer;
  background: #f5f5f5;
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
  background: #f5f5f5;
  cursor: url("~@/assets/pointer.png"), pointer;
  z-index: 99;
}

.marquee-text:hover {
  animation-play-state: paused;
  background: #ffb1b9;
}

.marquee a {
  color: black;
  z-index: 9999;
}

.marquee a:hover {
}

@-webkit-keyframes marquee {
  0% {
    transform: translate(-5%, 0);
  }

  100% {
    transform: translate(-70%, 0);
  }
}
</style>
