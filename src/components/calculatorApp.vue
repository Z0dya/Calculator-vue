<template>
    <div class="grid">
        <input type="text" v-model="answer" placeholder="0" />
        <button @click="clickedPanel(num)" class="numbers blocks" v-for="num in numbers" :key="num + Math.random">
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
        <button @click="reset" class="reset blocks">C</button>
        <button @click="equal" class="equal blocks">=</button>
    </div>
</template>

<script>
export default {
    data() {
        return {
            numbers: ['1', '2', '3', '4', '5', '6', '7', '8', '9', '0'],
            operators: ['+', '-', '*', '/', '%'],
            answer: '',
        };
    },
    methods: {
        reset() {
            this.answer = '';
        },
        equal() {
            this.answer = eval(this.answer);
        },
        clickedPanel(num) {
            if (this.answer.match(/[\+\-\*\/]/gm)?.length > 0 && this.operators.includes(num)) {
                this.equal();
            } else {
                this.answer = this.answer + num;
            }
        },
    },
};
</script>

<style scoped lang="scss">
.grid {
    display: flex;
    width: 150px;
    flex-wrap: wrap;
    input {
        width: 100%;
    }
    .blocks {
        font-size: 30px;
        width: 50px;
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
        background-color: #ffbf60;
    }
    .reset,
    .equal {
        background-color: rgb(169, 169, 169);
    }
    .reset:hover,
    .equal:hover {
        background-color: rgb(101, 101, 101);
    }
}
</style>
