<template>
  <div class="box-type">
    <div class="time-card" id="time">
      {{ showTime }}
    </div>
  </div>
</template>

<script>
export default {
  name: 'BottomBox',
  props: {
    time: {
      type: Number,
      default: 0
    }
  },
  data: function () {
    return {
      aaa: 0
    }
  },
  computed: {
    showTime: function () {
      let h = this.showNum(parseInt(this.time / 60 / 60))
      let m = this.showNum(parseInt(this.time / 60) % 60)
      let s = this.showNum(this.time % 60)
      return [h, m, s].join(":")
    }
  },
  methods: {
    showNum: function (num) {
      if (num < 10) {
        return '0' + num
      }
      return num
    }
  }
}
</script>

<style scoped>
.box-type {
  width: 1220px;
  height: 440px;
  background-color: #F2F4F7;
  display: flex;
  flex-direction: row;
  justify-content: center;
  align-items: center;
}
.time-card {
  width: 960px;
  height: 200px;
  margin: 0 40px;
  padding: 127px 90px 113px 90px;
  font-size: 200px;
  font-family: PTMono-Bold, "PT Mono", monospace;
  font-weight: 700;
  text-align: center;
  color: #333333;
}
</style>
