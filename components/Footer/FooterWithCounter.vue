<template>
  <div class="footer-counter">
    <counter />
    <subscribe />
    <footer-main />
  </div>
</template>

<style lang="scss" scoped>
@import './footer-style.scss';
</style>

<script>
import Counter from '../Counter';
import Subscribe from '../SubscribeForm';
import Footer from './Footer';

export default {
  components: {
    Counter,
    Subscribe,
    'footer-main': Footer,
  },
};
</script>
