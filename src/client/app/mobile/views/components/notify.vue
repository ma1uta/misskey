<template>
<div class="mk-notify">
	<div>
		<mk-notification-preview :notification="notification"/>
	</div>
</div>
</template>

<script lang="ts">
import Vue from 'vue';
import * as anime from 'animejs';

export default Vue.extend({
	props: ['notification'],
	mounted() {
		this.$nextTick(() => {
			anime({
				targets: this.$el,
				bottom: '0px',
				duration: 500,
				easing: 'easeOutQuad'
			});

			setTimeout(() => {
				anime({
					targets: this.$el,
					bottom: `-${this.$el.offsetHeight}px`,
					duration: 500,
					easing: 'easeOutQuad',
					complete: () => this.$destroy()
				});
			}, 6000);
		});
	}
});
</script>

<style lang="stylus" scoped>
.mk-notify
	$height = 78px

	position fixed
	z-index 1024
	bottom -($height)
	left 0
	right 0
	width 100%
	max-width 500px
	height $height
	margin 0 auto
	padding 8px
	pointer-events none
	font-size 80%

	> div
		height 100%
		-webkit-backdrop-filter blur(2px)
		backdrop-filter blur(2px)
		background-color rgba(#000, 0.5)
		border-radius 7px
		overflow hidden

</style>
