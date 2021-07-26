
//顶部状态栏-标题
created() {
			let res = uni.getSystemInfoSync();
			this.statusBarHeight = res.statusBarHeight;
			let menu = wx.getMenuButtonBoundingClientRect();
			//获取获取菜单按钮（右上角胶囊按钮）的布局位置信息。坐标信息以屏幕左上角为原点。（top表示上边框到手机顶部的距离 bottom是下边框到手机顶部的距离）
			console.log('menu:' + menu + '这个？' + res.statusBarHeight)
			this.titleBarHeight = (menu.top - res.statusBarHeight) * 2 + menu.height;
			if (res.model.indexOf('iPhone') > -1) {
				this.titleBarHeight += 4
			}
		},
 //搜索
 <template>
	<view class="vSearch">
		<view class="iconfont icon-sousuo icon-search"></view>
		<input type="text" class="uni-input" confirm-type="search" placeholder-class="input-placeholder"
			:value="inputValue" placeholder="请输入关键词进行搜索" @input="onInput" @confirm="onConfirm" @focus="onFocus"
			@blur="onBlur" />
		<view v-if="showDelete" class="iconfont icon-s-shanchutupian icon-cancel" @click="onClear"></view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				showDelete: false,
				inputValue: '',
			}
		},
		methods: {
			clear(){
				this.inputValue = ""
			},
			onInput(event) {
				this.inputValue = event.target.value
			},
			onFocus() {
				this.showDelete = true;
			},
			onBlur() {
				this.showDelete = false;
			},
			onConfirm() {
				this.$emit('emitSearch', {
					type: "ok",
					val: this.inputValue
				})
			},
			onClear() {
				this.inputValue = ""
				this.$emit('emitSearch', {
					type: "clear",
					val: this.inputValue
				})
			}
		}
	}
</script>

<style lang="scss" scoped>
	.vSearch {
		padding: 0 30rpx;
		width: 100%;
		height: 88rpx;
		background: #F3F3F3;
		border-radius: 45rpx;
		box-sizing: border-box;
		display: flex;
		align-items: center;
		justify-content: space-between;

		.uni-input {
			flex: 1;
			height: 30rpx;
			font-size: 30rpx;
			font-family: Microsoft YaHei;
			font-weight: 400;
			color: $uni-text-color;
		}

		.input-placeholder {
			height: 30rpx;
			font-size: 30rpx;
			font-family: Microsoft YaHei;
			font-weight: 400;
			color: $uni-text-color-placeholder;
			text-align: left;
		}

		.iconfont {
			color: $uni-text-color;
			font-size: 36rpx;
		}

		.icon-search {
			margin-right: 15rpx;
			border: 3rpx solid #EAEAEA;
			border-radius: 50%;
		}

		.icon-cancel {
			margin-left: 15rpx;
		}
	}
</style>
