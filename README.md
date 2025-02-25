<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>ZaalKalkulator</title>
    <style>
        /* Tema Dasar (Light Mode) */
        :root {
            --background-color: #f4f4f4;
            --calculator-bg: #ffffff;
            --display-bg: #e0e0e0;
            --display-text: #333333;
            --button-bg: #f0f0f0;
            --button-text: #333333;
            --button-hover: #d0d0d0;
            --operator-bg: #a8d5ba;
            --operator-hover: #8cc2a1;
            --equal-bg: #34c759;
            --equal-hover: #30d158;
            --clear-bg: #ff3b30;
            --clear-hover: #ff5a50;
            --backspace-bg: #a8d5ba; /* Warna hijau seperti operator */
            --backspace-hover: #8cc2a1; /* Warna hover hijau */
            --history-bg: #ffffff;
            --history-text: #333333;
        }

        /* Tema Gelap (Dark Mode) */
        [data-theme="dark"] {
            --background-color: #333333;
            --calculator-bg: #444444;
            --display-bg: #555555;
            --display-text: #ffffff;
            --button-bg: #666666;
            --button-text: #ffffff;
            --button-hover: #777777;
            --operator-bg: #6a9c7d;
            --operator-hover: #5a8c6d;
            --equal-bg: #2a9d3e;
            --equal-hover: #258c35;
            --clear-bg: #d32f2f;
            --clear-hover: #c62828;
            --backspace-bg: #6a9c7d; /* Warna hijau seperti operator */
            --backspace-hover: #5a8c6d; /* Warna hover hijau */
            --history-bg: #444444;
            --history-text: #ffffff;
        }

        body {
            font-family: Arial, sans-serif;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            background-color: var(--background-color);
            margin: 0;
            transition: background-color 0.3s;
        }

        .container {
            display: flex;
            gap: 20px;
        }

        .calculator {
            background-color: var(--calculator-bg);
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0px 0px 10px rgba(0, 0, 0, 0.1);
            transition: background-color 0.3s;
        }

        .calculator input[type="text"] {
            width: 100%;
            height: 50px;
            background-color: var(--display-bg);
            border: none;
            color: var(--display-text);
            text-align: right;
            padding: 10px;
            font-size: 24px;
            border-radius: 5px;
            margin-bottom: 10px;
            box-sizing: border-box;
            transition: background-color 0.3s, color 0.3s;
        }

        .calculator .buttons {
            display: grid;
            grid-template-columns: repeat(4, 1fr);
            gap: 10px;
        }

        .calculator .buttons button {
            background-color: var(--button-bg);
            border: none;
            color: var(--button-text);
            padding: 20px;
            font-size: 18px;
            border-radius: 5px;
            cursor: pointer;
            transition: background-color 0.3s, color 0.3s;
        }

        .calculator .buttons button:hover {
            background-color: var(--button-hover);
        }

        .calculator .buttons button.operator {
            background-color: var(--operator-bg);
        }

        .calculator .buttons button.operator:hover {
            background-color: var(--operator-hover);
        }

        .calculator .buttons button.equal {
            background-color: var(--equal-bg);
            grid-column: span 2;
        }

        .calculator .buttons button.equal:hover {
            background-color: var(--equal-hover);
        }

        .calculator .buttons button.clear {
            background-color: var(--clear-bg);
            grid-column: span 2;
        }

        .calculator .buttons button.clear:hover {
            background-color: var(--clear-hover);
        }

        .calculator .buttons button.backspace {
            background-color: var(--backspace-bg);
            font-size: 20px;
        }

        .calculator .buttons button.backspace:hover {
            background-color: var(--backspace-hover);
        }

        .history {
            background-color: var(--history-bg);
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0px 0px 10px rgba(0, 0, 0, 0.1);
            width: 200px;
            max-height: 400px;
            overflow-y: auto;
            transition: background-color 0.3s, color 0.3s;
        }

        .history h3 {
            margin-top: 0;
            color: var(--history-text);
        }

        .history ul {
            list-style-type: none;
            padding: 0;
            margin: 0;
        }

        .history ul li {
            padding: 5px 0;
            color: var(--history-text);
            border-bottom: 1px solid var(--display-bg);
        }

        .history ul li:last-child {
            border-bottom: none;
        }

        .theme-switcher {
            position: absolute;
            top: 20px;
            right: 20px;
        }

        .theme-switcher button {
            background-color: var(--button-bg);
            border: none;
            color: var(--button-text);
            padding: 10px;
            font-size: 24px;
            border-radius: 50%;
            width: 50px;
            height: 50px;
            cursor: pointer;
            display: flex;
            justify-content: center;
            align-items: center;
            transition: background-color 0.3s, color 0.3s;
        }

        .theme-switcher button:hover {
            background-color: var(--button-hover);
        }
    </style>
