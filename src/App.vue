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
import Popup from "./components/Popup.vue";
import Info from "./components/Info.vue";

export default {
  name: "App",
  components: {
    Popup,
    Info,
  },
  props: {},
  data() {
    return {
      isMobile: false,
      currentWindowIndex: 0,
      currentPopupIndex: 0,
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
          size: 30,
          yOffset: 100,
        },
        {
          type: "image",
          imgPath: "photos/PAU03667.jpg",
          active: false,
          bgColor: "#f5f5f5",
          left: 0,
          top: 0,
          size: 24,
          yOffset: 200,
        },
        {
          type: "image",
          imgPath: "photos/PAU03312.jpg",
          active: false,
          bgColor: "#f5f5f5",
          left: 0,
          top: 0,
          size: 26,
          yOffset: 250,
        },
        {
          type: "image",
          imgPath: "gifs/FOF_WeAreAllSearchingForConnection.gif",
          active: false,
          bgColor: "#f5f5f5",
          left: 0,
          top: 0,
          size: 48,
          yOffset: 200,
        },
        {
          type: "image",
          imgPath: "photos/PAU03270.jpg",
          active: false,
          bgColor: "#f5f5f5",
          left: 0,
          top: 0,
          size: 37,
          yOffset: 150,
        },
        {
          type: "image",
          imgPath: "photos/PAU03675.jpg",
          active: false,
          bgColor: "#f5f5f5",
          left: 0,
          top: 0,
          size: 32,
          yOffset: 175,
        },
        {
          type: "image",
          imgPath: "photos/PAU03286.jpg",
          active: false,
          bgColor: "#f5f5f5",
          left: 0,
          top: 0,
          size: 27,
          yOffset: 275,
        },
        {
          type: "image",
          imgPath: "photos/PAU03338.jpg",
          active: false,
          bgColor: "#f5f5f5",
          left: 0,
          top: 0,
          size: 26,
          yOffset: 200,
        },
        {
          type: "image",
          imgPath: "photos/PAU03357.jpg",
          active: false,
          bgColor: "#f5f5f5",
          left: 0,
          top: 0,
          size: 18,
          yOffset: 200,
        },
        {
          type: "image",
          imgPath: "photos/PAU03368.jpg",
          active: false,
          bgColor: "#f5f5f5",
          left: 0,
          top: 0,
          size: 28,
          yOffset: 250,
        },
        {
          type: "image",
          imgPath: "gifs/KnowledgeIsPower_Animation.gif",
          active: false,
          bgColor: "#f5f5f5",
          left: 0,
          top: 0,
          size: 34,
          yOffset: 200,
        },
        {
          type: "image",
          imgPath: "photos/PAU03386.jpg",
          active: false,
          bgColor: "#f5f5f5",
          left: 0,
          top: 0,
          size: 18,
          yOffset: 200,
        },
        {
          type: "image",
          imgPath: "photos/PAU03420.jpg",
          active: false,
          bgColor: "#f5f5f5",
          left: 0,
          top: 0,
          size: 34,
          yOffset: 175,
        },
        {
          type: "image",
          imgPath: "photos/PAU03450.jpg",
          active: false,
          bgColor: "#f5f5f5",
          left: 0,
          top: 0,
          size: 27,
          yOffset: 200,
        },
        {
          type: "image",
          imgPath: "photos/PAU03467.jpg",
          active: false,
          bgColor: "#f5f5f5",
          left: 0,
          top: 0,
          size: 36,
          yOffset: 200,
        },
        {
          type: "image",
          imgPath: "photos/PAU03524.jpg",
          active: false,
          bgColor: "#f5f5f5",
          left: 0,
          top: 0,
          size: 38,
          yOffset: 200,
        },
        {
          type: "image",
          imgPath: "photos/PAU03578.jpg",
          active: false,
          bgColor: "#f5f5f5",
          left: 0,
          top: 0,
          size: 22,
          yOffset: 250,
        },
        {
          type: "image",
          imgPath: "gifs/FOF_Wifi_Animation.gif",
          active: false,
          bgColor: "#f5f5f5",
          left: 0,
          top: 0,
          size: 30,
          yOffset: 200,
        },
        {
          type: "image",
          imgPath: "photos/PAU03597.jpg",
          active: false,
          bgColor: "#f5f5f5",
          left: 0,
          top: 0,
          size: 27,
          yOffset: 275,
        },
        {
          type: "image",
          imgPath: "photos/PAU03631.jpg",
          active: false,
          bgColor: "#f5f5f5",
          left: 0,
          top: 0,
          size: 20,
          yOffset: 250,
        },
        {
          type: "image",
          imgPath: "photos/PAU03694.jpg",
          active: false,
          bgColor: "#f5f5f5",
          left: 0,
          top: 0,
          size: 29,
          yOffset: 300,
        },
        {
          type: "image",
          imgPath: "photos/PAU03781.jpg",
          active: false,
          bgColor: "#f5f5f5",
          left: 0,
          top: 0,
          size: 19,
          yOffset: 200,
        },
        {
          type: "image",
          imgPath: "gifs/RollCaps.gif",
          active: false,
          bgColor: "#f5f5f5",
          left: 0,
          top: 0,
          size: 24,
          yOffset: 250,
        },
        {
          type: "design",
          imgPath: "connection_small_color.png",
          active: false,
          bgColor: "#f5f5f5",
          left: 0,
          top: 0,
          size: 31,
          yOffset: 200,
        },
        {
          type: "finale",
          active: false,
          bgColor: "#f5f5f5",
          left: 0,
          top: 0,
          size: 40,
          yOffset: 200,
        },
      ],
    };
  },
  computed: {},
  mounted() {
    this.checkMobile();
  },
  methods: {
    checkMobile() {
      if (
        /(android|bb\d+|meego).+mobile|avantgo|bada\/|blackberry|blazer|compal|elaine|fennec|hiptop|iemobile|ip(hone|od)|ipad|iris|kindle|Android|Silk|lge |maemo|midp|mmp|netfront|opera m(ob|in)i|palm( os)?|phone|p(ixi|re)\/|plucker|pocket|psp|series(4|6)0|symbian|treo|up\.(browser|link)|vodafone|wap|windows (ce|phone)|xda|xiino/i.test(
          navigator.userAgent
        ) ||
        /1207|6310|6590|3gso|4thp|50[1-6]i|770s|802s|a wa|abac|ac(er|oo|s\-)|ai(ko|rn)|al(av|ca|co)|amoi|an(ex|ny|yw)|aptu|ar(ch|go)|as(te|us)|attw|au(di|\-m|r |s )|avan|be(ck|ll|nq)|bi(lb|rd)|bl(ac|az)|br(e|v)w|bumb|bw\-(n|u)|c55\/|capi|ccwa|cdm\-|cell|chtm|cldc|cmd\-|co(mp|nd)|craw|da(it|ll|ng)|dbte|dc\-s|devi|dica|dmob|do(c|p)o|ds(12|\-d)|el(49|ai)|em(l2|ul)|er(ic|k0)|esl8|ez([4-7]0|os|wa|ze)|fetc|fly(\-|_)|g1 u|g560|gene|gf\-5|g\-mo|go(\.w|od)|gr(ad|un)|haie|hcit|hd\-(m|p|t)|hei\-|hi(pt|ta)|hp( i|ip)|hs\-c|ht(c(\-| |_|a|g|p|s|t)|tp)|hu(aw|tc)|i\-(20|go|ma)|i230|iac( |\-|\/)|ibro|idea|ig01|ikom|im1k|inno|ipaq|iris|ja(t|v)a|jbro|jemu|jigs|kddi|keji|kgt( |\/)|klon|kpt |kwc\-|kyo(c|k)|le(no|xi)|lg( g|\/(k|l|u)|50|54|\-[a-w])|libw|lynx|m1\-w|m3ga|m50\/|ma(te|ui|xo)|mc(01|21|ca)|m\-cr|me(rc|ri)|mi(o8|oa|ts)|mmef|mo(01|02|bi|de|do|t(\-| |o|v)|zz)|mt(50|p1|v )|mwbp|mywa|n10[0-2]|n20[2-3]|n30(0|2)|n50(0|2|5)|n7(0(0|1)|10)|ne((c|m)\-|on|tf|wf|wg|wt)|nok(6|i)|nzph|o2im|op(ti|wv)|oran|owg1|p800|pan(a|d|t)|pdxg|pg(13|\-([1-8]|c))|phil|pire|pl(ay|uc)|pn\-2|po(ck|rt|se)|prox|psio|pt\-g|qa\-a|qc(07|12|21|32|60|\-[2-7]|i\-)|qtek|r380|r600|raks|rim9|ro(ve|zo)|s55\/|sa(ge|ma|mm|ms|ny|va)|sc(01|h\-|oo|p\-)|sdk\/|se(c(\-|0|1)|47|mc|nd|ri)|sgh\-|shar|sie(\-|m)|sk\-0|sl(45|id)|sm(al|ar|b3|it|t5)|so(ft|ny)|sp(01|h\-|v\-|v )|sy(01|mb)|t2(18|50)|t6(00|10|18)|ta(gt|lk)|tcl\-|tdg\-|tel(i|m)|tim\-|t\-mo|to(pl|sh)|ts(70|m\-|m3|m5)|tx\-9|up(\.b|g1|si)|utst|v400|v750|veri|vi(rg|te)|vk(40|5[0-3]|\-v)|vm40|voda|vulc|vx(52|53|60|61|70|80|81|83|85|98)|w3c(\-| )|webc|whit|wi(g |nc|nw)|wmlb|wonu|x700|yas\-|your|zeto|zte\-/i.test(
          navigator.userAgent.substr(0, 4)
        )
      ) {
        this.isMobile = true;
      }
      console.log("MOBILE??? ", this.isMobile);
    },
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
      let yOffset = this.windowData[this.currentPopupIndex].yOffset;
      if (this.isMobile) {
        yOffset = yOffset / 2;
      }
      let topPos = e.y - yOffset;
      if (topPos > window.innerHeight - 150 && !this.isMobile) {
        topPos = topPos - 400;
      } else if (this.isMobile && topPos > window.innerHeight - 100) {
        topPos = topPos - 200;
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
  animation: marquee 500s linear infinite;

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
    transform: translate(0%, 0);
  }

  100% {
    transform: translate(-100%, 0);
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
