<template>
    <CalculatorScreen :Sum="Sum" :NumberToProcess="NumberToProcess" :Method="Method" :Solved="Solved" />

    <div class="CalculatorMenuFlex">
        <ol class="MainPad">
            <li @click="ChangeSum(Clear)">C</li>
            <li class="WideItem" @click="ChangeSum(ClearEntry)">CE</li>
            <li @click="ChangeSum(item)" v-for="item, index in Keypad" :key="index">
                {{ item }}
            </li>
            <li @click="Calculate(Method)" class="WideItem">=</li>

        </ol>

        <ol class="Operators">
            <li @click="SetMethod(Add)">+</li>
            <li @click="SetMethod(Subtract)">-</li>
            <li @click="SetMethod(Divide)">/</li>
            <li @click="SetMethod(Multiply)">*</li>
        </ol>
    </div>
</template>

<script>
import CalculatorScreen from './CalculatorScreen.vue';




export default {
    name: 'CalculatorComponent',
    components: {
        CalculatorScreen
    },
    setup() {

        return {}
    },
    data() {
        return {
            Keypad: Array(10).fill(0).map((x, i) => i).reverse(),
            Solved: 0,
            Sum: 0,
            NumberToProcess: 0,
            Method: null,
            Clear: "C",
            ClearEntry: "CE",
            Add: "+",
            Subtract: "-",
            Divide: "/",
            Multiply: "*"

        }
    },
    methods: {
        ChangeSum(x) {
            console.log(this.Method)
            console.log(this.NumberToProcess)
            this.Solved = 0
            if (x === "C") {
                this.Sum = 0
                this.NumberToProcess = 0
                this.Method = null
            }
            if (x === "CE") {

                let SumStringed = this.Sum.toString()
                let NumberToProcessStringed = this.NumberToProcess.toString()
                if (SumStringed.length !== 1 && !this.Method) {
                    this.Sum = SumStringed.slice(0, SumStringed.length - 1)
                }
                if (NumberToProcessStringed.length !== 1 && this.Method) {
                    this.NumberToProcess = NumberToProcessStringed.slice(0, NumberToProcessStringed.length - 1)
                }
            }

            if (this.Method) {
                this.NumberToProcess = '' + this.NumberToProcess + x
                this.NumberToProcess = parseInt(this.NumberToProcess)
            }
            else {
                this.Sum = '' + this.Sum + x
                this.Sum = parseInt(this.Sum)
            }

        },

        SetMethod(method) {
            if (this.Solved) {
                this.Sum = this.Solved
            }
            if (this.Method != method) {
                this.Calculate(this.Method)
                this.Method = method
            }
            this.Method = method
        },

        Calculate(method) {

            switch (method) {
                case "+":
                    this.Solved = this.Sum += this.NumberToProcess
                    this.Sum = 0
                    this.NumberToProcess = 0
                    this.Method = null
                    console.log("Solved", this.Solved)
                    break;
                case "-":
                    this.Solved = this.Sum - this.NumberToProcess
                    this.Sum = 0
                    this.NumberToProcess = 0
                    this.Method = null
                    console.log("Solved", this.Solved)
                    break;
                case "/":
                    this.Solved = this.Sum / this.NumberToProcess
                    this.Sum = 0
                    this.NumberToProcess = 0
                    this.Method = null
                    console.log("Solved", this.Solved)
                    break;
                case "*":
                    this.Solved = this.Sum * this.NumberToProcess
                    this.Sum = 0
                    this.NumberToProcess = 0
                    this.Method = null
                    console.log("Solved", this.Solved)
                    break;

                default:
                    break;
            }

        }
    }
}




</script>

<style scoped>
.CalculatorMenuFlex {
    display: flex;
}

.MainPad {
    width: 80%;
    list-style: none;
    display: flex;
    flex-wrap: wrap;
    align-items: center;
    justify-content: space-between;
    gap: 0.5vw;
    font-size: 8vw;
    color: #ffffff;
}

li {
    display: flex;
    align-items: center;
    justify-content: center;
    width: 32.9%;
    aspect-ratio: 1/1;
    background-color: rgb(75, 75, 75);
}

li:active {
    background-color: rgb(128, 140, 150);
    transition: 200ms ease-in-out;
}

.WideItem {
    width: 65.9%;
    aspect-ratio: 2.001/1;

}


.Operators {
    width: 20%;
    list-style: none;
    display: flex;
    flex-direction: column;
    align-items: flex-end;
    justify-content: flex-end;
    gap: 0.5vw;
    font-size: 8vw;
    color: #ffffff;
}

.Operators>li {
    display: flex;
    align-items: center;
    justify-content: center;
    width: 98%;
    height: 19.7%;
    background-color: rgb(75, 75, 75);
}
</style>