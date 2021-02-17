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
        maxWidth: size + '%',
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
    isMobile: Boolean,
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
      size: 0,
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
  computed: {},
  mounted() {
    if (this.isMobile) {
      this.size = this.data.size * 2;
    } else {
      this.size = this.data.size;
    }

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

    // $(() => {
    //   $(".draggable").draggable({
    //     containment: "#app",
    //     stack: ".draggable",
    //   });
    // });
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
  },
};
</script>

<style scoped>
.window-contents img {
  max-width: 100%;
  height: auto;
  display: inline-flex;
}

.image {
  display: contents;
}

@media only screen and (max-width: 768px) {
  .window-container {
    max-width: 100%;
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
