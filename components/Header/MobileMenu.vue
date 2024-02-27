<template>
  <div class="mobile-nav">
    <div
      :class="{ 'menu-open': open }"
      class="menu"
    >
      <v-list
        dense
        tag="nav"
      >
        <v-list-item
          v-for="(item, index) in navMenu"
          :key="index"
          :href="'#' + item"
          link
          :style="{ animationDuration: index * 0.15 + 's' }"
        >
          <v-list-item-title class="menu-list">
            {{ $t('hostingLanding.header_'+item) }}
          </v-list-item-title>
        </v-list-item>
        <v-list-item
          :href="link.hosting.berita"
          :style="{ animationDuration: navMenu.length * 0.15 + 's' }"
          link
        >
          <v-list-item-title class="menu-list">
            {{ $t('hostingLanding.header_berita') }}
          </v-list-item-title>
        </v-list-item>
        <v-list-item
          :href="link.hosting.contact"
          :style="{ animationDuration: navMenu.length * 0.15 + 's' }"
          link
        >
          <v-list-item-title class="menu-list">
            {{ $t('hostingLanding.header_contact') }}
          </v-list-item-title>
        </v-list-item>
        <v-divider class="divider-sidebar" />
        <v-list-item
          v-for="item in ['login', 'register']"
          :key="item"
          :href="link.hosting[item]"
          :style="{ animationDuration: navMenu.length * 0.15 + 's' }"
          link
        >
          <v-list-item-title class="menu-list">
            {{ $t('hostingLanding.header_'+item) }}
          </v-list-item-title>
        </v-list-item>
      </v-list>
    </div>
  </div>
</template>

<style scoped lang="scss">
@import './header-style';
</style>

<script>
import navMenu from './menu';
import link from '@/assets/text/link';

export default {
  props: {
    open: {
      type: Boolean,
      default: false,
    },
  },
  data() {
    return {
      link,
      navMenu,
    };
  },
};
</script>
