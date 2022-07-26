<template>
  <div class="wrapper">
    倒计时组件父级
    <CountDown v-slot="timeObj" :time="5">
      <div>
        还剩{{timeObj.d}}天{{timeObj.hh}}小时{{timeObj.mm}}分{{timeObj.ss}}秒  
      </div>  
    </CountDown>
  </div>
</template>

<script>
import CountDown from 'components/CountDown.vue'
export default {
  name: 'CountDown',
  components: {
    CountDown
  },
  data() {
    return {
    };
  },
  created() {},
  methods: {},
};
</script>
<style lang="scss" scoped>
.wrapper{}
</style>