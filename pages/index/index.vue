<template>
	<view>
		
		<view class="uni-padding-wrap uni-common-mt">
			<view class="uni-title uni-common-mt">
				Vertical Scroll
				<text>\n纵向滚动</text>
			</view>
			<view>
				<scroll-view :scroll-top="scrollTop" scroll-y="true" class="scroll-Y" @scrolltoupper="upper"
					@scrolltolower="lower" @scroll="scroll">
					<view id="demo1" class="uni-bg-red">A</view>
					<view id="demo2" class="uni-bg-green">B</view>
					<view id="demo3" class="uni-bg-blue">C</view>
				</scroll-view>
			</view>
			<view @tap="goTop" class="uni-link uni-center uni-common-mt">
				点击这里返回顶部
			</view>
		</view>
	</view>
	<view>
		<view class="page-body">
			<view class="btn-area">
				<!-- 点击按钮跳转外部网站，使用点击跳转按钮 -->
				<view>
    				<button @click="openExternalUrl">打开外部链接</button>
  				</view>
	
				<navigator url="/pages/my/my" open-type="switchTab" hover-class="other-navigator-hover">
					<button type="default">跳转tab页面</button>
				</navigator>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				scrollTop: 0,
				old: {
					scrollTop: 0
				}
			}
		},
		methods: {
			openExternalUrl() {
				const url = 'https://www.baidu.com'; // 替换为你想要打开的外部链接
				uni.openURL({
					url: url,
					success: (res) => {
					console.log('打开外部链接成功', res);
					},
					fail: (err) => {
					console.error('打开外部链接失败', err);
					}
				});
			},
			
			upper: function(e) {
				console.log(e)
			},
			lower: function(e) {
				console.log(e)
			},
			scroll: function(e) {
				console.log(e)
				this.old.scrollTop = e.detail.scrollTop
			},
			goTop: function(e) {
				// 解决view层不同步的问题
				this.scrollTop = this.old.scrollTop
				this.$nextTick(function() {
					this.scrollTop = 0
				});
				uni.showToast({
					icon: "none",
					title: "纵向滚动 scrollTop 值已被修改为 0"
				})
			}
		}
	}
</script>

<style>
	.scroll-Y {
		height: 300rpx;
	}
	.scroll-view_H {
		white-space: nowrap;
		width: 100%;
	}
	.scroll-view-item {
		height: 300rpx;
		line-height: 300rpx;
		text-align: center;
		font-size: 36rpx;
	}
	.scroll-view-item_H {
		display: inline-block;
		width: 100%;
		height: 300rpx;
		line-height: 300rpx;
		text-align: center;
		font-size: 36rpx;
	}
	.uni-bg-red {
		background-color: red;
		height: 200px;
	}
	.uni-bg-green{
		background-color: green;
		height: 200px;
	}
	.uni-bg-blue{
		background-color: blue;
		height: 200px;
	}
	
	
</style>