<template>
  <!-- <div class="wrapper">
    还剩{{days}}天{{hours}}小时{{mins}}分{{seconds}}秒
  </div> -->
  <div class="wrapper">
    <slot v-bind="{
      d: days, 
      h: hours, 
      m: mins, 
      s: seconds,
      hh: `00${hours}`.slice(-2),
      mm: `00${mins}`.slice(-2),
      ss: `00${seconds}`.slice(-2)
    }">
    </slot>
    <!-- 还剩{{days}}天{{hours}}小时{{mins}}分{{seconds}}秒 -->
  </div>
</template>

<script>
export default {
  name: 'CountDown',
  props: {
    time: {
      type: [String, Number],
      default: 0
    },
    isMilliSecond: {
      type: Boolean,
      default: false
    },
    end: {
      type: [String, Number],
    },
    refreshCounter: {
      type: [String, Number],
      default: 0
    }
  },
  data() {
    return {
      days: '0',
      hours: '00',
      mins: '00',
      seconds: '00',
      timer: null,
      curTime: 0
    };
  },
  computed: {
    duration () {
      if (this.end) {
        let end = String(this.end).length >= 13 ? +this.end : +this.end * 1000
        end -= Date.now()
        return end
      }
      const time = this.isMilliSecond ? Math.round(+this.time / 1000) : Math.round(+this.time)
      return time
    }
  },
  mounted () {
    this.curTime = Date.now()
    this.countDown()
  },
  watch: {
    duration() {
      this.countDown()
    },
    refreshCounter() {
      this.countDown()
    }
  },
  methods: {
    countDown () {
      this.getTime(this.duration)
    },
    getTime (duration) {
      this.timer && clearTimeout(this.timer)
      if (duration <= 0) {
        return 
      }
      const { dd = 0, hh = 0, mm = 0, ss = 0 } = this.durationFormatter(duration)
      this.days = dd
      this.hours = hh
      this.mins = mm
      this.seconds = ss
      this.timer = setTimeout(() => {
        const now = Date.now()
        const diffTime = Math.floor((now - this.curTime) / 1000)
        const step = diffTime > 1 ? diffTime : 1
        this.curTime = now
        this.getTime(duration - step)
      }, 1000);
    },
    durationFormatter (time) { // 120
      if (!time) return { ss: 0 }
      let t = time
      const ss = t % 60 // 0
      t = (t - ss) / 60 // 2
      if (t < 1) return { ss }
      const mm = t % 60 // 2
      t = (t - mm) / 60 
      if(t < 1) return { mm, ss}
      const hh = t % 24
      t = (t - hh) / 24
      if(t < 1) return { hh, mm, ss}
      const dd = t
      return { dd, hh, mm, ss}
    }
  },
};
</script>
<style scoped>
.wrapper{}
</style>