# kalkulatorsesat<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Kalkulator Unik</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
            background-color: #f5f5f5;
        }
        
        .calculator {
            background-color: #333;
            border-radius: 10px;
            padding: 20px;
            width: 300px;
            box-shadow: 0 10px 20px rgba(0, 0, 0, 0.3);
        }
        
        .display {
            background-color: #e0e0e0;
            height: 60px;
            margin-bottom: 15px;
            border-radius: 5px;
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 0 10px;
            font-size: 24px;
            overflow: hidden;
            color: red;
            font-weight: bold;
        }
        
        .buttons {
            display: grid;
            grid-template-columns: repeat(4, 1fr);
            grid-gap: 10px;
        }
        
        button {
            height: 50px;
            font-size: 20px;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            transition: background-color 0.2s;
        }
        
        button:hover {
            opacity: 0.8;
        }
        
        .number {
            background-color: #505050;
            color: white;
        }
        
        .operator {
            background-color: #ff9500;
            color: white;
        }
        
        .equal {
            background-color: #ff3b30;
            color: white;
        }
        
        .clear {
            background-color: #a5a5a5;
        }
        
        #kontol-message {
            color: red;
            font-size: 24px;
            text-align: center;
            margin-top: 15px;
            font-weight: bold;
            height: 30px;
            display: none;
        }
    </style>
</head>
<body>
    <div class="calculator">
        <div class="display" id="display">0</div>
        <div class="buttons">
            <button class="clear" onclick="clearDisplay()">C</button>
            <button class="operator" onclick="appendOperator('/')">/</button>
            <button class="operator" onclick="appendOperator('*')">*</button>
            <button class="operator" onclick="appendOperator('-')">-</button>
            
            <button class="number" onclick="appendNumber('7')">7</button>
            <button class="number" onclick="appendNumber('8')">8</button>
            <button class="number" onclick="appendNumber('9')">9</button>
            <button class="operator" onclick="appendOperator('+')">+</button>
            
            <button class="number" onclick="appendNumber('4')">4</button>
            <button class="number" onclick="appendNumber('5')">5</button>
            <button class="number" onclick="appendNumber('6')">6</button>
            <button class="number" onclick="appendNumber('1')">1</button>
            
            <button class="number" onclick="appendNumber('2')">2</button>
            <button class="number" onclick="appendNumber('3')">3</button>
            <button class="number" onclick="appendNumber('0')">0</button>
            <button class="equal" onclick="calculate()">=</button>
        </div>
        <div id="kontol-message"></div>
    </div>

    <script>
        let currentInput = '0';
        let previousInput = '';
        let operation = null;
        let resetScreen = false;
        const display = document.getElementById('display');
        const kontolMessage = document.getElementById('kontol-message');

        function appendNumber(number) {
            if (currentInput === '0' || resetScreen) {
                currentInput = number;
                resetScreen = false;
            } else {
                currentInput += number;
            }
            updateDisplay();
        }

        function appendOperator(op) {
            if (operation !== null) calculate();
            previousInput = currentInput;
            operation = op;
            resetScreen = true;
        }

        function clearDisplay() {
            currentInput = '0';
            previousInput = '';
            operation = null;
            updateDisplay();
            kontolMessage.style.display = 'none';
        }

        function updateDisplay() {
            display.textContent = currentInput;
        }

        function calculate() {
            let result;
            const prev = parseFloat(previousInput);
            const current = parseFloat(currentInput);
            
            if (isNaN(prev) || isNaN(current)) return;
            
            switch (operation) {
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
                    result = prev / current;
                    break;
                default:
                    return;
            }
            
            // Always show KONTOL as the answer
            currentInput = 'KONTOL';
            operation = null;
            updateDisplay();
            
            // No need for separate message, we show in the display
            kontolMessage.style.display = 'none';
        }
    </script>
</body>
</html>

