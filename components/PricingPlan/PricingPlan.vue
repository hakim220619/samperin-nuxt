<template>
  <div class="root">
    <v-container :class="{ fixed: isDesktop }">
      <main-title :caption="$t('hostingLanding.pricing_headtitle')" :text="$t('hostingLanding.pricing_title')"
        align="center" />
      <div class="pricing-wrap">
        <section>
          <div v-for="item in ListPaketAll">
            <div data-aos="fade-up" data-aos-offset="-100" data-aos-duration="200">
              <div>
                <pricing-card :price=item.price :id="item.id" highlighted img="/images/hosting/home.png"
                  :title=item.namePaket desc="Sampah organik, unorganik, residu" />
              </div>
            </div>
          </div>
          <!-- <div
            data-aos="fade-up"
            data-aos-offset="-100"
            data-aos-duration="400"
          >
            <div>
              <pricing-card
                :price="150000"
                :feature-list="feature.startup"
               
                img="/images/hosting/office.png"
                title="Niaga"
                desc="Sampah organik, unorganik, residu"
              />
            </div>
          </div>
          <div
            data-aos="fade-up"
            data-aos-offset="-100"
            data-aos-duration="500"
          >
            <div>
              <pricing-card
                :price="0"
                :feature-list="feature.company"
                img="/images/hosting/company.png"
                title="Industri"
                desc="Sampah dan limbah Industri"
              />
            </div>
          </div> -->

        </section>
      </div>
    </v-container>
  </div>
</template>

<style lang="scss" scoped>
@import './pricing-plan-style.scss';
</style>

<script>
import AOS from 'aos';
import Title from '../Title';
import PricingCard from '../Cards/Pricing';
import listFeature from './listFeature';
import axios from 'axios';
import ApiService from '@/plugins/apiService';

export default {
  components: {
    'main-title': Title,
    PricingCard,
  },
  data() {
    return {
      ListPaketAll: [],
      feature: listFeature,
    };
  },
  computed: {
    isDesktop() {
      const lgUp = this.$vuetify.display.lgAndUp;
      return lgUp;
    },
  },
  mounted() {

    let token = JSON.parse(localStorage.getItem('token'));
    return axios
      .get(ApiService.url + "/listPaket", {
        headers: {
          Accept: "application/json",
        },
      })
      .then((response) => { this.ListPaketAll = response.data.data }),

      AOS.init({
        once: true,
      });
  },
};
</script>
