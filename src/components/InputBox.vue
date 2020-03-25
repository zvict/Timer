<template>
  <div class="box-type">
    <div class="input-type">
      <input type="text" id="hour" v-model="inHour" placeholder="0" @input="toTime">时
    </div>
    <div class="input-type">
      <input type="text" id="minute" v-model="inMinute" placeholder="0" @input="toTime">分
    </div>
    <div class="input-type">
      <input type="text" id="second" v-model="inSecond" placeholder="0" @input="toTime">秒
    </div>
  </div>
</template>

<script>
export default {
  name: 'InputBox',
  data: function () {
	return {
      inHour: "0",
      inMinute: "0",
	  inSecond: "0",
	  bound: 0
	}
  },
  methods: {
    toTime: function () {
      let second = Number(this.inSecond)
      let minute = Number(this.inMinute)
      let hour = Number(this.inHour)
      second = second >= 0 ? second : 0
      minute = minute >= 0 ? minute : 0
      hour = hour >= 0 ? hour : 0
      second = second > 59 ? 59 : second
	  minute = minute > 59 ? 59 : minute
	  this.bound = hour * 60 * 60 + minute * 60 + second
	  this.$emit('bound', this.bound)
    }
  }
}
</script>

<style scoped>
.box-type {
  width: 270px;
  height: 40px;
  display: flex;
  flex-direction: row;
  margin: 15px 0 15px 30px;
}
.input-type {
  width: 70px;
  height: 40px;
  margin: 0 10px;
  display: flex;
  flex-direction: row;
  align-items: center;
  justify-content: space-between;
  background-color: #FFFFFF;
  border-radius: 5px;
  padding-right: 9px;
  font-family: PingFangSC-Regular, "PingFang SC", sans-serif;
}
input {
  width: 20px;
  border: 0;
  margin-left: 9px;
  color: #BFBFBF;
}
</style>
