<template>
	<div class="recommend" ref="recommend">
		<div v-if="recommends.length>0" class="recommend-content">
			<div class="slider-wrapper">
				<slider>
					<div v-for="item in recommends ">
						<a :href="item.linkUrl">
							<img :src="item.picUrl" alt="">
						</a>
					</div>
				</slider>
			</div>
		</div>
		<div class="recommend-list">
			<h1 class="list-title">热门歌单推荐</h1>
		</div>
	</div>
</template>

<script>
	import Slider from 'base/slider/slider.vue'
	import {getRecommend} from 'api/recommend'
	import {ERR_OK} from 'api/config'
	export default {
		data() {
			return {
				recommends:[]
			};
		},
		created() {
			this._getRecommend();
		},
		methods:{
			_getRecommend() {
				getRecommend().then((res)=>{
					if(res.code === ERR_OK){
						this.recommends=res.data.slider;
					}
				})
			}
		},
		components:{
			Slider
		}
	}
</script>

<style scoped lang="stylus" rel="stylesheet/stylus">
	@import "~common/stylus/variable"
	@import "~common/stylus/mixin"
	.recommend
		position: fixed
		width: 100%
		top: 88px
		bottom: 0
// 		.recommend-content
// 			height: 100%
// 			overflow: hidden
// 			.slider-wrapper
// 				position: relative
// 				width: 100%
// 				overflow: hidden
			.recommend-list
				.list-title
					height: 65px
					line-height: 65px
					text-align: center
					font-size: $font-size-medium
					color: $color-theme
// 				.item
// 					display: flex
// 					box-sizing: border-box
// 					align-items: center
// 					padding: 0 20px 20px 20px
// 					.icon
// 						flex: 0 0 60px
// 						width: 60px
// 						padding-right: 20px
					.text
						display: flex
						flex-direction: column
						justify-content: center
						flex: 1
						line-height: 20px
						overflow: hidden
						font-size: $font-size-medium
						.name
							margin-bottom: 10px
							color: $color-text
						.desc
							color: $color-text-d
</style>
