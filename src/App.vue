<template>
  <div id="app">
    <div class="h-screen w-screen dark:bg-black">
      <div class="container mx-auto">
        <div v-show="!lose && !won" class="text-center mt-6 p-8">
          <h1 class="text-6xl leading-tight font-bold mb-2">Igor Did It Again</h1>
          <timer :start="start" :won="won" @timestamp="setResult" />
          <div class="text-xl font-light mb-4 max-w-3xl mx-auto">
            <typed :description="true" :options="{loop: false, typeSpeed: 30}" elt="description" />
          </div>
          <password @lose="loseFn" @won="wonFn" @start="startFn" />
        </div>
        <div v-if="lose" class="text-center mt-6 p-8 mx-auto max-w-3xl">
          <p class="text-6xl over">GAME OVER</p>
          <p class="text-4xl over">Dimitrov is triggered!</p>
          <img src="./assets/triggered.jpg" class="mx-auto" />
          <typed
            class="mt-20"
            :strings="[`That's an L boys. <br> Sorry. <br> GM.`]"
            :options="{loop: false}"
          />
        </div>
        <div v-if="won" class="text-center mt-6 p-8 mx-auto max-w-3xl">
          <p class="text-6xl">Congratulations!</p>
          <p class="text-3xl">Solved in {{ time }}</p>
          <p class="text-4xl text-green-700">Access Granted!</p>
          <br />
          <br />
          <br />
          <iframe
            width="560"
            height="315"
            src="https://www.youtube.com/embed/VvJm4pQZ04s"
            frameborder="0"
            allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture"
            allowfullscreen
          ></iframe>
          <typed
            class="mt-20 text-4xl"
            :strings="[`Here's your *secret* recipe, <br>Спаси́бо.`]"
            :options="{loop: false}"
          />
        </div>
      </div>
    </div>
  </div>
</template>


<script>
import Timer from "./components/Timer.vue";
import Typed from "./components/Typed.vue";
import Password from "./components/Password.vue";

export default {
  name: "App",
  components: {
    Timer,
    Password,
    Typed
  },
  data() {
    return {
      lose: false,
      won: false,
      start: false,
      result: null
    };
  },
  computed: {
    time() {
      return this.result
        ? `${Math.floor((this.result / 60) % 60)}mins ${Math.floor(
            this.result % 60
          )}s`
        : "";
    }
  },
  methods: {
    loseFn(value) {
      this.lose = value;
    },
    wonFn(value) {
      this.won = value;
    },
    startFn() {
      this.start = true;
    },
    setResult(value) {
      this.result = value - 26;
    }
  }
};
</script>
<style lang="scss">
@import "assets/styles/tailwind.postcss";
@import url("https://fonts.googleapis.com/css?family=Roboto+Mono&display=swap");
html {
  overflow: scroll;
  overflow-x: hidden;
}
::-webkit-scrollbar {
  width: 0px; /* Remove scrollbar space */
  background: transparent; /* Optional: just make scrollbar invisible */
}
/* Optional: show position indicator in red */
::-webkit-scrollbar-thumb {
  background: #ff0000;
}
body {
  background-color: #000;
  color: #fff;
  font-family: "Roboto Mono";
}

@mixin anim($name, $dur, $iterate) {
  animation-name: $name;
  animation-duration: $dur;
  animation-iteration-count: $iterate;
}

@keyframes example {
  0% {
    color: red;
    text-shadow: 0 0 20px red;
  }
  25% {
    color: red;
    text-shadow: 2px 2px 2px red;
    transform: translate(-2px, 1px);
  }
  40% {
    color: darkred;
    text-shadow: none;
    transform: translate(0, 0);
  }
  50% {
    color: red;
    text-shadow: 5px 5px 2px darkred, -5px -5px 2px red;
    transform: translate(0px, 5px);
  }
  70% {
    color: red;
    text-shadow: none;
    transform: translate(0, 0);
  }
  80% {
    color: darkred;
    text-shadow: 0 0 20px red;
    transform: translate(-2px, 1px);
  }
  100% {
    color: red;
    text-shadow: none;
  }
}

.over {
  text-align: center;
  @include anim(example, 2s, infinite);
}
</style>