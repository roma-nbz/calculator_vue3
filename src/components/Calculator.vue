<script setup>
import { ref } from 'vue'

let previous = ref('')
const result = ref('')

const concatNum = num => {
	previous.value === 0 ? previous.value === num : previous.value += num
}

const concatOp = op => {
	if (previous.value === 0 || previous.value === '.') {
		if (op == '-') {
			previous.value = op
			return
		} else {
			return
		}
	}
	previous.value += op
}

const clear = () => {
	previous.value = ''
	result.value = ''
}

const evaluate = () => {
	result.value = eval(previous.value)
}
</script>

<template>
	<article class="calc">
		<output class="calc__output-result">{{ result || 0 }}</output>
		<output class="calc__output-previous">{{ previous }}</output>
		<div class="calc__main">
			<button @click="clear()" class="calc__btn calc__btn_orange">C</button>
			<button @click="concatOp('/')" class="calc__btn calc__btn_blue">/</button>
			<button @click="concatOp('*')" class="calc__btn calc__btn_blue">*</button>
			<button @click="concatOp('-')" class="calc__btn calc__btn_blue">-</button>
			<button @click="concatNum('7')" class="calc__btn">7</button>
			<button @click="concatNum('8')" class="calc__btn">8</button>
			<button @click="concatNum('9')" class="calc__btn">9</button>
			<button @click="concatOp('+')" class="calc__btn calc__btn_blue">+</button>
			<button @click="concatNum('4')" class="calc__btn">4</button>
			<button @click="concatNum('5')" class="calc__btn">5</button>
			<button @click="concatNum('6')" class="calc__btn">6</button>
			<button @click="concatNum('1')" class="calc__btn">1</button>
			<button @click="concatNum('2')" class="calc__btn">2</button>
			<button @click="concatNum('3')" class="calc__btn">3</button>
			<button @click="evaluate()" class="calc__btn calc__btn_orange">=</button>
			<button @click="concatNum('0')" class="calc__btn">0</button>
			<button @click="concatNum('.')" class="calc__btn">.</button>
		</div>
	</article>
</template>

<style lang="scss" scoped>
.calc {
	padding: 100px 20px 50px;
	background-color: #212121;

	&__output-result {
		width: 345px;
		display: flex;
		justify-content: flex-end;
		overflow: hidden;
		white-space: nowrap;
		font-size: 40px;
		font-weight: 300;
		color: #fff;
		height: 48px;
		margin-bottom: 25px;
	}

	&__output-previous {
		display: flex;
		justify-content: flex-end;
		color: #E1E1E1;
		font-size: 22px;
		font-weight: 400;
		height: 20px;
		margin-bottom: 60px;
	}

	&__main {
		display: grid;
		grid-template-columns: repeat(4, 1fr);
		grid-template-rows: repeat(5, 1fr);
		gap: 20px;
	}

	&__btn {
		width: 70px;
		height: 70px;
		border-radius: 50%;
		background-color: #212121;
		box-shadow: -5px -5px 10px rgba(51, 51, 51, 0.25);
		color: #848484;
		font-size: 40px;
		font-weight: 400;
		text-transform: uppercase;
		border: none;
		cursor: pointer;

		&_orange {
			color: #FFA048;
		}

		&_blue {
			color: #48BDFF;
		}

		&:nth-child(8),
		&:nth-child(15) {
			grid-row: span 2;
			height: 160px;
			border-radius: 40px;
		}

		&:nth-child(16) {
			grid-column: span 2;
			width: 160px;
			border-radius: 40px;
			text-align: start;
			padding-left: 25px;
		}
	}
}
</style>