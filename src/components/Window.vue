<template>
  <transition name="" mode="out-in">
    <div
      @mousedown="moveToFront"
      class="draggable window-container"
      v-bind:style="{
        left: window.left + '%',
        top: window.top + '%',
        maxWidth: window.size + 'vw',
      }"
    >
      <div v-if="window.type != 'continue'" class="window-bar">
        <img
          v-on:click="$emit('closeWindow', index)"
          class="x"
          src="@/assets/x.png"
        />
      </div>
      <div class="window-contents">
        <div v-if="window.type == 'image'">
          <img
            draggable="false"
            :src="require('@/assets/' + window.imgPath + '')"
          />
        </div>
        <div v-if="window.type == 'text'" class="text">
          {{ window.text }}
        </div>
        <div v-if="window.type == 'continue'" class="continue">
          <button v-on:click="$emit('nextCollection', index)">
            <img
              src="https://media.giphy.com/media/MTt7Eh8WPudlStuY7L/giphy.gif"
              alt="Next button"
            />
          </button>
        </div>
        <div v-if="window.type == 'ytvideo'" class="ytvideo">
          <iframe
            width="560"
            height="315"
            src="https://www.youtube.com/embed/HKLxvdFtlZE"
            frameborder="0"
            allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
            allowfullscreen
          ></iframe>
        </div>
      </div>
    </div>
  </transition>
</template>

<script>
export default {
  name: "Window",
  props: {
    imgPath: String,
    index: Number,
    window: Object,
    openDelay: Number,
  },
  data() {
    return {
      active: false,
    };
  },
  computed: {},
  mounted() {
    $(() => {
      $(".draggable").draggable({ containment: "#app" });
    });
  },
  methods: {
    moveToFront() {
      // ("trying to move to front");
      // (e.target);
      // e.target.style.zIndex = e.target.style.zIndex++;
    },
    activate() {},
    closeWindow() {
      this.active = false;
    },
    getOpenDelay() {
      return this.openDelay;
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.window-container {
  background: #f5f5f5;
  position: absolute;
  border: 2px solid black;
}

.window-container:hover {
  border: 2px solid #ffb1b9;
}

.window-container:hover > .window-bar {
  border-bottom: 2px solid #ffb1b9;
}

.draggable:hover {
  cursor: url("~@/assets/mouse.png"), auto;
}

.window-bar {
  height: 25px;
  background: #ffb1b9;
  border-bottom: 2px solid black;
  position: relative;
}

.window-bar .x {
  height: 10px;
  position: absolute;
  left: 15px;
  top: 50%;
  padding: 5px;
  transform: translate(-50%, -50%);
}

.window-bar .x:hover {
  height: 15px;
  cursor: url("~@/assets/pointer.png"), auto;
}

.window-contents {
  padding: 15px;
}

.window-contents img {
  max-width: 100%;
}

.window-contents .text {
  color: black;
  text-align: center;
  font-family: "VT323", monospace;
  font-size: 36px;
  display: inline;
  line-height: 40px;
  /* background: lightgreen; */
}

/* YOUTUBE EMBED */
.ytvideo iframe {
  max-width: 100%;
}
</style>
