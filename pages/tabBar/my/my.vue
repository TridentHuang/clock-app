<template>
	<view>
		<uni-card :title="activity.name" v-for="activity in activities" note="true">
			<view class="users">
				<view class="user" v-for="item in activity.users">{{item.name}}</view>
				<view class="user">...</view>
			</view>
			<template v-slot:footer>
				<button type="primary" class="share" open-type="share" size="mini">分享</button>
			</template>
		</uni-card>
	</view>
</template>

<script>
	import {
		uniCard
	} from '@dcloudio/uni-ui'
	export default {
		components: {
			uniCard
		},
		onShareAppMessage(res) {
			return {
				title: '微信小程序测试分享',
				path: '/pages/tabBar/issue/issue'
			}
		},
		onLoad: function() {
			// 查看是否授权
			wx.getSetting({
				success: function(res) {
					console.log("res:" + res);
					if (res.authSetting['scope.userInfo']) {
						// 已经授权，可以直接调用 getUserInfo 获取头像昵称
						wx.getUserInfo({
							success: function(res) {
								console.log(res.userInfo)
							}
						})
					}else{
						console.log("未授权")
					}
				}
			})
		},
		data() {
			return {
				activities: [{
					name: "百词斩",
					users: [{
							name: '张三'
						},
						{
							name: '李四'
						},
						{
							name: '李四'
						},
						{
							name: '李四'
						},
						{
							name: '李四'
						}
					]
				}, {
					name: "流利说",
					users: [{
							name: '张三'
						},
						{
							name: '李四'
						},
						{
							name: '李四'
						},
						{
							name: '李四'
						},
						{
							name: '李四'
						}
					]
				}, {
					name: "流利说",
					users: [{
							name: '张三'
						},
						{
							name: '李四'
						},
						{
							name: '李四'
						},
						{
							name: '李四'
						},
						{
							name: '李四'
						}
					]
				}, {
					name: "流利说",
					users: [{
							name: '张三'
						},
						{
							name: '李四'
						},
						{
							name: '李四'
						},
						{
							name: '李四'
						},
						{
							name: '李四'
						}
					]
				}]

			}
		},
		methods: {

		}
	}
</script>

<style>
	.users {
		display: flex;
		flex-wrap: wrap;
	}

	.user {
		background-color: #008000;
		color: white;
		padding: 5upx 20upx;
		border-radius: 10upx;
		margin: 20upx 20upx;
	}

	.share {
		float: right;
	}
</style>
