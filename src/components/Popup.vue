<template>
  <transition name="bounce">
    <div
      @mousedown="moveToFront"
      class="draggable window-container"
      v-show="active"
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
        <br />
        Thanks for popup window shopping with us : - )
        <br />
        <br />
        Come inside @
        <a target="_blank" href="https://www.friendofafriend.studio/shop"
          >friendofafriend.studio</a
        >
        for a closer look ♥
      </div>
      <!-- <div class="window-contents continue" v-if="data.type == 'continue'">
        <button v-on:click="$emit('nextCollection', index)">
          <img
            src="https://media.giphy.com/media/MTt7Eh8WPudlStuY7L/giphy.gif"
            alt="Next button"
          />
        </button>
      </div> -->
      <!-- <div class="window-contents ytvideo" v-if="data.type == 'ytvideo'">
        <iframe
          width="560"
          height="315"
          src="https://www.youtube.com/embed/HKLxvdFtlZE"
          frameborder="0"
          allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
          allowfullscreen
        ></iframe>
      </div> -->
    </div>
  </transition>
</template>

<script>
export default {
  name: "Popup",
  props: {
    index: Number,
    data: Object,
  },
  data() {
    return {
      active: true,
      isDragging: false,
      mouseIsDown: false,
    };
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
  },
  methods: {
    moveToFront() {
      // ("trying to move to front");
      // (e.target);
      // e.target.style.zIndex = e.target.style.zIndex++;
    },
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
  display: block;
  line-height: 30px;
  padding: 15px;
}

/* YOUTUBE EMBED */
.ytvideo iframe {
  max-width: 100%;
}
</style>
