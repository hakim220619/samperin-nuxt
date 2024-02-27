<template>
  <div class="parallax-wrap dots-wrap">
    <div v-if="loaded" class="inner-parallax large">
      <div class="cloud-wrap">
        <scroll-parallax :speed="0.3">
          <div class="figure left big">
            <div>
              <svg class="cloud">
                <use xlink:href="/images/hosting/cloud_parallax.svg#main" />
              </svg>
            </div>
          </div>
        </scroll-parallax>
        <scroll-parallax :speed="0.2">
          <div class="figure left small">
            <div>
              <svg class="cloud">
                <use xlink:href="/images/hosting/cloud_parallax.svg#main" />
              </svg>
            </div>
          </div>
        </scroll-parallax>
      </div>
      <div class="cloud-wrap">
        <scroll-parallax :speed="0.3">
          <div class="figure right big">
            <div>
              <svg class="cloud">
                <use xlink:href="/images/hosting/cloud_parallax.svg#main" />
              </svg>
            </div>
          </div>
        </scroll-parallax>
        <scroll-parallax :speed="0.2">
          <div class="figure right small">
            <div>
              <svg class="cloud">
                <use xlink:href="/images/hosting/cloud_parallax.svg#main" />
              </svg>
            </div>
          </div>
        </scroll-parallax>
      </div>
      <div class="cloud-wrap">
        <scroll-parallax :speed="0.3">
          <div class="figure left big">
            <div>
              <svg class="cloud">
                <use xlink:href="/images/hosting/cloud_parallax.svg#main" />
              </svg>
            </div>
          </div>
        </scroll-parallax>
        <scroll-parallax :speed="0.2">
          <div class="figure left small">
            <div>
              <svg class="cloud">
                <use xlink:href="/images/hosting/cloud_parallax.svg#main" />
              </svg>
            </div>
          </div>
        </scroll-parallax>
      </div>
    </div>
  </div>
</template>

<style lang="scss" scoped>
@import './parallax-style.scss';
</style>

<script>
export default {
  data() {
    return {
      loaded: false,
    };
  },
  mounted() {
    this.loaded = true;
  },
};
</script>
