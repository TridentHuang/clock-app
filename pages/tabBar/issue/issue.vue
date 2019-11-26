<template>
	<view class="clock-issue">
		<form @submit="formSubmit">
			<view class="issue">
				<input type="text" name="name" class="item" placeholder="请输入名称" />
				<picker mode="multiSelector" class="item" name="arrayIndex" :value='arrayIndex' :range="array" @change="changeEndTime">
					<view>
						<text class="endTimeTitle">打卡截止时间 </text>
						<text class="endTime">
							{{array[0][arrayIndex[0]]}}{{array[1][arrayIndex[1]]}}
						</text>
					</view>
				</picker>
			</view>
			<uni-card title="说明">
				<view class="des">
					🌟 发布活动后发链接邀请成员，成员成功加入活动后即可开始每天学习打卡
				</view>
				<view class="des">
					🌟 打卡截止时间：指每日最迟打卡时间，如当日23:00或者次日02:00，可点击选择
				</view>
			</uni-card>
			<view class="publish">
				<button type="primary" form-type="submit" class="btn">发布</button>
			</view>
		</form>
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
		data() {
			return {
				name: '',
				arrayIndex: [1, 0],
				array: [
					['当日', '次日'],
					['00:00', '01:00', '02:00', '03:00', '04:00', '05:00',
						'06:00', '07:00', '08:00', '09:00', '10:00', '11:00',
						'12:00', '13:00', '14:00', '15:00', '16:00', '17:00',
						'18:00', '19:00', '20:00', '21:00', '22:00', '23:00'
					]
				]
			}
		},
		methods: {
			changeEndTime(e) {
				console.log(e.detail.value)
				this.arrayIndex = e.detail.value;
			},
			formSubmit(e) {
				let items = e.detail.value
				let name = items.name;
				let endTime = this.array[0][this.arrayIndex[0]] + this.array[1][this.arrayIndex[1]]
				uni.request({
					url: 'http://localhost:8080/activity/issue',
					method: 'POST',
					data: {
						name:name,
						endTime:endTime
					}
				});
			}
		}
	}
</script>

<style>
	.clock-issue {
		position: relative;
		height: 94vh;
	}

	.issue {
		width: 92%;
		margin: 10upx auto;
	}

	.item {
		margin: 60upx 0;
		border-bottom: 4upx solid #008000;
	}

	.user {
		background-color: green;
		color: white;
		padding: 5upx 20upx;
		border-radius: 10upx;
	}

	.publish {
		width: 100%;
		bottom: 20upx;
		position: absolute;
	}

	.btn {
		width: 98%;
		margin: 0 auto;
	}

	.des {
		color: #8F8F94;
		font-size: 30upx;
	}

	.endTimeTitle {
		color: #808080;
	}

	.endTime {
		margin-left: 20upx;
	}
</style>
