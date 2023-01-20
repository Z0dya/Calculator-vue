<template>
	<div class="container">
		<div class="grid">
			<input @keydown.enter="equal" type="text" v-model="answer" placeholder="0" />
			<button
				@click="clickedPanel(num)"
				class="numbers blocks"
				v-for="num in numbers"
				:key="num + Math.random"
			>
				{{ num }}
			</button>
			<button
				@click="clickedPanel(oper)"
				class="operators blocks"
				v-for="oper in operators"
				:key="oper + Math.random"
			>
				{{ oper }}
			</button>
			<button @click="dot" class="operators blocks">.</button>
			<button @click="reset" class="reset blocks">C</button>
			<button @click="equal" class="equal blocks">=</button>
		</div>
	</div>
</template>

<script>
export default {
	data() {
		return {
			numbers: ['1', '2', '3', '4', '5', '6', '7', '8', '9', '0'],
			operators: ['+', '-', '*', '/', '%'],
			answer: '',
			resetNum: false,
			dotEnable: true
		};
	},
	methods: {
		// функция сброса значений (C)
		reset() {
			this.answer = '';
		},
		// функция подсчета (=)
		equal() {
			// если результат содержит %, то убираем его и делим введеные цифры на 100
			if (this.answer.includes('%')) {
				this.answer = this.answer.replace('%', '');
				this.answer = this.answer / 100;
				this.resetNum = true;
			}
			// иначе, считаем результат встроенной функцией eval и переводим переменную resetNum в true
			else {
				this.answer = eval(this.answer);
				this.resetNum = true;
			}
		},
		dot() {
			// если длинна больше 0 И не содержит точку то добавляем точку
			// if (this.answer.length > 0 && !this.answer.includes('.')) {
			//     this.answer = this.answer + '.';
			// }
			if (this.answer.length > 0 && this.dotEnable) {
				this.answer = this.answer + '.';
				this.dotEnable = false;
			}
		},
		// функция нажатия на кнопки
		clickedPanel(num) {
			// если true то очищаем результат и переводим переменную в false
			if (this.resetNum) {
				this.answer = '';
				this.resetNum = false;
				return;
			}
			if (this.answer.includes('%')) {
				this.equal();
				return;
			}
			// если 1 символ равен любому из операторов, то очищаем оператор и добавляем нажатую цифру
			if (['+', '-', '*', '/', '%', '.'].includes(this.answer[0])) {
				this.answer = '' + num;
				return;
			}
      if (this.answer.match(/[\+\-\*\/]/gm)?.length > 0) {
				this.dotEnable = true;
			}
			// если операторов больше 0 и операторы содержат строку то вызываем функцию подсчета (чтобы нельзя было вводить больше 1 оператора)
			if (this.answer.match(/[\+\-\*\/]/gm)?.length > 0 && this.operators.includes(num)) {
				this.equal();
        return;
			}
			// иначе результат равен результат + нажатая кнопка (нажали 2 = 2, нажали 6 = 26)
			this.answer = this.answer + num;
		}
	}
};
</script>

<style scoped lang="scss">
.container {
	display: flex;
	justify-content: center;
	align-items: center;
	width: 100%;
	height: 100%;
	.grid {
		display: grid;
		grid-template-columns: repeat(3, 1fr);
		grid-template-rows: repeat(6, 1fr);
		width: 1fr;
		input {
			width: 300px;
			grid-column: 1/4;
			font-size: 30px;
		}
		.blocks {
			font-size: 50px;
			width: 100%;
			border: 0;
			cursor: pointer;
			transition: all 0.2s ease;
			border: 1px solid #2f2f2f;
		}
		.numbers {
			background-color: #3f3f3f;
			color: #fff;
		}
		.numbers:hover {
			background-color: #707070;
		}
		.operators {
			background-color: #ff9900;
		}
		.operators:hover {
			background-color: #feca7c;
		}
		.reset,
		.equal {
			background-color: rgb(169, 169, 169);
		}
		.reset:hover,
		.equal:hover {
			background-color: rgb(101, 101, 101);
		}
		.reset {
			grid-column: 2/4;
		}
		.equal {
			grid-column: 1/4;
		}
	}
}
</style>
