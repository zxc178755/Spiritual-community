<script>
	export default {
		globalData: {
			_isInput: false,
			inputBoxProps: {
				_placeholder: '',
				_objId: -1
			},
		},
		methods: {
			isInputWatch(callBack) {
				Object.defineProperty(this.globalData, 'isInput', {
					enumerable: true,
					configurable: true,
					set(e) { // 设置了 set 和 get 就不能有 value, 和 wriatable
						this._isInput = e
						console.log('globalData')
						if (callBack)
							callBack(e)
					},
					get() {
						return this._isInput
					}
				})
			},
			placeholderWatch(callBack) {
				let inputBoxProps = this.globalData.inputBoxProps
				Object.defineProperty(inputBoxProps, 'placeholder', {
					enumerable: true,
					configurable: true,
					set(e) {
						let pre = inputBoxProps._placeholder
						if (callBack && pre !== e) {
							inputBoxProps._placeholder = e
							callBack(e)
						}
					},
					get() {
						return inputBoxProps._placeholder
					}
				})
			},
			objIdWatch(callBack) {
				let inputBoxProps = this.globalData.inputBoxProps
				Object.defineProperty(inputBoxProps, 'objId', {
					enumerable: true,
					configurable: true,
					set(e) {
						let pre = inputBoxProps._objId
						console.log('pre', pre)
						console.log('new', e)
						if (pre !== e) {
							inputBoxProps._objId = e
							callBack()
						}
					},
					get() {
						return inputBoxProps._objId
					}
				})
			},
		},
		onLaunch: function() {
			console.log('App Launch')
		},
		onShow: function() {
			console.log('App Show')
		},
		onHide: function() {
			console.log('App Hide')
		}
	}
</script>

<style>
	/*每个页面公共css */
	@import "./static/icon/iconfont.css";
	@import "./common.css";
</style>
