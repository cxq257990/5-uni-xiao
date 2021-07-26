
回调
onToggleIDSelect() {
				let fn = async () => {
					this.showIDSelect = !this.showIDSelect;
					if (this.showIDSelect || this.showEmoji) {
						this.showBg = true;
					} else {
						this.showBg = false;
					}

				};
				this.$util.checkIslogin(fn.bind(null));
			},
  
  	checkIslogin: (fn) => {
		if (!!uni.getStorageSync('userPhone')) {
			fn();
		} else {
			uni.navigateTo({
				url: '/pages/login/login'
			});
		}
	},
