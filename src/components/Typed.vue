<template>
  <div class="typedcontent text-justify">
    <div id="typed-strings" v-if="description">
      <p>
        A very important guest is visiting Mr. Dimitrov today and you were tasked with cooking his favorite cake.
        <br />The recipe for this cake, however, was stolen by Igor,
        <i>**sighs**</i>, and locked on this machine.
        <br />Solve the
        <span class="font-bold">6</span> puzzles in this room to get the
        <span class="font-bold">5</span> parts password and recover the secret recipe.
        <br />Or ..
        <br />
        <i>You can start preparing your funeral</i> 💀. RIP.
        <br />
        <br />You have
        <i>45min</i> to find the recipe and start cooking, before the guest is here.
        <br />
        <br />Good luck.
        <br />GM.
        <br />P.S: The first
        <span class="font-bold">4</span> inputs will turn green when the keys are correct.
        The last one is malfunctioning for some reason (we both know the reason, Igor broke it), so make sure you got the right key before submitting.
      </p>
    </div>
    <p :id="elt" style="display: inline;"></p>
  </div>
</template>

<script>
import Typed from "typed.js";

export default {
  name: "Typed",
  props: {
    description: {
      type: Boolean,
      default: () => false
    },
    elt: {
      type: String,
      default: () => "elt"
    },
    strings: {
      type: Array,
      default: () => ["<i>First</i> sentence.", "&amp; a second sentence."]
    },
    options: {
      type: Object,
      default: () => {
        return {
          loop: true
        };
      }
    }
  },

  data() {
    return {
      typed: null
    };
  },

  mounted() {
    let options = {
      ...this.options,
      typeSpeed: 40
    };
    if (this.description) {
      options.stringsElement = "#typed-strings";
    } else {
      options.strings = this.strings;
    }
    this.typed = new Typed(`#${this.elt}`, options);
  }
};
</script>

<style lang="scss">
.typedcontent {
  min-height: 5rem;
}
</style>