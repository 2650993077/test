<template>
	<view class="app">
		<view class="login" v-if="isReg">
			<view>
				<!--v-if 条件判断，不满足条件的话则不会出现在dom中-->
				<view class="name">
					用户名：
					<input class="nameInput" placeholder="请输入用户名" type="text" v-model="name">
				</view>
				<view class="passWord">
					密 码：
					<input class="passwordInput" placeholder="请输密码" type="password" v-model="password">
				</view>
				<button class="butLogin" @click="login()">登 录</button>
				<button class="butRegister" @click="reg()">注 册</button>
			</view>
		</view>
		<view class="regins" v-else>
			<view>
				<view class="name">
					用户名：
					<input class="nameInput" placeholder="请输入用户名" type="text" v-model="name">
				</view>

				<view class="passWord">
					密 码：
					<input class="passwordInput" placeholder="请输入密码" type="password" v-model="password">
				</view>

				<view class="passWords">
					确认密码：
					<input class="passwordsInput" placeholder="请确认密码" type="password" v-model="repeat">
				</view>
				<button class="butLogin" @click="addUser()">确 定</button>
				<button class="butRegister" @click="cancel()">取 消</button>
			</view>
		</view>
	</view>
	
</template>
<script>
	export default {
		data() {
			return {
				isReg: true,
				name: "",
				password: "",
				repeat: ""
			}
		},
		onLoad() {

		},
		methods: {
			/*登录按钮的方法*/
			login() {
				if (this.name.length >= 6 && this.password.length >= 6) { //验证用户名跟密码长度不能小于6
					if (localStorage.getItem("name") === this.name &&
						localStorage.getItem("password") === this.password) { //"localStorage.getItem("name") "获取本地value地址
						console.log("用户名：" + this.name);
						console.log("密码：" + this.password);
						this.name = "";
						this.password = "";
						this.$router.push(""); //参数为跳转的网页
						console.log("登录进来了");
					} else {
						alert('用户名或密码不正确');
					}
				} else {
					alert('用户名或者密码少于6位数');
				}
			},
			/*注册按钮的方法*/
			reg() {
				this.isReg = false; //登录页面不展示
				this.name = "";
				this.password = "";
				this.repeat = "";
			},
			cancel() { //取消注册返回登录页面
				this.isReg = true;
			},
			addUser() { //确认注册
				if (!isNaN(this.name) && !isNaN(this.password) && !isNaN(this.repeat)) { //验证用户名跟密码是否是数字，数字：true，字母：false
					if (this.name.length >= 6 && this.password.length >= 6 && this.repeat.length >= 6) { //验证用户名跟密码长度不能小于6
						if (this.name !== localStorage.getItem("name")) { //验证用户名是否重复
							if (this.password === this.repeat) { //验证两次输入密码是否一致
								//将名字和密码存入localstorage中 
								localStorage.setItem("password", this.password)
								localStorage.setItem("name", this.name);
								//将输入框清空
								this.name = "";
								this.password = "";
								this.isReg = true; //显示登录页面
							} else {
								alert("两次密码不一致");
							}
						} else {
							alert("用户名已经被注册，重新输入用户名")
						}
					} else {
						alert("用户名或者密码少于6位数");
					}
				} else {
					alert("用户名输入不正确，请输入数字");
				}
			}
		}
	}
</script>

<style>
	.butRegister {
		width: 150rpx;
		height: 70rpx;
		line-height: 74rpx;
		margin-left: 60%;
		margin-top: -9%;
	}

	.butLogin {
		width: 150rpx;
		height: 70rpx;
		line-height: 74rpx;
		margin-top: 10%;
		margin-left: 20%;
	}

	.passwordsInput {
		width: 48%;
		height: 50rpx;
		margin-top: -7%;
		margin-left: 24%;
		background-color: #f8f8f8;
		font-size: 26rpx;
		padding-left: 2%;
	}

	.passwordInput {
		width: 52%;
		height: 50rpx;
		margin-top: -7%;
		margin-left: 17%;
		background-color: #f8f8f8;
		font-size: 26rpx;
		padding-left: 2%;
	}

	.nameInput {
		width: 50%;
		height: 50rpx;
		margin-top: -7%;
		margin-left: 20%;
		background-color: #f8f8f8;
		font-size: 26rpx;
		padding-left: 2%;
	}

	.passWords {
		margin-top: 8%;
		margin-left: 10%;
	}

	.passWord {
		margin-top: 8%;
		margin-left: 18%;
	}

	.name {
		margin-top: 10%;
		margin-left: 15%;
	}

	.login,
	.regins {
		font-size: 32rpx;
	}

	.app {
		border: 1rpx solid #d1d1d1;
		background-color: #d1d1d1;
		border-radius: 5%;
		height: 500rpx;
		margin-top: 20%;
	}
</style>
