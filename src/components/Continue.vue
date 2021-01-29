<template>
  <transition name="fade">
    <div v-show="active" class="draggable continue-container">
      <div class="continue-options" v-if="firstEncounter">
        WELCOME TO FRIEND OF A FRIEND'S POPUP LOOKBOOK... CLICK ANYWHERE TO
        START
        <br />
        <br />
        <div class="button-container">
          <!-- <button v-on:click="updatedCollection()">
            NO THANKS!
          </button> -->
          <button v-on:click="updatedCollection()">
            <!-- <img
              src="https://media.giphy.com/media/MTt7Eh8WPudlStuY7L/giphy.gif"
              alt="Next button"
            /> -->
            OKAY!
          </button>
        </div>
      </div>
      <!-- <div id="quick-continue" class="continue-options" v-else>
        <button v-on:click="updatedCollection()">
          <img
            src="https://media.giphy.com/media/MTt7Eh8WPudlStuY7L/giphy.gif"
            alt="Next button"
          />
        </button>
      </div> -->
    </div>
  </transition>
</template>

<script>
export default {
  name: "Continue",
  props: {},
  data() {
    return {
      active: false,
      firstEncounter: true,
    };
  },
  computed: {},
  mounted() {
    $(() => {
      $(".draggable").draggable({ containment: "parent" });
    });

    setTimeout(() => {
      this.active = true;
    }, 500);
  },
  methods: {
    updatedCollection() {
      // this.active = false;
      // setTimeout(() => {
      //   this.active = true;
      // }, 7000);
      // if (this.firstEncounter) {
      //   this.firstEncounter = false;
      // }
      // this.$emit("nextCollection");
      this.active = false;
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.continue-container {
  background: #ffb1b9;
  position: absolute;
  border: 2px solid black;

  top: 40%;
  left: 35%;
  width: 30%;
  z-index: 99;
}

.draggable:hover {
  cursor: url("~@/assets/mouse.png"), auto;
}

.continue-options {
  color: black;
  text-align: center;
  font-family: "VT323", monospace;
  font-size: 24px;
  padding: 15px;
}

.continue-options img {
  max-width: 100%;
}

.button-container {
  display: inline-block;
}

.continue-options button {
  /* background: none;
  border: none; */
  padding: 5px;
  border-radius: 5px;
  font-family: "VT323", monospace;
  font-size: 24px;
  outline-color: #ffb1b9;
  margin: 5px;
  cursor: url("~@/assets/pointer.png"), auto;
}

.continue-options button:hover {
  background: #f1817e;
}

#quick-continue {
  width: 50px;
}
</style>
