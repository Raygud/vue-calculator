# vue-calculator

[Live site!](https://vue-calculator-orpin.vercel.app/)

styled for mobile only due to time constraints.


## initial thoughts on Vue.js

I am impressed with Vue and have not missed any features from React. I appreciate its built-in functionalities and the ease of styling, which reminds me of Styled Components in React.


## Notes
.1 Should have gone with display grid instead of flex, had some issues and had to use a hacky fix with aspect ratio.
.2 Bug when choosing a new operator without getting the sum of the first calculation(e.g. returns -4 when it should return 4)

## Code

#### Changing displayed number

```
ChangeSum(x) {
            console.log(this.Method)
            console.log(this.NumberToProcess)
            if (x === "C") {
                this.Sum = 0
                this.NumberToProcess = 0
                this.Method = null
                this.Solved = 0
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
                this.Solved = 0
            }
        },
```

If the parameter is 'C', clear everything. If the parameter is 'CE', remove only the last index. Check if a method is set. If true, change the value of the second number. Otherwise, add to the first number.

### Changing method(+,-,/,x)

```
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
```

Update 'Sum(Starting number)' with the value of the previous calculation if one exists. If the selected method differs from the current method clicked, solve the initial calculation and apply the new method using the result.

### Calculating 

```
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
```

Calculate the result of the two provided numbers using the provided method, and reset all values leaving only Solved(the return value of the provided function)

### Screen

```
 <div>

        {{ Solved? null: Sum }}


        {{ Solved? Solved: null }}


        {{ Method }}

        {{ NumberToProcess? NumberToProcess: null }}

    </div>
```

if there is a solved value display that if not display the current number the user is editing(Sum) if a second number exists(NumberToProcess) display that.


