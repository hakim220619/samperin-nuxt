<template>
  <v-navigation-drawer
    v-if="isMobile"
    v-model="openDrawer"
    fixed
    temporary
    class="mobile-nav"
  >
    <mobile-menu :open="openDrawer" />
  </v-navigation-drawer>
  <v-app-bar
    id="header"
    v-scroll="handleScroll"
    :class="{ fixed: fixed, 'open-drawer': openDrawer }"
    class="header"
    app
  >
    <div class="header-top">
      <v-container :class="{ 'fixed-width': isDesktop }">
        <div class="logo">
          <v-btn
            v-if="isMobile"
            :class="{ 'is-active': openDrawer }"
            class="hamburger hamburger--spin mobile-menu"
            variant="text"
            icon
            @click.stop="handleToggleOpen"
          >
            <span class="hamburger-box">
              <span class="bar hamburger-inner" />
            </span>
          </v-btn>
          <nuxt-link
            v-if="invert"
            :to="routerLink.hosting.home"
          >
            <img :src="logo" alt="logo">
            {{ brand.hosting.name }}
          </nuxt-link>
          <span v-if="!invert && loaded">
            <a
              v-smooth-scroll="{ offset: 100 }"
              href="#home"
              class="anchor-link scrollactive-item"
            >
              <img :src="logo" alt="logo">
              {{ brand.hosting.name }}
            </a>
          </span>
        </div>
        <div class="user-menu">
          <hidden point="smDown">
            <v-icon>mdi-phone</v-icon>
            085 702 889 886
            <v-divider class="divider" />
            <v-btn :href="routerLink.hosting.login" class="text-btn" variant="text">
              {{ $t('hostingLanding.header_login') }}
            </v-btn>
            <v-btn
              :href="routerLink.hosting.register"
              color="secondary"
              class="button"
              variant="flat"
              v-text="$t('hostingLanding.header_register')"
            />
          </hidden>
          <setting-menu :invert="invert" />
        </div>
      </v-container>
    </div>
    <hidden point="smDown">
      <div class="navigation">
        <v-container class="fixed-width">
          <nav class="nav-menu">
            <v-btn
              v-if="invert"
              :href="routerLink.hosting.home"
              class="icon"
              icon
            >
              <v-icon>mdi-home</v-icon>
            </v-btn>
            <v-btn
              v-if="!invert"
              href="#home"
              class="icon"
              icon
            >
              <v-icon>mdi-home</v-icon>
            </v-btn>
            <ul class="scrollactive-nav">
              <li
                v-for="(item, index) in menuList"
                :key="index"
              >
                <v-btn
                  v-if="!invert"
                  v-smooth-scroll="{ offset: -100 }"
                  :href="item.url"
                  :class="{ active: activeMenu === item.name }"
                  class="menu-link"
                  variant="text"
                  @click="scrollToMyEl(item.name)"
                  v-text="$t('hostingLanding.header_'+item.name)"
                />
                <v-btn
                  v-if="invert"
                  :href="'/' + item.url"
                  variant="text"
                  v-text="$t('hostingLanding.header_'+item.name)"
                />
                
              </li>
              <li>
                <v-btn
                  :href="routerLink.hosting.tentang"
                  variant="text"
                  v-text="$t('hostingLanding.header_tentang')"
                />
              </li>
              <li>
                <v-btn
                  :href="routerLink.hosting.bayar"
                  variant="text"
                  v-text="$t('hostingLanding.header_bayar')"
                />
              </li>
              <li>
                <v-btn
                  :href="routerLink.hosting.berita"
                  variant="text"
                  v-text="$t('hostingLanding.header_berita')"
                />
              </li>
              <li>
                <v-btn
                  :href="routerLink.hosting.contact"
                  variant="text"
                  v-text="$t('hostingLanding.header_contact')"
                />
              </li>
            </ul>
          </nav>
        </v-container>
      </div>
    </hidden>
  </v-app-bar>
</template>

<style lang="scss" scoped>
@import './header-style.scss';
</style>

<script>
import { inject } from 'vue';
import logo from '@/assets/images/hosting-logo.svg';
import link from '@/assets/text/link';
import brand from '@/assets/text/brand';
import { useRouter } from '#app';
import Hidden from '../Hidden';
import navMenu from './menu';
import Settings from './Settings';
import MobileMenu from './MobileMenu';

let counter = 0;
function createData(name, url, offset) {
  counter += 1;
  return {
    id: counter,
    name,
    url,
    offset,
  };
}

export default {
  components: {
    'setting-menu': Settings,
    Hidden,
    MobileMenu,
  },
  props: {
    invert: {
      type: Boolean,
      default: false,
    },
  },
  setup() {
    const smoothScroll = inject('smoothScroll');
    function scrollToMyEl(elemId) {
      const myEl = document.getElementById(elemId);
      const router = useRouter();

      router.push(`#${elemId}`);
      smoothScroll({
        scrollTo: myEl, // scrollTo is also allowed to be number
        hash: `#${elemId}`, // required if updateHistory is true
        offset: -100,
      });
    }

    return {
      scrollToMyEl,
    };
  },
  data() {
    return {
      logo,
      routerLink: link,
      loaded: false,
      brand,
      sections: {},
      activeMenu: '',
      fixed: false,
      openDrawer: null,
      navOffset: 20,
      menuList: [
        createData(navMenu[0], '#' + navMenu[0]),
        createData(navMenu[1], '#' + navMenu[1]),
        createData(navMenu[2], '#' + navMenu[2]),

      ],
    };
  },
  computed: {
    isMobile() {
      const smDown = this.$vuetify.display.smAndDown;
      return smDown;
    },
    isDesktop() {
      const mdUp = this.$vuetify.display.mdAndUp;
      return mdUp;
    },
  },
  mounted() {
    this.loaded = true;
    const id = window.location.hash;
    const content = id.replace('#', '');
    const element = document.getElementById(content);
    if (element) {
      element.scrollIntoView();
    }

    const section = document.querySelectorAll('.scroll-nav-content > *');
    Array.prototype.forEach.call(section, (e) => {
      this.sections[e.id] = e.offsetTop;
    });
  },
  methods: {
    handleScroll() {
      const scrollPosition = document.documentElement.scrollTop || document.body.scrollTop;
      const topPosition = scrollPosition + 200;

      Object.keys(this.sections).forEach((i) => {
        if (this.sections[i] <= topPosition) {
          this.activeMenu = i;
        }
      });

      if (scrollPosition > 70) {
        this.fixed = true;
      } else {
        this.fixed = false;
      }
    },
    handleToggleOpen() {
      this.openDrawer = !this.openDrawer;
    },
  },
};
</script>
