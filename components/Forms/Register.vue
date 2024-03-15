<template>
  <AuthFrame :title="$t('common.register_title')" :subtitle="$t('common.register_subtitle')">
    <div>
      <div class="head">
        <title-secondary :align="isMobile ? 'center' : 'left'">
          {{ $t('common.register') }}
        </title-secondary>
        <v-btn :href="routerLink.hosting.login" class="button-link" variant="text" size="small">
          <v-icon class="icon signArrow">
            mdi-arrow-right
          </v-icon>
          {{ $t('common.register_already') }}
        </v-btn>
      </div>
      <!-- <social-auth /> -->
      <!-- <div class="separator">
        <p>
          {{ $t('common.register_or') }}
        </p>
      </div> -->
      <v-form ref="form" v-model="valid">
        <v-row class="spacing3">
          <v-col cols="6" sm="6" class="px-3">
            <v-text-field v-model="name" :label="$t('common.register_name')" :rules="requiredRules" color="secondary"
              class="input" name="name" filled required />
          </v-col>
          <v-col cols="6" sm="6" class="px-3">
            <v-text-field v-model="email" :label="$t('common.register_email')" :rules="emailRules" color="secondary"
              class="input" name="email" filled required />
          </v-col>
          <v-col cols="6" sm="6" class="px-3">
            <v-select :items="provinsiData" item-text="nama" item-value="id" v-model="provinsi"
              label="nama" return-object outlined></v-select>
          </v-col>
          <v-col cols="6" md="6" class="px-3">
            <v-text-field v-model="password" :label="$t('common.register_password')" :rules="requiredRules"
              color="secondary" type="password" class="input" name="email" filled required />
          </v-col>
          <v-col cols="6" md="6" class="px-3">
            <v-text-field v-model="confirmPassword" :label="$t('common.register_confirm')" :rules="passwordRules"
              color="secondary" type="password" class="input" name="confirm" filled required />
          </v-col>
        </v-row>
        <div class="btn-area">
          <div class="form-helper">
            <div class="form-control-label">
              <v-checkbox v-model="checkbox" :label="$t('common.form_terms')" :rules="requiredRules"
                :hide-details="hideDetail" color="secondary" required />
              <span>
                <a href="#" class="link">
                  {{ $t('common.form_privacy') }}
                </a>
              </span>
            </div>
          </div>
          <v-btn size="large" color="secondary" @click="handleSubmit">
            {{ $t('common.continue') }}
          </v-btn>
        </div>
      </v-form>
    </div>
  </AuthFrame>
</template>

<style lang="scss" scoped>
@import './form-style';
</style>

<script>
import routerLink from '@/assets/text/link';
import TitleSecondary from '../Title/TitleSecondary';
import SocialAuth from './SocialAuth';
import AuthFrame from './AuthFrame';
import axios from 'axios';

export default {
  components: {

    SocialAuth,
    TitleSecondary,
    AuthFrame,
  },

  data() {

    return {
      routerLink,
      valid: true,
      email: '',
      name: '',
      provinsi: '',
      nama: '',
      hideDetail: true,
      emailRules: [
        v => !!v || 'E-mail is required',
        v => /.+@.+\..+/.test(v) || 'E-mail must be valid',
      ],
      password: '',
      confirmPassword: '',
      requiredRules: [v => !!v || 'This field is required'],
      passwordRules: [
        v => !!v || 'This field is required',
        v => v === this.password || 'Passwords do not match',
      ],
      checkbox: false,
      provinsiData: [],
      rule: {
        values: [
          {
            "value_display": "Broken clouds",
            "value": "803"
          },
          {
            "value_display": "Clear sky",
            "value": "800"
          }
        ]
      },
    };
  },
  computed: {
    isMobile() {
      const smDown = this.$vuetify.display.smAndDown;
      return smDown;
    },
  },
  mounted: function () {

    axios.get("http://127.0.0.1:8000/api/getProvince").then((response) => this.provinsiData = response.data.data);
  },
  methods: {
    async handleSubmit() {
      const { valid } = await this.$refs.form.validate();

      if (valid) {
        console.log('data submited');
        this.hideDetail = true;
      } else {
        this.hideDetail = false;
      }
    },
    // async saveRegister() {
    //   submitted.value = true;
    //   let data = new FormData();
    //   data.append('user_id', user_id.value.id);
    //   // console.log(data);

    //   axios
    //     .post('http://localhost:3000/api/province', data, {
    //       headers: {
    //         Accept: 'application/json',
    //         'Content-Type': 'multipart/form-data',
    //         Authorization: 'Bearer ' + token
    //       }
    //     })
    //     .then((response) => {
    //       console.log(response);
    //     })
    //     .catch((err) => console.log(err));
    // }
  },
};
</script>
