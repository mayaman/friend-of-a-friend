<template>
  <transition name="fade">
    <div
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
  },
  data() {
    return {};
  },
  computed: {
    // left: () => {
    //   // $emit("setLeft", index);
    //   return Math.ceil(Math.random() * 80);
    // },
    // top: () => {
    //   // $emit("setTop", index);
    //   return Math.ceil(Math.random() * 80);
    // },
    // size: () => {
    //   // $emit("setSize", index);
    //   return Math.ceil(Math.random() * 10) + 10;
    // },
  },
  mounted() {
    $(() => {
      $(".draggable").draggable({ containment: "parent" });
    });

    console.log(window);
    console.log(window.type);
  },
  methods: {},
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.window-container {
  background: white;
  position: absolute;
  border: 3px solid black;
}

.window-container:hover {
  border: 3px solid #ffb1b9;
}

.window-container:hover > .window-bar {
  border-bottom: 3px solid #ffb1b9;
}

.draggable:hover {
  cursor: url("~@/assets/mouse.png"), auto;
}

.window-bar {
  height: 30px;
  background: #ffb1b9;
  border-bottom: 3px solid black;
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
  text-align: left;
  font-family: "Courier New", monospace;
  font-weight: bold;
}

.window-contents .continue button {
  background: #ffb1b9;
  border: none;
  padding: 5px;
  border-radius: 5px;
  font-family: "Courier New", monospace;
  font-weight: bold;
  font-size: 24px;
}

.window-contents .continue button:hover {
  background: #6aaae4;
  cursor: url("~@/assets/pointer.png"), auto;
}
</style>
