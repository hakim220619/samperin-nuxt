<template>
  <div class="main-feature">
    <v-container fixed>
      <main-title
        :caption="$t('hostingLanding.mainfeature_headtitle')"
        :text="$t('hostingLanding.mainfeature_title')"
        align="center"
      />
      <v-row class="spacing6 grid">
        <v-col
          v-for="(item, index) in featureList"
          :key="index"
          md="4"
          cols="12"
          class="pa-6"
        >
          <div class="item">
            <figure>
              <img :src="item.img" :alt="item.title">
            </figure>
            <h6 class="use-text-subtitle2">
              {{ $t('hostingLanding.mainfeature_' + item.title) }}
            </h6>
            <p class="use-text-paragraph">
              {{ $t('hostingLanding.mainfeature_' + item.desc) }}
            </p>
          </div>
        </v-col>
      </v-row>
    </v-container>
  </div>
</template>

<style lang="scss" scoped>
@import './feature-style.scss';
</style>

<script>
import Title from '../Title';

export default {
  components: {
    'main-title': Title,
  },
  data() {
    return {
      featureList: [
        {
          img: '/images/hosting/feature1.png',
          title: 'titleitem1',
          desc: 'descitem1',
        },
        {
          img: '/images/hosting/feature2.png',
          title: 'titleitem2',
          desc: 'descitem2',
        },
        {
          img: '/images/hosting/feature3.png',
          title: 'titleitem3',
          desc: 'descitem3',
        },
      ],
    };
  },
};
</script>
