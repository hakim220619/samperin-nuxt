<template>
  <div class="page-wrap">
    <div class="cloud-deco">
      <parallax-cloud />
    </div>
    <hidden point="mdUp">
      <div class="logo logo-header">
        <a :href="routerLink.hosting.home">
          <img src="/images/hosting-logo.svg" alt="logo">
          <p class="use-text-subtitle2">
            {{ brand.hosting.projectName }}
          </p>
        </a>
      </div>
    </hidden>
    <v-container class="max-lg inner-wrap">
      <v-card class="form-box fragment-fadeUp">
        <v-btn
          :href="routerLink.hosting.home"
          icon
          variant="text"
          class="backtohome"
        >
          <i class="ion-ios-home-outline" />
          <i class="ion-ios-arrow-round-back-outline" />
        </v-btn>
        <div class="auth-frame">
          <v-row>
            <v-col md="5" cols="12" class="pa-4">
              <hidden point="smDown">
                <div class="greeting">
                  <div class="logo">
                    <img src="/images/hosting-logo.svg" alt="logo">
                    <p class="use-text-subtitle2">
                      {{ brand.hosting.projectName }}
                    </p>
                  </div>
                  <h4 class="use-text-title2 pb-2">
                    {{ title }}
                  </h4>
                  <h6 class="use-text-paragraph">
                    {{ subtitle }}
                  </h6>
                </div>
              </hidden>
            </v-col>
            <v-col md="7" cols="12">
              <div class="form-wrap">
                <div class="frm-deco">
                  <svg class="cloud">
                    <use xlink:href="/images/hosting/cloud_bottom_frm.svg#main" />
                  </svg>
                </div>
                <slot />
              </div>
            </v-col>
          </v-row>
        </div>
      </v-card>
    </v-container>
  </div>
</template>

<style lang="scss" scoped>
@import './form-style.scss';
</style>

<script>
import brand from '@/assets/text/brand';
import routerLink from '@/assets/text/link';
import Hidden from '../Hidden';
import ParallaxCloud from '../Parallax/Cloud';

export default {
  components: {
    Hidden,
    ParallaxCloud,
  },
  props: {
    title: {
      type: String,
      required: true,
    },
    subtitle: {
      type: String,
      default: '',
    },
  },
  data() {
    return {
      brand,
      routerLink,
    };
  },
};
</script>
