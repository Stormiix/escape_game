<template>
  <div>
    <label
      class="block uppercase tracking-wide text-xs font-bold mb-2"
      for="grid-password"
      :class="textValidationClass"
    >{{ name }}</label>
    <input
      class="appearance-none block w-full bg-transparent text-white border border-white py-3 px-4 mb-3 leading-tight focus:outline-none"
      :class="validationClass"
      :type="novalidation ? 'password' : 'text'"
      :placeholder="placeholder"
      v-model="value"
    />
  </div>
</template>

<script>
export default {
  props: {
    idx: {
      type: Number,
      default: () => 0
    },
    password: {
      type: String
    },
    len: {
      type: Number,
      default: () => 4
    },
    novalidation: {
      type: Boolean,
      default: false
    }
  },
  data() {
    return {
      placeholder: "*".repeat(this.len),
      status: false,
      value: null
    };
  },
  computed: {
    name() {
      return `Puzzle ${this.idx + 1}`;
    },
    validationClass() {
      return {
        "text-white border border-white": this.novalidation || !this.value,
        "text-red-700 border border-red-700":
          !this.novalidation && this.value && !this.status,
        "text-green-700 border border-green-700":
          !this.novalidation && this.value && this.status
      };
    },
    textValidationClass() {
      return {
        "text-white": this.novalidation || !this.value,
        "text-red-700": !this.novalidation && this.value && !this.status,
        "text-green-700": !this.novalidation && this.value && this.status
      };
    }
  },
  watch: {
    value(newValue) {
      this.$emit("password", newValue.toLowerCase());
      if (!this.novalidation) {
        this.status = newValue.toLowerCase() == this.password;
        this.$emit("status", this.idx, this.status);
      }
    }
  }
};
</script>

<style>
</style>