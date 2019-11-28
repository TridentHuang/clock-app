<template>
	<view>
		<uni-card :title="activity.name" v-for="(activity,index) in activities" note="true" :key="index">
			<view class="users">
				<view class="user" v-for="(item,index) in activity.list" :key="index">{{item.nickName}}</view>
				<view class="user">...</view>
			</view>
			<template v-slot:footer>
				<button type="primary" class="share" open-type="share" size="mini">分享</button>
			</template>
		</uni-card>
		<button type="primary" @click="share">分享测试</button>
	</view>
</template>

<script>
	import url from '@/common/config.js'
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
				path: '/pages/share/record/record'
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
					} else {
						console.log("未授权")
					}
				}
			})
		},
		data() {
			return {
				activities: []
			}
		},
		methods: {
			share() {
				wx.navigateTo({
					url: '/pages/share/record/record'
				})
			}
		},
		onLoad() {
			console.log("进来了")
			uni.request({
				url: url + '/activity/getAll/1',
				method: 'GET',
				success: res => {
					console.log(res.data)
					this.activities = res.data.data;
				},
			});
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
