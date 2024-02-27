<template>
  <div class="root">
    <div class="bg" />
    <v-container class="max-md">
      <transition-group
        :name="transition"
        tag="div"
        class="slider-wrap"
      >
        <div
          v-for="number in [currentImg]"
          :key="number"
          class="slide slider-content"
        >
          <div class="inner item">
            <v-row>
              <v-col sm="4" cols="12" class="promo-image">
                <section>
                  <figure class="image">
                    <img
                      :src="content[Math.abs(currentImg) % content.length].image"
                      :alt="content[Math.abs(currentImg) % content.length].title"
                    >
                  </figure>
                </section>
              </v-col>
              <v-col sm="8" cols="12">
                <div class="text">
                  <h1>
                    <v-btn variant="text">
                      {{ content[Math.abs(currentImg) % content.length].title }}
                    </v-btn>
                  </h1>
                  <p class="use-text-subtitle2">
                    {{ content[Math.abs(currentImg) % content.length].desc }}
                  </p>
                  <section class="time">
                    <h6 class="use-text-caption">
                      <span>
                        {{ $t('hostingLanding.promo_periode') }}
                        :&nbsp;
                        {{ content[Math.abs(currentImg) % content.length].date }}
                      </span>
                    </h6>
                  </section>
                </div>
              </v-col>
            </v-row>
          </div>
        </div>
      </transition-group>
      <a
        href="javascript:void(0)"
        class="prev"
        @click="prev"
      >
        <v-icon>mdi-chevron-left</v-icon>
      </a>
      <a
        href="javascript:void(0)"
        class="next"
        @click="next"
      >
        <v-icon>mdi-chevron-right</v-icon>
      </a>
    </v-container>
    <div class="cloud-top">
      <svg>
        <use xlink:href="/images/hosting/cloud_top.svg#main" />
      </svg>
    </div>
    <div class="cloud-top-cover">
      <svg>
        <use xlink:href="/images/hosting/cloud_top.svg#main" />
      </svg>
    </div>
  </div>
</template>

<style lang="scss" scoped>
@import './promotion-style.scss';
</style>

<script>
import img from '@/assets/images/imgAPI';

const sliderData = [
  {
    image: img.hosting[0],
    title: 'Wordpress Hosting start from $2/mo',
    desc:
      'Sed imperdiet enim ligula vitae viverra. Vivamus sit amet interdum elit.',
    date: '12 Jul - 10 Aug',
  },
  {
    image: img.hosting[1],
    title: 'Dedicated VPS start from $5/mo',
    desc:
      'Sed imperdiet enim ligula vitae viverra. Vivamus sit amet interdum elit.',
    date: '12 Jul - 10 Aug',
  },
  {
    image: img.hosting[2],
    title: '.COM + Hosting Only $15/mo',
    desc:
      'Sed imperdiet enim ligula vitae viverra. Vivamus sit amet interdum elit.',
    date: '12 Jul - 10 Aug',
  },
];

export default {
  data() {
    return {
      content: sliderData,
      transition: '',
      autoplay: null,
      currentImg: 0,
    };
  },
  mounted() {
    this.playSlider();
  },
  beforeUnmount() {
    clearInterval(this.autoplay);
  },
  methods: {
    playSlider() {
      this.autoplay = setInterval(() => {
        this.currentImg += 1;
        this.transition = 'slide-right';
      }, 50000);
    },
    manualPlay() {
      clearInterval(this.autoplay);
      setTimeout(() => {
        this.playSlider();
      }, 1);
    },
    next() {
      this.manualPlay();
      this.currentImg += 1;
      this.transition = 'slide-right';
    },
    prev() {
      this.manualPlay();
      this.currentImg -= 1;
      this.transition = 'slide-left';
    },
    swipeLeft() {
      this.next();
    },
    swipeRight() {
      this.prev();
    },
  },
};
</script>
