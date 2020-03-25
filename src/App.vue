<template>
  <div id="app">
    <upper-box @time="getTime"></upper-box>
    <bottom-box :time="time"></bottom-box>
  </div>
</template>

<script>
import UpperBox from "./components/UpperBox"
import BottomBox from "./components/BottomBox"
export default {
  name: 'App',
  components: {
    UpperBox,
    BottomBox
  },
  data: function () {
    return {
      time: 0
    }
  },
  methods: {
    getTime (data) {
      this.time = data
      // console.log("app-time", this.time)
    },
  }
}
</script>

<style>
#app {
	width: 1220px;
	height: 510px;
	position: absolute;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
</style>
