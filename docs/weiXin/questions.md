<!--
 * @Description:
 * @Author: panrui
 * @Date: 2023-04-25 08:57:17
 * @LastEditTime: 2023-05-30 09:58:44
 * @LastEditors: panrui
 * 不忘初心,不负梦想
-->

## 最后更新时间 2023-05-30 09-45-53

## 问题记录

#### 小程序已经打开触发过 onload 方法，如果再次扫码(小程序二维码)，是否会再次触发 onload 钩子

> 会重新触发 onload 方法

#### form 表单提交涉及多张图片

```js
// 图片选择的同时,调用wx.uploadFile 上传文件接口,服务器返回图片地址,然后结合表单进行提交

// 图片选择的同时,将图片转换成base64 存入数组当中,并跟随json数据进行传输
wx.chooseImage({
  sizeType: ["compressed"],
  sourceType: ["album", "camera"],
  success(res) {
    const isLt300k = res.tempFiles[0].size / 1024 < 300;
    if (!isLt300k) {
      uni.showToast({
        title: "图片太大了",
        duration: 1000,
      });
      return;
    }
    _this.uploadList = _this.uploadList.concat(res.tempFilePaths);
    wx.getFileSystemManager().readFile({
      filePath: res.tempFilePaths[0],
      encoding: "base64",
      success: (data) => {
        _this.pic = _this.pic.concat(data.data);
      },
      fail: (error) => {
        console.log(error);
      },
      complete: () => {
        console.log("转换完成");
      },
    });
  },
});
```

#### （右上角胶囊按钮）的布局位置信息

```js
// 设置固定的高度导致显示异常
// 获取菜单按钮（右上角胶囊按钮）的布局位置信息。坐标信息以屏幕左上角为原点
wx.getMenuButtonBoundingClientRect();
```

#### 数据通过 setData 更新，但是页面没有渲染

```js
// 解决方案：将一些普通的变量不用在data对象当中定义,或者定义的时候将默认值修改未false或者null
data: {
  balance: null, // 金币数量
  level: null // 用户等级
},

// 然后对变量进行更新
_this.setData({
  balance: data.balance,
  level: data.level
})
```

#### "errMsg":"hideLoading:fail:toast can't be found"

> hideloading( )和 toast 的问题，不能多个 loading 和 toast 同时触发

#### 使用 scroll-view 组件时候，我设置高度为 100%，在编辑器里面他是按照父元素的高度进行设置，但是在真机里面他按照屏幕的高度进行计算

```
设置父元素
width:100%;
height:100%;
overflow:hidden;

scroll-view 添加一个calss
然后设置成
width: 100%;
height: 100%;

注释1：因为调试里面是chrome内核，安卓里面是腾讯的x5内核，苹果里面是webkit内核
注释2：scroll-view 组件有个单独属性enable-flex，是否启用flexbox布局
```

#### 小程序 iOS 系统橡皮筋效果处理

```
1：当整个无需滚动时候，在页面json配置文件当中，添加disableScroll:true 禁止整个页面滚动，局部还是可以存在滚动元素
```

#### 小程序对接腾讯地图问题

```
1：使用marker进行地图点位标记，点击标记的点位时，返回的markerid不是我传递的id，而是返回一个900000开头的Number类型数据。
虽然官方文档确实说明了，该字段的数据类型是number
https://developers.weixin.qq.com/miniprogram/dev/component/map.html
但是我不同小程序，调用同一个接口。返回值同样的情况下，一个可以正常返回，一个不可以。不可以的小程序，真机调试却正常。
注释1：最后查明的原因是我调用的基础库版本不一致导致的，并且小程序后续版本已作出兼容处理，将markerid 在对象和对象的detail属性对象中都添加了
```

#### 小程序全屏模式开发记录

```
可以在页面josn文件中进行导航栏配置
"navigationStyle": "custom"
```

#### text 组件 长按复制功能

```
使用基础库2.12.1，text 组件的 selectable 换成 user-select 之后就可以复制，但是文本会从 inline 变成 inline-block 需要开发者自行适配
<text class="templeinfo_box_text1" user-select="true">寺庙信息</text>
```

#### 微信小程序授权用户接口调整解决方案

```js
// 使用uniapp方案
<!-- #ifdef MP-WEIXIN -->
<button v-if="canIUseGetUserProfile" class="login_box_button" @click="getUserProfile">微信登录</button>
<button v-else class="login_box_button" open-type="getUserInfo" @getuserinfo="handUserinfo">微信登录</button>
<!-- #endif -->
```

