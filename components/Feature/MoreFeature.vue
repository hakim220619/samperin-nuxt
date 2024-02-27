<template>
  <div class="more-feature">
    <div class="chart-deco" />
    <v-container :class="{ fixed: isDesktop }">
      <div class="item">
        <div>
          <v-row
            :class="[isMobile ? 'column-reverse' : 'row']"
            class="spacing6"
          >
            <v-col md="6" cols="12" class="pa-6">
              <figure class="illustration">
                <img src="/images/hosting/illustration1.png" alt="feature">
              </figure>
            </v-col>
            <v-col md="6" cols="12" class="pa-6">
              <div class="text">
                <div
                  data-aos="fade-left"
                  data-aos-offset="-200"
                  data-aos-delay="400"
                  data-aos-duration="300"
                >
                  <div>
                    <main-title
                      :caption="$t('hostingLanding.morefeature_headtitle1')"
                      :text="$t('hostingLanding.morefeature_title1')"
                      :align="isMobile ? 'center' : 'left'"
                    />
                    <div :class="{ 'text-center': isMobile }">
                      <p class="use-text-subtitle2" :class="isMobile ? 'text-center' : 'text-left'">
                        {{ $t('hostingLanding.morefeature_desc1') }}
                      </p>
                      <v-btn color="primary">
                        {{ $t('hostingLanding.learnmore') }}
                      </v-btn>
                    </div>
                  </div>
                </div>
              </div>
            </v-col>
          </v-row>
        </div>
      </div>
      <v-divider class="divider" />
      <div class="item">
        <div>
          <v-row class="spacing6">
            <v-col md="6" cols="12">
              <div class="text text-right">
                <div
                  data-aos="fade-left"
                  data-aos-offset="-200"
                  data-aos-delay="400"
                  data-aos-duration="300"
                >
                  <div>
                    <main-title
                      :caption="$t('hostingLanding.morefeature_headtitle2')"
                      :text="$t('hostingLanding.morefeature_title2')"
                      :align="isMobile ? 'center' : 'right'"
                    />
                    <div :class="{ 'text-center': isMobile }">
                      <p
                        :class="isMobile ? 'text-center' : 'text-right'"
                        class="use-text-subtitle2"
                      >
                        {{ $t('hostingLanding.morefeature_desc2') }}
                      </p>
                      <v-btn color="primary">
                        {{ $t('hostingLanding.learnmore') }}
                      </v-btn>
                    </div>
                  </div>
                </div>
              </div>
            </v-col>
            <v-col md="6" cols="12">
              <figure class="illustration">
                <img src="/images/hosting/illustration2.png" alt="feature">
              </figure>
            </v-col>
          </v-row>
        </div>
      </div>
      <v-divider class="divider" />
     
    </v-container>
  </div>
</template>

<style lang="scss" scoped>
@import './feature-style.scss';
</style>

<script>
import AOS from 'aos';
import Title from '../Title';

export default {
  components: {
    'main-title': Title,
  },
  computed: {
    isDesktop() {
      const lgUp = this.$vuetify.display.lgAndUp;
      return lgUp;
    },
    isMobile() {
      const smDown = this.$vuetify.display.smAndDown;
      return smDown;
    },
  },
  mounted() {
    AOS.init({
      once: true,
    });
  },
};
</script>
