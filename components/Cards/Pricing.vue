<template>
  <v-card class="pricing" :class="{ highlighted: highlighted }">
    <div class="main-title">
      <h6>
        {{ title }}
      </h6>
      <img :src="img" alt="img">
      <h5 v-if="price > 0">
        {{ formatCurrency(Number(price)) }}<span>/bulan</span>
      </h5>
      <h5 v-else>
        Call
      </h5>
      <p class="desc">
        {{ desc }}
      </p>
    </div>
    <ul class="feature">
      <li v-for="(item, index) in ListPaketAll" :key="index">
        <span v-if="item.type === 'plus'" class="icon success-icon">
          <i class="ion-ios-checkmark-outline" />
        </span>
        <span v-else class="icon error-icon">
          <i class="ion-ios-close-outline" />
        </span>
        {{ item.description }}
      </li>
    </ul>
    <div class="btn-area">
      <v-btn :color="highlighted ? 'secondary' : 'primary'" block large class="button">
        {{ $t('hostingLanding.getstarted') }}
      </v-btn>
    </div>
  </v-card>
</template>

<style lang="scss" scoped>
@import './cards-style.scss';
</style>

<script>
import axios from 'axios';
import ApiService from '@/plugins/apiService';
export default {
  props: {
    id: {
      type: String,
      required: true,
    },
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
    desc: {
      type: String,
      default: '',
    },
    highlighted: {
      type: Boolean,
      default: false,
    },
  },
  data() {
    const formatCurrency = (value) => {
            return value.toLocaleString('en-US', { style: 'currency', currency: 'IDR' }).replace('IDR', 'Rp. ').replace('.00', '');
        };
    return {
      formatCurrency,
      ListPaketAll: [],
    };
  },
  mounted() {
    return axios
      .get(ApiService.url + "/listPaketDetail/" + this.id, {
        headers: {
          Accept: "application/json",
        },
        
      })
      .then((response) => { this.ListPaketAll = response.data.data })
  },
  computed: {
    calculatePrice() {
      return this.price > 0 ? this.price : 'Call';
    },
  },
};
</script>
