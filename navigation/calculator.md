---
layout: post
type: hacks
title: Calculator
search_exclude: true
permalink: /calculator/
---



<!-- f0f0f0 -->
<style>
    body {
        display: flex;
        justify-content: center;
        align-items: center;
        height: 100vh;
        margin: 80px;
        background-color: #f0f0f0;
        font-family: Arial, sans-serif;
    }

    .calculator {
        border: 1px solid #ccc;
        border-radius: 10px;
        box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
        overflow: hidden;
    }

    #display {
        width: 100%;
        padding: 20px;
        border: none;
        background-color: #222;
        color: #000;
        font-size: 2em;
        text-align: right;
        box-sizing: border-box;
    }

    .buttons {
        display: grid;
        grid-template-columns: repeat(4, 1fr);
        gap: 1px;
    }

    .btn {
        padding: 20px;
        background-color: #000;
        border: none;
        font-size: 1.5em;
        cursor: pointer;
        transition: background-color 0.3s;
    }

    .btn:hover {
        background-color: #008000;
    }

    .operator {
        background-color: #88E788;
    }

    .operator:hover {
        background-color: #ddd;
    }

    .equal {
        background-color: #4CAF50;
        color: white;
        grid-column: span 4;
    }

    .equal:hover {
        background-color: #45a049;
    }

    .clear {
        background-color: #f44336;
        color: white;
        grid-column: span 4;
    }

    .clear:hover {
        background-color: #e53935;
    }
</style>


<body>
    <div class="calculator">
        <input type="text" id="display" disabled>
        <div class="buttons">
            <button class="btn" onclick="appendNumber('7')">7</button>
            <button class="btn" onclick="appendNumber('8')">8</button>
            <button class="btn" onclick="appendNumber('9')">9</button>
            <button class="btn operator" onclick="appendOperator('/')">/</button>
            <button class="btn" onclick="appendNumber('4')">4</button>
            <button class="btn" onclick="appendNumber('5')">5</button>
            <button class="btn" onclick="appendNumber('6')">6</button>
            <button class="btn operator" onclick="appendOperator('*')">*</button>
            <button class="btn" onclick="appendNumber('1')">1</button>
            <button class="btn" onclick="appendNumber('2')">2</button>
            <button class="btn" onclick="appendNumber('3')">3</button>
            <button class="btn operator" onclick="appendOperator('-')">-</button>
            <button class="btn" onclick="appendNumber('0')">0</button>
            <button class="btn" onclick="appendNumber('.')">.</button>
            <button class="btn operator" onclick="appendOperator('+')">+</button>
            <button class="btn equal" onclick="calculate()">=</button>
            <button class="btn clear" onclick="clearDisplay()">C</button>
        </div>
    </div>
    <script>
        let display = document.getElementById('display');
        let currentInput = '';
        let operator = '';
        let previousInput = '';
        function appendNumber(number) {
            currentInput += number;
            display.value = currentInput;
        }
        function appendOperator(op) {
            if (currentInput === '') return;
            if (previousInput !== '') {
                calculate();
            }
            operator = op;
            previousInput = currentInput;
            currentInput = '';
        }
        function calculate() {
            if (previousInput === '' || currentInput === '') return;
            let result;
            const prev = parseFloat(previousInput);
            const current = parseFloat(currentInput);            
            switch (operator) {
                case '+':
                    result = prev + current;
                    break;
                case '-':
                    result = prev - current;
                    break;
                case '*':
                    result = prev * current;
                    break;
                case '/':
                    if (current === 0) {
                        alert('Cannot divide by zero');
                        clearDisplay();
                        return;
                    }
                    result = prev / current;
                    break;
                default:
                    return;
            }            
            display.value = result;
            previousInput = '';
            currentInput = result.toString();
        }
        function clearDisplay() {
            display.value = '';
            currentInput = '';
            previousInput = '';
            operator = '';
        }
    </script>
</body>