<template>
  <div class="box-type">
    <hint-box :updown="updown" :bound="bound" :status="status" v-show="status != 0"></hint-box>
    <input-box @bound="getBound" v-show="status === 0"></input-box>
    <div class="btns-left" v-show="status === 0">
      <ctrl-button id="countup" @click.native.prevent="countUp">开始正计时</ctrl-button>
      <ctrl-button id="countdown" @click.native.prevent="countDown">开始倒计时</ctrl-button>
    </div>
    <div :class="status === 3 ? 'thinner-btns-mid' : 'btns-mid'">
      <ctrl-button id="resume" @click.native.prevent="countResume" v-show="status===2">恢复计时器</ctrl-button>
      <ctrl-button id="pause" @click.native.prevent="countPause" v-show="status===1">暂停计时器</ctrl-button>
    </div>
    <div class="btns-right" v-show="status != 0">
      <ctrl-button id="clear" btn-color="red" @click.native.prevent="countClear">{{ message }}</ctrl-button>
      <ctrl-button id="restart" btn-color="orange" @click.native.prevent="countRestart">重新再计时</ctrl-button>
    </div>
  </div>
</template>

<script>
import InputBox from "./InputBox"
import CtrlButton from "./CtrlButton"
import HintBox from "./HintBox"
export default {
  name: 'UpperBox',
  components: {
    InputBox,
    CtrlButton,
    HintBox
  },
  data: function () {
    return {
      time: 0,
      bound: 0,
      status: 0,
      updown: 0,
      intr: 100,
      timer: "",
      message: ""
    }
  },
  methods: {
    getBound (data) {
      this.bound = data
    },
    countUp () {
      this.updown = 1
      this.timer = setInterval(this.upTime, this.intr)
    },
    countDown () {
      this.updown = 0
      this.time = this.bound * 1000 / this.intr
      this.timer = setInterval(this.downTime, this.intr)
    },
    countResume () {
      this.status = 1
      if (this.updown === 0) {
        this.timer = setInterval(this.downTime, this.intr)
      }
      else {
        this.timer = setInterval(this.upTime, this.intr)
      }
    },
    countPause () {
      this.status = 2
      clearInterval(this.timer)
    },
    countRestart () {
      clearInterval(this.timer)
      if (this.updown === 0) {
        this.time = this.bound * 1000 / this.intr
      }
      else {
        this.time = 0
      }
      this.countResume()
    },
    countClear () {
      clearInterval(this.timer)
      this.time = 0
      this.status = 0
    },
    upTime () {
      if (this.time === this.bound * 1000 / this.intr) {
        this.status = 3
        clearInterval(this.timer)
      }
      else {
        this.status = 1
        this.time = this.time + 1
      }
    },
    downTime () {
      if (this.time === 0) {
        this.status = 3
        clearInterval(this.timer)
      }
      else {
        this.status = 1
        this.time = this.time - 1
      }
    }
  },
  watch: {
    status: function () {
      if (this.updown === 0) {
        this.message = "清空倒计时"
      }
      else {
        this.message = "清空正计时"
      }
    },
    time: function () {
      this.$emit('time', Math.floor(this.time * this.intr / 1000))
    }
  }
}
</script>

<style scoped>
.box-type {
  width: 1220px;
  height: 70px;
  background-color: #97A5BC;
  display: flex;
  flex-direction: row;
  align-content: flex-start;
  align-items: center;
}
.btns-left {
  width: 236px;
  height: 40px;
  display: flex;
  flex-direction: row;
  margin-left: 0;
  margin-top: 15px;
  margin-bottom: 15px;
}
.btns-mid {
  display: flex;
  width: 236px;
  height: 40px;
  margin-left: 0;
  margin-top: 15px;
  margin-bottom: 15px;
}
.thinner-btns-mid {
  display: flex;
  width: 211px;
  height: 40px;
  margin-left: 0;
  margin-top: 15px;
  margin-bottom: 15px;
}
.btns-right {
  display: flex;
  margin-top: 15px;
  margin-right: 30px;
  margin-bottom: 15px;
  margin-left: 520px;
  flex-direction: row;
  width: 236px;
  height: 40px;
}
</style>
