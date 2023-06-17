<template>
	<view class="home">
		<!-- 头像 -->
		<view class="head">
			<u-avatar :src="src"></u-avatar>
			<view style="margin: 26rpx 0 0 26rpx;">
				登录/注册
			</view>
		</view>
		<!-- 查缴停车费 -->
		<u-card :show-head="false">
			<view class="car-one" slot="body">
				<view class="cell">
					<u-cell-group class="cell-row" :border="false">
						<u-cell-item icon="scan" title="临牌缴费" :arrow="false"></u-cell-item>

					</u-cell-group>
					<u-cell-group class="cell-row" :border="false">
						<u-cell-item icon="file-text" title="缴费说明" :arrow="false"></u-cell-item>
					</u-cell-group>

				</view>

				<view class="carnum">
					<u-form :model="form">
						<view class="f">
							<u-form-item prop="carN">
								<input class="in" :style="{'border-color':this.index==0?'#fab6b6':''}" disabled
									type="text" :value="form.carN[0]" @click="inputClick(0)">
								<input class="in" :style="{'border-color':this.index==1?'#fab6b6':''}" disabled
									type="text" :value="form.carN[1]" @click="inputClick(1)">
								<label style="font-size: 90rpx;">·</label>
								<input class="in" :style="{'border-color':this.index==2?'#fab6b6':''}" disabled
									type="text" :value="form.carN[2]" @click="inputClick(2)">
								<input class="in" :style="{'border-color':this.index==3?'#fab6b6':''}" disabled
									type="text" :value="form.carN[3]" @click="inputClick(3)">
								<input class="in" :style="{'border-color':this.index==4?'#fab6b6':''}" disabled
									type="text" :value="form.carN[4]" @click="inputClick(4)">
								<input class="in" :style="{'border-color':this.index==5?'#fab6b6':''}" disabled
									type="text" :value="form.carN[5]" @click="inputClick(5)">
								<input class="in" :style="{'border-color':this.index==6?'#fab6b6':''}" disabled
									type="text" :value="form.carN[6]" @click="inputClick(6)">
								<input class="in" :style="{'border-color':this.index==7?'#fab6b6':''}" disabled
									type="text" :value="indexaMax>6?form.carN[7]:'+'" @click="inputClick(7)">
							</u-form-item>

						</view>

					</u-form>
					<u-button @click="submit">查缴停车费</u-button>
					<u-keyboard ref="uKeyboard" :show-tips="false" :cancel-btn="false" :mask="false" confirm-text="关闭"
						mode="car" v-model="show" @change="valChange" @backspace="backspace"></u-keyboard>
				</view>


			</view>
		</u-card>
		<!-- 我的车辆 -->
		<u-card :show-head="false">
			<view class="myCar" slot="body">
				<view class="myCar-title">
					<label>我的车辆</label>
					<u-icon name="arrow-right"></u-icon>
				</view>
				<u-button type="info" :custom-style="customStyleButton">添加爱车</u-button>
			</view>
		</u-card>
		<!-- 车辆服务 -->
		<u-card :show-head="false">
			<view class="carServer" slot="body">
				<label :style="{'font-size':'32rpx'}">车场服务</label>
				<view class="">
					<!-- 第一排 -->
					<u-grid :col="4" :border="false">
						<u-grid-item>
							<u-icon name="integral-fill" :size="46"></u-icon>
							<view class="grid-text">会员权益</view>
						</u-grid-item>
						<u-grid-item>
							<u-icon name="file-text-fill" :size="46"></u-icon>
							<view class="grid-text">缴费记录</view>
						</u-grid-item>
						<u-grid-item>
							<u-icon name="red-packet-fill" :size="46"></u-icon>
							<view class="grid-text">停车券</view>
						</u-grid-item>
						<u-grid-item>
							<u-icon name="car-fill" :size="46"></u-icon>
							<view class="grid-text">我的车辆</view>
						</u-grid-item>
					</u-grid>
					<!-- 第二排 -->
					<u-grid :col="4" :border="false">
						<u-grid-item>
							<u-icon name="clock-fill" :size="46"></u-icon>
							<view class="grid-text">预约停车</view>
						</u-grid-item>
						<u-grid-item>
							<u-icon name="map-fill" :size="46"></u-icon>
							<view class="grid-text">智能寻车</view>
						</u-grid-item>
						<u-grid-item>
							<u-icon name="plus-circle" :size="46"></u-icon>
							<view class="grid-text">月卡续费</view>
						</u-grid-item>
						<u-grid-item>
							<u-icon name="rmb-circle-fill" :size="46"></u-icon>
							<view class="grid-text">应急缴费</view>
						</u-grid-item>
					</u-grid>
				</view>
			</view>
		</u-card>

	</view>
</template>

<script>
	export default {
		data() {
			return {
				form: {
					carN: ['粤', 'B', '', '', '', '', '', '']
				},
				show: false,
				index: 0,
				indexaMax: 6,
				carStr: "",
				customStyleButton: {
					width: '200rpx',
					margin: '50rpx 0rpx 0rpx 0rpx'

				},
				src: "../../static/logo.png"
			}
		},
		onLoad() {

		},
		methods: {
			submit() {
				this.carStr = this.form.carN.join('')
				console.log(this.carStr)
			},
			valChange(val) {
				this.$set(this.form.carN, this.index, val)
				if (this.index == this.indexaMax) {
					this.show = false
				}
				this.index += 1

			},
			backspace() {
				let lastIndex = this.indexaMax
				for (; lastIndex >= 0; lastIndex--) {
					if (this.form.carN[lastIndex] != "") {
						break
					}
				}
				if (lastIndex > -1) {
					console.log(lastIndex)
					this.$set(this.form.carN, lastIndex, "")
					this.index = lastIndex
					console.log(this.index)
				}

			},
			inputClick(key) {
				this.show = true
				this.index = key
				if (key == 7) {
					this.indexaMax = 7
				}
			}
		}
	}
</script>

<style lang="scss">
	.home {
		.head {
			margin: 40rpx 0 0 40rpx;
			height: 260rpx;
			// 弹性盒子
			display: flex;
			// 两端对齐
			justify-content: left
		}

		.car-one {
			.cell {
				// 弹性盒子
				display: flex;
				// 两端对齐
				justify-content: space-between
			}

			.carnum {
				.f {
					.in {
						font-size: 42rpx;
						color: $u-main-color;
						flex: 1;
						width: 64rpx;
						height: 84rpx;
						border-radius: 6rpx;
						border: 1px solid $u-form-item-border-color;
						margin: 4rpx;
						text-align: center;
					}
				}
			}
		}

		.myCar {
			.myCar-title {
				// 弹性盒子
				display: flex;
				// 两端对齐
				justify-content: space-between;
				font-size: 32rpx;
			}
		}
	}
</style>