</head>
<body>

<div class="theme-switcher">
    <button onclick="toggleTheme()">☀️</button>
</div>

<div class="container">
    <div class="calculator">
        <input type="text" id="display" disabled>
        <div class="buttons">
            <button onclick="clearDisplay()" class="clear">C</button>
            <button onclick="backspace()" class="backspace">←</button>
            <button onclick="appendToDisplay('÷')" class="operator">÷</button>
            <button onclick="appendToDisplay('x')" class="operator">x</button>
            <button onclick="appendToDisplay('7')">7</button>
            <button onclick="appendToDisplay('8')">8</button>
            <button onclick="appendToDisplay('9')">9</button>
            <button onclick="appendToDisplay('-')" class="operator">-</button>
            <button onclick="appendToDisplay('4')">4</button>
            <button onclick="appendToDisplay('5')">5</button>
            <button onclick="appendToDisplay('6')">6</button>
            <button onclick="appendToDisplay('+')" class="operator">+</button>
            <button onclick="appendToDisplay('1')">1</button>
            <button onclick="appendToDisplay('2')">2</button>
            <button onclick="appendToDisplay('3')">3</button>
            <button onclick="calculate()" class="equal">=</button>
            <button onclick="appendToDisplay('0')">0</button>
            <button onclick="appendToDisplay('.')">.</button>
        </div>
    </div>

    <div class="history">
        <h3>History</h3>
        <ul id="history-list"></ul>
        <button onclick="clearHistory()" style="width: 100%; padding: 10px; margin-top: 10px; background-color: var(--clear-bg); color: white; border: none; border-radius: 5px; cursor: pointer;">Clear History</button>
    </div>
</div>

<script>
    // Fungsi untuk menambahkan nilai ke layar
    function appendToDisplay(value) {
        document.getElementById('display').value += value;
    }

    // Fungsi untuk menghapus layar
    function clearDisplay() {
        document.getElementById('display').value = '';
    }

    // Fungsi untuk menghapus satu karakter terakhir (backspace)
    function backspace() {
        const display = document.getElementById('display');
        display.value = display.value.slice(0, -1);
    }

    // Fungsi untuk melakukan perhitungan
    function calculate() {
        const display = document.getElementById('display');
        let expression = display.value;

        // Ganti simbol 'x' dengan '*' dan '÷' dengan '/' untuk perhitungan
        const calculationExpression = expression.replace(/x/g, '*').replace(/÷/g, '/');

        try {
            const result = eval(calculationExpression);
            // Format hasil dengan simbol 'x' dan '÷'
            const formattedResult = result.toString().replace(/\*/g, 'x').replace(/\//g, '÷');
            display.value = formattedResult;

            // Format history dengan simbol 'x' dan '÷'
            const formattedHistory = expression + ' = ' + formattedResult;
            addToHistory(formattedHistory);
        } catch (error) {
            display.value = 'Error';
        }
    }

    // Fungsi untuk menambahkan history
    function addToHistory(entry) {
        const historyList = document.getElementById('history-list');
        const li = document.createElement('li');
        li.textContent = entry;
        historyList.appendChild(li);

        // Simpan history ke localStorage
        const history = JSON.parse(localStorage.getItem('calculatorHistory') || '[]');
        history.push(entry);
        localStorage.setItem('calculatorHistory', JSON.stringify(history));
    }

    // Fungsi untuk memuat history dari localStorage
    function loadHistory() {
        const historyList = document.getElementById('history-list');
        const history = JSON.parse(localStorage.getItem('calculatorHistory') || '[]');
        history.forEach(entry => {
            const li = document.createElement('li');
            li.textContent = entry;
            historyList.appendChild(li);
        });
    }

    // Fungsi untuk menghapus history
    function clearHistory() {
        const historyList = document.getElementById('history-list');
        historyList.innerHTML = '';
        localStorage.removeItem('calculatorHistory');
    }

    // Fungsi untuk mengubah tema
    function toggleTheme() {
        const body = document.body;
        const themeButton = document.querySelector('.theme-switcher button');

        if (body.getAttribute('data-theme') === 'dark') {
            body.removeAttribute('data-theme');
            themeButton.textContent = '☀️'; // Emoji matahari untuk mode terang
        } else {
            body.setAttribute('data-theme', 'dark');
            themeButton.textContent = '🌙'; // Emoji bulan untuk mode gelap
        }
    }

    // Memuat history saat halaman dimuat
    window.onload = loadHistory;
</script>

</body>
</html>
