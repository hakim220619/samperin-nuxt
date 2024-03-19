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
            <v-select v-model="provinsi" :items="langList" :value="provinsi" class="input"
              color="primary"   prepend-inner-icon="mdi-web" />
          </v-col>
          <v-col cols="6" sm="6" class="px-3">
            <v-select v-model="regencyid" :items="getRegency" :value="regency" class="input"
              color="primary"  prepend-inner-icon="mdi-web" />
          </v-col>
          <v-col cols="6" sm="6" class="px-3">
            <v-select v-model="district" :items="getDistrict" :value="district" class="input"
              color="primary"  prepend-inner-icon="mdi-web" />
          </v-col>
          <v-col cols="6" sm="6" class="px-3">
            <v-select v-model="villages" :items="getVillages" :value="villages" class="input"
              color="primary"  prepend-inner-icon="mdi-web" />
          </v-col>
          <v-col cols="12" sm="12" class="px-3">
            <v-text-field v-model="name" label="address" :rules="requiredRules" color="secondary"
              class="input" name="name" filled required />
          </v-col>
          <v-col cols="12" md="12" class="px-3">
            <v-text-field v-model="password" :label="$t('common.register_password')" :rules="requiredRules"
              color="secondary" type="password" class="input" name="email" filled required />
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
    const provinsi = '';
    const regencyid = '';
    const district = '';
    const villages = '';
    return {
      routerLink,
      valid: true,
      email: '',
      name: '',
      provinsi,
      regencyid,
      district,
      villages,
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
      regencyData: [],
      districtData: [],
      villagesData: [],

    };
  },

  computed: {
    isMobile() {
      const smDown = this.$vuetify.display.smAndDown;
      return smDown;
    },
    langList() {
      axios.get("http://127.0.0.1:8000/api/getProvince").then((response) =>  this.provinsiData = response.data.data )
      // console.log(this.provinsiData);
      const list = [];
      const i18n = this.provinsiData;

      i18n.map((locale) => {
        list.push({ title: locale.nama, value: locale.id });
        return false;
      });
      return list;
    },
    getRegency() {
      axios.get("http://127.0.0.1:8000/api/getRegency/"+ this.provinsi).then((response) => { this.regencyData = response.data.data })
      // console.log(this.regencyData);
      const listRegency = [];
      const regencylist = this.regencyData;

      regencylist.map((locale) => {
        listRegency.push({ title: locale.nama, value: locale.id });
        return false;
      });
      return listRegency;
    },
    getDistrict() {
      axios.get("http://127.0.0.1:8000/api/getDistrict/"+ this.regencyid).then((response) => { this.districtData = response.data.data })
      // console.log(this.districtData);
      const list = [];
      const districtList = this.districtData;

      districtList.map((locale) => {
        list.push({ title: locale.nama, value: locale.id });
        return false;
      });
      return list;
    },
    getVillages() {
      axios.get("http://127.0.0.1:8000/api/getVillage/"+ this.district).then((response) => { this.villagesData = response.data.data })
      // console.log(this.districtData);
      const list = [];
      const villagestList = this.villagesData;

      villagestList.map((locale) => {
        list.push({ title: locale.nama, value: locale.id });
        return false;
      });
      return list;
    },
    // 
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
    
    // getRegency(id) {
    //   axios.get("http://127.0.0.1:8000/api/getRegency/" + id).then((response) => { this.regencyData = response.data.data })
    //   // console.log(this.provinsiData);
    //   const list = [];
    //   const i18n = this.regencyData;

    //   i18n.map((locale) => {
    //     list.push({ title: locale.nama, value: locale.id });
    //     return false;
    //   });
    //   return list;
    // },
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
