<template>
  <transition name="bounce">
    <div
      class="draggable window-container"
      v-show="active"
      v-bind:id="index"
      v-bind:style="{
        background: data.bgColor,
        left: data.left + 'px',
        top: data.top + 'px',
        maxWidth: data.size + '%',
        maxHeight: 'auto',
      }"
    >
      <div v-if="data.type != 'continue'" class="window-bar">
        <img @click.self="closeWindow" class="x" src="@/assets/x.png" />
      </div>
      <div class="window-contents design" v-if="data.type == 'design'">
        <img
          @click.self="handlePopupClick"
          draggable="false"
          :src="require('@/assets/' + data.imgPath + '')"
        />
      </div>
      <div class="window-contents image" v-if="data.type == 'image'">
        <img
          @click.self="handlePopupClick"
          draggable="false"
          :src="require('@/assets/' + data.imgPath + '')"
        />
      </div>
      <div
        @click.self="handlePopupClick"
        class="window-contents text"
        v-if="data.type == 'text'"
      >
        {{ data.text }}
      </div>
      <div
        @click.self="handlePopupClick"
        class="window-contents text"
        v-if="data.type == 'finale'"
      >
        Thanks for popup window shopping with us!
        <br />
        <br />
        Come visit
        <a target="_blank" href="https://www.friendofafriend.studio/shop"
          >friendofafriend.studio</a
        >
        for a closer look ♥
      </div>
    </div>
  </transition>
</template>

<script>
export default {
  name: "Popup",
  props: {
    index: Number,
    data: Object,
    numClicks: Number,
  },
  data() {
    return {
      active: true,
      showing: false,
      isDragging: false,
      mouseIsDown: false,
      topZIndex: 0,
    };
  },
  watch: {
    numClicks: function(num) {
      if (!this.showing) {
        $("#" + this.index).css("z-index", this.topZIndex);
      }
      this.showing = num > this.index;
    },
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
      $(".draggable")
        .draggable({
          containment: "#app",
          stack: ".draggable",
        })
        .on("dragstop", (event) => {
          this.topZIndex = event.target.style.zIndex;
        })
        .mousedown(() => {
          this.isDragging = false;
          this.mouseIsDown = true;
        })
        .mousemove(() => {
          if (this.mouseIsDown) {
            this.isDragging = true;
          }
        })
        .mouseup(() => {
          this.mouseIsDown = false;
          if (this.isDragging) {
            setTimeout(() => {
              this.isDragging = false;
            }, 1);
          }
        });
    });

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
    },
    handlePopupClick(e) {
      if (!this.isDragging) {
        this.$emit("handleClick", e);
      }
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
  /* background: #f5f5f5; */
  position: absolute;
  border: 2px solid black;
  display: inline-grid;
}

.window-container:hover {
  border: 2px solid #ffb1b9;
}

.window-container:hover > .window-bar {
  border-bottom: 2px solid #ffb1b9;
}

.draggable {
}

.draggable:hover {
  cursor: url("~@/assets/mouse.png"), auto;
}

.window-bar {
  height: 20px;
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
  /* padding: 15px; */
  display: inline-flex;
}

.window-contents img {
  max-width: 100%;
  height: auto;
  display: inline-flex;
}

.image {
  display: contents;
}

.text,
.design {
  color: black;
  text-align: center;
  font-family: "VT323", monospace;
  font-size: 24px;
  line-height: 30px;
  display: block;
  padding: 15px;
}

@media only screen and (max-width: 768px) {
  .window-container {
    max-width: 75% !important;
    width: auto;
  }

  .text,
  .design {
    font-size: 18px;
    line-height: 24px;
    padding: 15px;
  }
}
</style>