```js
<script>
	import config from '@/common/config.js'
	export default {
		name: "Login",
		data() {
			return {
				canIUseGetUserProfile: false,
				encryptedData: '', //加密数据
				jsCode: '', // 登录code
				iv: '' // 加密数据
			};
		},
		props: {
		},
		mounted() {
			// #ifdef MP-WEIXIN
				if(wx.getUserProfile) {
					this.canIUseGetUserProfile = true
				}
			// #endif
		},
		methods: {
			/**
			 * 获取用户头像信息
			 */
			getUserProfile: function(e) {
				let _this = this
				// #ifdef MP-WEIXIN
				wx.getUserProfile({
					desc: '用于展示头像和名称',
					success: (data) => {
						console.log(data)
						uni.login({
							success(res) {
								if (res.code) {
									_this.jsCode = res.code // 更新jsCode
									_this.getToken(data)
								}
							}
						})
					},
					fail: (error) => {
						console.log(error)
					},
					complete: () => {
					}
				})
				// #endif
			},
			/**
			 * 登录
			 */
			handUserinfo: function(e) {
				let _this = this
				// #ifndef H5
				// 获取登录code
				uni.login({
					success(res) {
						if (res.code) {
							_this.jsCode = res.code // 更新jsCode
							uni.getSetting({
								success: function(res) {
									if (res.authSetting['scope.userInfo']) {
										// 已授权情况
										// #ifndef H5
										uni.getUserInfo({
											success(res) {
												_this.getToken(res)
											}
										})
										// #endif
									} else {
										_this.getToken(e.target)
									}
								}
							})
						}
					}
				})
				// #endif
			},
			/**
			 * 获取登录token
			 */
			getToken: function(data) {
				let _this = this
				// 更新授权信息
				uni.showLoading({
					title: '获取信息中'
				});
				_this.encryptedData = data.encryptedData
				_this.iv = data.iv
				const url = _this.canIUseGetUserProfile ? `/user/${config.version}/getToken` : '/user/getToken'
				_this.$ajax.post(url, {
					code: _this.jsCode,
					encryptedData: _this.encryptedData,
					iv: _this.iv
				}).then(res => {
					uni.hideLoading()
					if (res.error == 0) {
						const data = res.res
						// 更新token
						// getApp().globalData.token = data.token
						try {
							uni.setStorageSync('token', data.token) // 将token同步写入本地缓存中
							uni.setStorageSync('user_name', data.nickname) // 将token同步写入本地缓存中
							uni.setStorageSync('user_image', data.face_icon) // 将token同步写入本地缓存中
							_this.$emit('callback') //触发回调
						} catch (e) {
							//TODO handle the exception
						}
					}
				}).catch(error => {
					uni.hideLoading()
					uni.showToast({
						title: '获取信息失败',
						duration: 2000
					})
				})
			}
		}
	}
</script>
```

## 待测试功能

> 小程序可以通过 background-image 设置背景图片，但仅支持网络图片

> 自定义组件中访问 app 对象

> 自定义组件中使用 npm 包

#### 微信 URL Scheme 详细参数

```js
weixin:// 打开微信
weixin://dl/scan 扫一扫
weixin://dl/feedback 反馈
weixin://dl/moments 朋友圈
weixin://dl/settings 设置
weixin://dl/notifications 消息通知设置
weixin://dl/chat 聊天设置
weixin://dl/general 通用设置
weixin://dl/officialaccounts 公众号
weixin://dl/games 游戏
weixin://dl/help 帮助
weixin://dl/feedback 反馈
weixin://dl/profile 个人信息
weixin://dl/features 功能插件

data(){
	return{
		url: 'weixin://'
	}
},
methods:{
	clickWechat() { //打开外部微信
		plus.runtime.openURL(this.url, function(res) {
			console.log(res);
		});
	}
}
```

## 版本变更

#### getUserInfo && getUserProFile

```
getUserInfo
2021.4.13 以后发布的新版本小程序 getUserInfo接口不在提供用户的头像和名称
getUserInfo 接口提供的返回值中 encryptedData 和 iv 可以解析出用户的openid等字段

getUserProFile
支持的小程序基础库版本 2.10.4 2.15.0及以上
getUserProFile 只在2.16.0及以上版本中,提供加密字符串,并且加密字符串当中不能解析用户的openid字段

code2Session
通过wx.login 登录接口获取到的code 可以查询用户的openid等信息
```
