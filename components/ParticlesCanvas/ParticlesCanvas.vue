<template>
  <div
    id="particles"
    class="deco"
  >
    <div class="deco-inner">
      <img :width="width" src="/images/hosting/particle.png" alt="particle">
    </div>
  </div>
</template>

<style lang="scss" scoped>
.deco {
  position: relative;
  height: 2000px;
  left: 0;
  top: 0;
  margin-bottom: -2000px;
  @include use-theme(opacity, 1, 0.1);
  @include breakpoints-down(md) {
    display: none;
  }
}
.deco-inner {
  position: absolute;
  top: 70px;
  left: 0;
  width: 100%;
  height: 100%;
}
.hide {
  visibility: hidden;
}
</style>

<script>
export default {
  data() {
    return {
      width: 1000,
      hide: true,
      loaded: false,
    };
  },
};
</script>
