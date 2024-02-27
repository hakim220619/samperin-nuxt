<template>
  <div class="root">
    <div class="parallax-img">
      <hidden point="smDown">
        <v-parallax
          :src="img.hosting[3]"
          :height="670"
          alt="parallax-bg"
        />
      </hidden>
    </div>
    <v-container class="fixed-width">
      <div class="wrapper">
        <v-row>
          <v-col md="5" cols="12" justify="center" class="pa-0">
            <div class="desc">
              <main-title
                :caption="$t('hostingLanding.benefit_headtitle')"
                :text="$t('hostingLanding.benefit_title')"
                align="left"
                dark
              />
              <ul class="list">
                <li>Vestibulum faucibus</li>
                <li>Vivamus sit amet interdum elit</li>
                <li>Donec dignissim</li>
                <li>Quisque lacinia purus</li>
                <li>Fusce placerat enim et odio molestie</li>
                <li>Pellentesque ac bibendum tortor</li>
                <li>Lorem ipsum dolor sit amet</li>
                <li>And more…</li>
              </ul>
              <v-btn size="large" color="secondary">
                {{ $t('hostingLanding.getstarted') }}
              </v-btn>
            </div>
          </v-col>
          <v-col md="7" cols="12" class="pa-0 d-flex">
            <hidden point="smDown">
              <figure class="img">
                <img :src="img.hosting[4]" alt="benefit">
              </figure>
            </hidden>
          </v-col>
        </v-row>
      </div>
    </v-container>
  </div>
</template>

<style lang="scss" scoped>
@import './benefit-style.scss';
</style>

<script>
import Title from '../Title';
import Hidden from '../Hidden';
import imgAPI from '@/assets/images/imgAPI';

export default {
  components: {
    Hidden,
    'main-title': Title,
  },
  data() {
    return {
      img: imgAPI,
    };
  },
};
</script>
