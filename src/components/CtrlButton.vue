<template>
  <div>
      <button :class="btnColor" class="btn-type"><slot></slot></button>
  </div>
</template>

<script>
export default {
  name: 'CtrlButton',
  props: {
    btnColor: {
      type: String,
      default: 'blue'
    }
  }
}
</script>

<style scoped>
.blue {
    background-color: #2188E9;
}
.red {
	background-color: #DD2E1D;
}
.orange {
    background-color: #FFB020;
}
.btn-type {
  border: 0;
	width: 98px;
	height: 40px;
	margin: 0 10px;
	text-align: center;
	color: #FFFFFF;
	border-radius: 5px;
	padding: 9px;
	font-size: 16px;
	font-family: PingFangSC-Regular, "PingFang SC", sans-serif;
}
</style>
