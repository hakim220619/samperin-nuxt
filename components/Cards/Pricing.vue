<template>
  <v-card
    class="pricing"
    :class="{highlighted: highlighted}"
  >
    <div class="main-title">
      <h6>
        {{ title }}
      </h6>
      <img :src="img" alt="img">
      <h5 v-if="price > 0">
        Rp {{ price }}<span>/bulan</span>
      </h5>
      <h5 v-else>
        Call
      </h5>
      <p class="desc">
        {{ desc }}
      </p>
    </div>
    <ul class="feature">
      <li
        v-for="(item, index) in featureList"
        :key="index"
      >
        <span
          v-if="item.type === 'plus'"
          class="icon success-icon"
        >
          <i class="ion-ios-checkmark-outline" />
        </span>
        <span
          v-else
          class="icon error-icon"
        >
          <i class="ion-ios-close-outline" />
        </span>
        {{ item.text }}
      </li>
    </ul>
    <div class="btn-area">
      <v-btn
        :color="highlighted ? 'secondary' : 'primary'"
        block
        large
        class="button"
      >
        {{ $t('hostingLanding.getstarted') }}
      </v-btn>
    </div>
  </v-card>
</template>

<style lang="scss" scoped>
@import './cards-style.scss';
</style>

<script>
export default {
  props: {
    title: {
      type: String,
      required: true,
    },
    img: {
      type: String,
      default: '/images/hosting/home.png',
    },
    price: {
      type: Number,
      required: true,
    },
    featureList: {
      type: Array,
      required: true,
    },
    desc: {
      type: String,
      default: '',
    },
    highlighted: {
      type: Boolean,
      default: false,
    },
  },
  computed: {
    calculatePrice() {
      return this.price > 0 ? this.price : 'Call';
    },
  },
};
</script>
