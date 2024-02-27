<template>
  <div class="root">
    <parallax-cloud />
    <main-feature />
    <more-feature />
  </div>
</template>

<style lang="scss" scoped>
@import './feature-style.scss';
</style>

<script>
import MainFeature from './MainFeature';
import MoreFeature from './MoreFeature';
import Cloud from '../Parallax/Cloud';

export default {
  components: {
    MainFeature,
    MoreFeature,
    'parallax-cloud': Cloud,
  },
};
</script>
