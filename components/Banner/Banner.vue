<template>
  <div class="root">
    <div class="deco-wrap">
      <div class="deco-inner" :class="{ hide: hide }">
        <div id="vantaRef" class="illustration" />
      </div>
    </div>

    <v-container class="max-md">
      <div class="banner-wrap">
        <div class="text">
          <h4 class="use-text-title2">
            {{ $t('hostingLanding.banner_title') }}
          </h4>
          <p class="use-text-subtitle2">
            {{ $t('hostingLanding.banner_subtitle') }}
          </p>
        </div>
      </div>
    </v-container>
  </div>
</template>

<style lang="scss" scoped>
@import './banner-style.scss';
</style>

<script>
import * as THREE from 'three';
import theme from '@/config/theme';
import Hidden from '../Hidden';

export default {
  components: {
    Hidden,
  },
  data() {
    return {
      theme,
      hide: false,
      name: '',
      domain: 'com',
      items: ['.com', '.net', '.org', '.co', '.biz', '.gov', '.id', '.abc', '.xyz', '.news', '.cc', '.me'], // eslint-disable-line
      val: '.com',
    };
  },
  computed: {
    isDesktop() {
      const mdUp = this.$vuetify.display.mdAndUp;
      return mdUp;
    },
  },
  async mounted() {
    if (process.client) {
      window.THREE = THREE;
      const { default: NET } = await import('vanta/dist/vanta.net.min');

      NET({
        el: '#vantaRef',
        THREE,
        color: theme.primary,
        backgroundColor: theme.primarylight,
        backgroundAlpha: 0,
        points: 4,
        maxDistance: 18,
        spacing: 12,
      });
    }
  },
};
</script>
