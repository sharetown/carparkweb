<template>
	<view class="car-input">
		<u-form :model="car">
			<!-- 车牌号输入框 -->
			<u-form-item prop="carNumber">
				<u-input class="child" disabled typt="text" border placeholder="" :value="car.carNumber[0]"
					@click="inputClick(0)" :border-color="index==0?'#DB005B	':''"></u-input>
				<u-input class="child" disabled typt="text" border placeholder="" :value="car.carNumber[1]"
					@click="inputClick(1)" :border-color="index==1?'#DB005B	':''"></u-input>
				<label style="font-size: 90rpx">·</label>
				<u-input class="child" disabled typt="text" border placeholder="" :value="car.carNumber[2]"
					@click="inputClick(2)" :border-color="index==2?'#DB005B	':''"></u-input>
				<u-input class="child" disabled typt="text" border placeholder="" :value="car.carNumber[3]"
					@click="inputClick(3)" :border-color="index==3?'#DB005B	':''"></u-input>
				<u-input class="child" disabled typt="text" border placeholder="" :value="car.carNumber[4]"
					@click="inputClick(4)" :border-color="index==4?'#DB005B	':''"></u-input>
				<u-input class="child" disabled typt="text" border placeholder="" :value="car.carNumber[5]"
					@click="inputClick(5)" :border-color="index==5?'#DB005B	':''"></u-input>
				<u-input class="child" disabled typt="text" border placeholder="" :value="car.carNumber[6]"
					@click="inputClick(6)" :border-color="index==6?'#DB005B	':''"></u-input>
				<u-input class="child" disabled typt="text" border placeholder=""
					:value="indexMax>6?car.carNumber[7]:'+'" @click="inputClick(7)"
					:border-color="index==7?'#DB005B':''"></u-input>
			</u-form-item>
			<!-- 提交按钮 -->
			<u-button @click="submit">{{submitName}}</u-button>
			<!-- 车牌号键盘 -->
			<u-keyboard ref="uKeyboard" :show-tips="false" :cancel-btn="false" :mask="false" confirm-text="关闭"
				mode="car" v-model="showCarKeyboard" @change="valChange" @backspace="backspace"></u-keyboard>
		</u-form>

	</view>
</template>

<script>
	export default {
		data() {
			return {
				showCarKeyboard: false, // 是否显示车牌号键盘
				//车牌号信息
				car: {
					carNumber: ['粤', 'B', '', '', '', '', '', ''],
					carNumStr: "",
				},
				//输入框下标
				index: 0,
				//区分燃油车格式和新能源车格式
				indexMax: 6,
				//按钮文本
				submitName: "查缴停车费"

			};
		},
		methods: {
			//输入车牌号后提交按钮方法
			submit() {
				//处理凭借成字符串，最终返回给后端
				this.car.carNumStr = this.car.carNumber.join('')
			},
			//车牌号键盘点击内容事件
			valChange(val) {
				//每次点击设置车牌号数组对应下标的值
				this.$set(this.car.carNumber, this.index, val)
				//限制车牌号长度
				if (this.index == this.indexMax) {
					this.showCarKeyboard = false
				}
				//下标自增
				this.index += 1

			},
			//车牌号回退键事件
			backspace() {
				//删除后重新限制最大输入长度
				if (this.indexMax == 7) {
					this.indexMax = 6
				}

				//计算最后一个不为空的元素的下标
				let lastIndex = this.indexMax
				for (; lastIndex >= 0; lastIndex--) {
					if (this.car.carNumber[lastIndex] != "") {
						break
					}
				}
				//自动从最后一个下标处开始删
				if (lastIndex > -1) {
					this.$set(this.car.carNumber, lastIndex, "")
					this.index = lastIndex
				} else {
					this.index = 0
				}

			},
			//输入框点击时
			inputClick(key) {
				//显示车牌号键盘
				this.showCarKeyboard = true
				//设置下标为当前点击的输入框
				this.index = key
				//如果点击‘+’号说明是新能源车，开放最后一位输入框
				if (key == 7) {
					this.indexMax = 7
				}
			}
		}
	}
</script>

<style lang="scss">
	.car-input {
		display: flex;
		justify-content: space-between;

		::v-deep .child {
			margin: 4rpx;

			input {

				width: 38rpx;
				height: 98rpx;
				font-size: 38rpx;
			}
		}
	}
</style>