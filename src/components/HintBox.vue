<template>
  <div :class="status === 3 ? 'wider-box-type' : 'box-type'" id="hint">
    {{ message }}
  </div>
</template>

<script>
export default {
  name: 'HintBox',
  props: {
    bound: {
      type: Number,
      default: 0
    },
    updown: {
      type: Number,
      default: 0
    },
    status: {
      type: Number,
      default: 0
    }
  },
  data: function () {
    return {
      message: '正在倒计时 00:00:00'
    }
  },
  watch: {
    status: function () {
      let h = this.showNum(parseInt(this.bound / 60 / 60))
      let m = this.showNum(parseInt(this.bound / 60) % 60)
      let s = this.showNum(this.bound % 60)
      if (this.status === 3) {
        if (this.updown === 0) {
          this.message = '倒计时 ' + [h, m, s].join(":") + ' 已结束'
        }
        else {
          this.message = '正计时 ' + [h, m, s].join(":") + ' 已结束'
        }
      }
      else {
        if (this.updown === 0) {
          this.message = '正在倒计时 ' + [h, m, s].join(":")
        }
        else {
          this.message = '正在正计时 ' + [h, m, s].join(":")
        }
      }
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
  width: 167px;
  height: 22px;
  margin: 24px 0 24px 30px;
  color: #FFFFFF;
  font-size: 16px;
  font-family: PingFangSC-Regular, "PingFang SC", sans-serif;
}
.wider-box-type {
  width: 192px;
  height: 22px;
  margin: 24px 0 24px 30px;
  color: #FFFFFF;
  font-size: 16px;
  font-family: PingFangSC-Regular, "PingFang SC", sans-serif;
}
</style>
