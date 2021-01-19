<template>
  <transition name="fade">
    <div
      class="draggable window-container"
      v-bind:style="{ left: left + '%', top: top + '%', maxWidth: size + 'vw' }"
    >
      <div class="window-bar">
        <img
          v-on:click="$emit('closeWindow', index)"
          class="x"
          src="@/assets/x.png"
        />
      </div>
      <div class="window-contents">
        <img
          draggable="false"
          :src="require('@/assets/' + window.imgPath + '')"
        />
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
    left: () => {
      return Math.ceil(Math.random() * 90);
    },
    top: () => {
      return Math.ceil(Math.random() * 80);
    },
    size: () => {
      return Math.ceil(Math.random() * 8) + 10;
    },
  },
  mounted() {
    $(() => {
      $(".draggable").draggable({ containment: "parent" });
    });
  },
  methods: {},
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.window-container {
  background: white;
  position: absolute;
  top: 50%;
  left: 50%;
}

.window-container:hover {
  /* background: hotpink; */
}

.draggable:hover {
  cursor: crosshair;
}

.window-bar {
  height: 30px;
  background: #ffb1b9;
  border: 1px solid black;
  position: relative;
}

.window-bar .x {
  height: 10px;
  position: absolute;
  left: 10px;
  top: 50%;
  transform: translate(0%, -50%);
}

.window-bar .x:hover {
  height: 15px;
  cursor: pointer;
}

.window-contents {
  padding: 15px;
  border: 1px solid black;
}

.window-contents img {
  max-width: 100%;
}
</style>
