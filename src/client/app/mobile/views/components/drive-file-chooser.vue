<template>
<div class="cdxzvcfawjxdyxsekbxbfgtplebnoneb">
	<div class="body">
		<header>
			<h1>%i18n:@select-file%<span class="count" v-if="files.length > 0">({{ files.length }})</span></h1>
			<button class="close" @click="cancel">%fa:times%</button>
			<button v-if="multiple" class="ok" @click="ok">%fa:check%</button>
		</header>
		<mk-drive class="drive" ref="browser"
			:select-file="true"
			:multiple="multiple"
			@change-selection="onChangeSelection"
			@selected="onSelected"
		/>
	</div>
</div>
</template>

<script lang="ts">
import Vue from 'vue';
export default Vue.extend({
	props: ['multiple'],
	data() {
		return {
			files: []
		};
	},
	methods: {
		onChangeSelection(files) {
			this.files = files;
		},
		onSelected(file) {
			this.$emit('selected', file);
			this.$destroy();
		},
		cancel() {
			this.$emit('canceled');
			this.$destroy();
		},
		ok() {
			this.$emit('selected', this.files);
			this.$destroy();
		}
	}
});
</script>

<style lang="stylus" scoped>
root(isDark)
	position fixed
	z-index 20000
	top 0
	left 0
	width 100%
	height 100%
	padding 8px
	background rgba(#000, 0.2)

	> .body
		width 100%
		height 100%
		background isDark ? #282c37 : #fff

		> header
			border-bottom solid 1px isDark ? #1b1f29 : #eee
			color isDark ? #fff : #111

			> h1
				margin 0
				padding 0
				text-align center
				line-height 42px
				font-size 1em
				font-weight normal

				> .count
					margin-left 4px
					opacity 0.5

			> .close
				position absolute
				top 0
				left 0
				line-height 42px
				width 42px

			> .ok
				position absolute
				top 0
				right 0
				line-height 42px
				width 42px

		> .drive
			height calc(100% - 42px)
			overflow scroll
			-webkit-overflow-scrolling touch

.cdxzvcfawjxdyxsekbxbfgtplebnoneb[data-darkmode]
	root(true)

.cdxzvcfawjxdyxsekbxbfgtplebnoneb:not([data-darkmode])
	root(false)

</style>
