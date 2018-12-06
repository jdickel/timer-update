<template>
  <div class='value'>{{ animatedNumber }}</div>
</template>
<script>
import { TweenMax } from "gsap/TweenMax";

export default {
  data() {
    return {
      lastUpdate: null,
      value: 1,
      production: 100,
      tweenedNumber: 0
    };
  },
  computed: {
    animatedNumber() {
      return this.tweenedNumber.toFixed(2);
    }
  },
  mounted() {
    let _self = this;
    setInterval(function() {
      _self.update(new Date().getTime());
    }, 500);
  },
  methods: {
    update(timestamp) {
      if (this.lastUpdate == null) {
        this.lastUpdate = timestamp;
        return;
      }
      var delta = timestamp - this.lastUpdate;
      this.lastUpdate = timestamp;
      this.value += (delta / 1000) * this.production;
    }
  },
  watch: {
    value(newValue) {
      TweenMax.to(this.$data, 0.5, { tweenedNumber: newValue });
    }
  }
};
</script>
