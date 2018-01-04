<template>
  <transition :name="slideDirection">
		<div v-show="currentSlide">
			<slot></slot>
		</div>
  </transition>
</template>

<script>
export default {
	props: {
		index: {type: Number, default: 0}
	},
	computed: {
		currentSlide () {
			return this.$parent.currentIndex == this.index
		},
    slideDirection () {
      return 'slide-' + this.$parent.direction
    }
	}
}
</script>

<style>
  .slide-right-enter-active {
		animation: slideRightIn .5s;
	}

  .slide-right-leave-active {
		animation: slideRightOut .5s;
		position: absolute;
		top: 0;
		left: 0;
		right: 0;
		bottom: 0;
		width: 100%;
	}

	@keyframes slideRightIn {
		from { transform: translateX(100%); }
		to { transform: translateX(0); }
	}

	@keyframes slideRightOut {
		from { transform: translateX(0); }
		to { transform: translateX(-100%); }
	}

  .slide-left-enter-active {
		animation: slideLeftIn .5s;
		position: absolute;
		top: 0;
		left: 0;
		right: 0;
		bottom: 0;
		width: 100%;
	}

  .slide-left-leave-active {
		animation: slideLeftOut .5s;
	}

	@keyframes slideLeftIn {
		from { transform: translateX(-100%); }
		to { transform: translateX(0); }
	}

	@keyframes slideLeftOut {
		from { transform: translateX(0); }
		to { transform: translateX(100%); }
	}
</style>