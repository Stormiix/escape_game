<template>
  <div>
    <video ref="video">
      <source src="video.mp4" type="video/mp4" />
    </video>
  </div>
</template>

<script>
export default {
  props: {
    start: {
      type: Boolean,
      default: () => false
    },
    won: {
      type: Boolean,
      default: () => false
    }
  },
  computed: {
    videoElement() {
      return this.$refs.video;
    }
  },
  watch: {
    start(newValue) {
      if (newValue) {
        this.videoElement.play();
      }
    },
    won(newValue) {
      if (newValue) {
        this.$emit("timestamp", this.videoElement.currentTime);
      }
    }
  }
};
</script>

<style lang="scss">
video {
  display: block;
  width: auto;
  margin: 0 auto;
}
</style>