<template>
  <div class="mt-20">
    <form class="w-full max-w-3xl mx-auto">
      <div class="flex flex-wrap -mx-3 mb-2">
        <div class="w-full md:w-1/5 px-3 mb-6 md:mb-0">
          <part
            :idx="0"
            :len="passwords[0].length"
            :password="passwords[0]"
            @status="setPartStatus"
          />
        </div>
        <div class="w-full md:w-1/5 px-3 mb-6 md:mb-0">
          <part
            :idx="1"
            :len="passwords[1].length"
            :password="passwords[1]"
            @status="setPartStatus"
          />
        </div>
        <div class="w-full md:w-1/5 px-3 mb-6 md:mb-0">
          <part
            :idx="2"
            :len="passwords[2].length"
            :password="passwords[2]"
            @status="setPartStatus"
          />
        </div>
        <div class="w-full md:w-1/5 px-3 mb-6 md:mb-0">
          <part
            :idx="3"
            :len="passwords[3].length"
            :password="passwords[3]"
            @status="setPartStatus"
          />
        </div>
        <div class="w-full md:w-1/5 px-3 mb-6 md:mb-0">
          <part
            :idx="4"
            :len="passwords[4].length"
            :password="passwords[4]"
            @status="setPartStatus"
            :novalidation="true"
            @password="setLastPassword"
          />
        </div>
      </div>

      <div class="flex flex-wrap -mx-3 mb-2">
        <div class="focus:outline-none w-full md:w-1/4 px-3 mb-6 md:mb-0">
          <button
            class="bg-black border border-white border-2 hover:bg-white hover:text-black text-white py-4 w-full items-center"
            @click.prevent="start()"
          >Start</button>
        </div>
        <div class="w-full md:w-2/4 px-3 mb-6 md:mb-0">
          <button
            class="focus:outline-none bg-black border border-2 py-4 w-full items-center"
            :disabled="disabled"
            :class="disabledClass"
            @click.prevent="submit()"
          >
            <span>Reveal secret recipe!</span>
          </button>
        </div>
        <div class="w-full md:w-1/4 px-3 mb-6 md:mb-0">
          <button
            class="focus:outline-none bg-black border border-red-700 border-2 hover:bg-gray-400 hover:bg-red-700 hover:text-black text-red-700 py-4 w-full items-center"
            @click.prevent="giveup()"
          >Give up!</button>
        </div>
      </div>
    </form>
  </div>
</template>

<script>
import Part from "./Part.vue";
export default {
  components: {
    Part
  },
  data() {
    return {
      passwords: ["d5xe6", "nazdrovia", "klavoc", "limofeconi", "babushka"],
      parts: [false, false, false, false, true],
      last: null
    };
  },
  computed: {
    disabledClass() {
      return {
        "border-white text-white hover:bg-white hover:text-black": !this
          .disabled,
        "border-grey-500 text-grey-500 cursor-not-allowed": this.disabled
      };
    },
    disabled() {
      return !this.parts.every(s => s);
    }
  },
  methods: {
    setPartStatus(idx, value) {
      this.$set(this.parts, idx, value);
    },
    giveup() {
      this.$emit("lose", true);
    },
    start() {
      this.$emit("start");
    },
    setLastPassword(value) {
      this.last = value;
    },
    submit() {
      if (this.last == this.passwords[4]) {
        this.$emit("won", true);
      } else {
        this.$emit("lose", true);
      }
    }
  }
};
</script>

<style>
</style>