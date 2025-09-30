# moderncalculator
//A modern calculator doing all the basic arithmatic operations storing history of last 5 calculations with dark and light theme changing button//
<br>
Author-InfinitezenCODER & mishra234ansumaan
<!DOCTYPE html>
<html lang="en" class="">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Themeable Calculator</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;700&display=swap" rel="stylesheet">
    <style>
        /* Custom styles for better aesthetics */
        body {
            font-family: 'Inter', sans-serif;
            -webkit-tap-highlight-color: transparent; /* Disable tap highlight on mobile */
        }
        .calculator-grid {
            display: grid;
            grid-template-columns: repeat(4, 1fr);
            gap: 1rem;
        }
        .btn {
            transition: all 0.2s ease-in-out;
        }
        .btn:active {
            transform: scale(0.95);
        }
        /* Scrollbar styling for history */
        #history-list::-webkit-scrollbar {
            width: 6px;
        }
        #history-list::-webkit-scrollbar-track {
            background: transparent;
        }
        #history-list::-webkit-scrollbar-thumb {
            background-color: #4a5568; /* dark:bg-gray-700 */
            border-radius: 20px;
        }
        html.dark #history-list::-webkit-scrollbar-thumb {
             background-color: #718096; /* dark:bg-gray-500 */
        }
    </style>
    <script>
        // Configuration for Tailwind dark mode
        tailwind.config = {
            darkMode: 'class',
        }
    </script>
</head>
<body class="bg-gray-100 dark:bg-gray-900 text-gray-900 dark:text-gray-100 flex items-center justify-center min-h-screen p-4 transition-colors duration-300">

    <div class="w-full max-w-md mx-auto">
        <!-- Calculator Body -->
        <div class="bg-white dark:bg-black rounded-3xl shadow-2xl p-6">
            <!-- Header: Theme Toggle -->
            <div class="flex justify-between items-center mb-6">
                <h1 class="text-xl font-bold text-gray-500 dark:text-gray-400">Calculator</h1>
                <button id="theme-toggle" class="p-2 rounded-full bg-gray-200 dark:bg-gray-700 hover:bg-gray-300 dark:hover:bg-gray-600 transition-colors">
                    <svg id="theme-icon-light" class="w-6 h-6 text-yellow-500" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 3v1m0 16v1m9-9h-1M4 12H3m15.364 6.364l-.707-.707M6.343 6.343l-.707-.707m12.728 0l-.707.707M6.343 17.657l-.707.707M16 12a4 4 0 11-8 0 4 4 0 018 0z"></path></svg>
                    <svg id="theme-icon-dark" class="w-6 h-6 text-blue-300 hidden" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M20.354 15.354A9 9 0 018.646 3.646 9.003 9.003 0 0012 21a9.003 9.003 0 008.354-5.646z"></path></svg>
                </button>
            </div>

            <!-- Display Screen -->
            <div class="bg-gray-100 dark:bg-gray-800 rounded-2xl p-6 mb-6 text-right break-words">
                <div id="expression" class="text-gray-500 dark:text-gray-400 text-xl h-7">&nbsp;</div>
                <div id="display" class="text-5xl font-bold h-14">0</div>
            </div>

            <!-- Buttons Grid -->
            <div class="calculator-grid">
                <!-- Row 1 -->
                <button data-value="clear" class="btn text-2xl font-semibold bg-gray-200 dark:bg-gray-700 text-orange-500 dark:text-orange-400 p-4 rounded-2xl">C</button>
                <button data-value="backspace" class="btn text-2xl font-semibold bg-gray-200 dark:bg-gray-700 text-orange-500 dark:text-orange-400 p-4 rounded-2xl">⌫</button>
                <button data-value="%" class="btn text-2xl font-semibold bg-white dark:bg-gray-700 text-black dark:text-white border-2 border-gray-200 dark:border-gray-600 p-4 rounded-2xl">%</button>
                <button data-value="/" class="btn text-2xl font-semibold bg-yellow-400 dark:bg-yellow-600 text-white p-4 rounded-2xl">÷</button>
                
                <!-- Row 2 -->
                <button data-value="7" class="btn text-2xl font-semibold bg-gray-200 dark:bg-gray-700 p-4 rounded-2xl">7</button>
                <button data-value="8" class="btn text-2xl font-semibold bg-gray-200 dark:bg-gray-700 p-4 rounded-2xl">8</button>
                <button data-value="9" class="btn text-2xl font-semibold bg-gray-200 dark:bg-gray-700 p-4 rounded-2xl">9</button>
                <button data-value="*" class="btn text-2xl font-semibold bg-green-500 dark:bg-green-600 text-white p-4 rounded-2xl">×</button>
                
                <!-- Row 3 -->
                <button data-value="4" class="btn text-2xl font-semibold bg-gray-200 dark:bg-gray-700 p-4 rounded-2xl">4</button>
                <button data-value="5" class="btn text-2xl font-semibold bg-gray-200 dark:bg-gray-700 p-4 rounded-2xl">5</button>
                <button data-value="6" class="btn text-2xl font-semibold bg-gray-200 dark:bg-gray-700 p-4 rounded-2xl">6</button>
                <button data-value="-" class="btn text-2xl font-semibold bg-pink-400 dark:bg-pink-600 text-white p-4 rounded-2xl">−</button>

                <!-- Row 4 -->
                <button data-value="1" class="btn text-2xl font-semibold bg-gray-200 dark:bg-gray-700 p-4 rounded-2xl">1</button>
                <button data-value="2" class="btn text-2xl font-semibold bg-gray-200 dark:bg-gray-700 p-4 rounded-2xl">2</button>
                <button data-value="3" class="btn text-2xl font-semibold bg-gray-200 dark:bg-gray-700 p-4 rounded-2xl">3</button>
                <button data-value="+" class="btn text-2xl font-semibold bg-red-500 dark:bg-red-600 text-white p-4 rounded-2xl">+</button>

                <!-- Row 5 -->
                <button data-value="sqrt" class="btn text-2xl font-semibold bg-violet-500 dark:bg-violet-600 text-white p-4 rounded-2xl">√</button>
                <button data-value="0" class="btn text-2xl font-semibold bg-gray-200 dark:bg-gray-700 p-4 rounded-2xl">0</button>
                <button data-value="." class="btn text-2xl font-semibold bg-gray-200 dark:bg-gray-700 p-4 rounded-2xl">.</button>
                <button data-value="=" class="btn text-2xl font-semibold bg-blue-500 dark:bg-blue-600 text-white p-4 rounded-2xl">=</button>
            </div>
        </div>

        <!-- History Panel -->
        <div class="bg-white dark:bg-black rounded-3xl shadow-2xl p-6 mt-6">
            <h2 class="text-xl font-bold mb-4 text-gray-500 dark:text-gray-400">History</h2>
            <div id="history-list" class="space-y-3 h-32 overflow-y-auto pr-2">
                <p class="text-gray-400 dark:text-gray-500 text-center">No calculations yet.</p>
            </div>
        </div>
    </div>

    <script>
        document.addEventListener('DOMContentLoaded', () => {
            // DOM Elements
            const display = document.getElementById('display');
            const expressionDiv = document.getElementById('expression');
            const historyList = document.getElementById('history-list');
            const calculatorGrid = document.querySelector('.calculator-grid');
            
            // Theme Elements
            const themeToggle = document.getElementById('theme-toggle');
            const lightIcon = document.getElementById('theme-icon-light');
            const darkIcon = document.getElementById('theme-icon-dark');

            // State variables
            let currentInput = '0';
            let expression = '';
            let history = [];
            let justCalculated = false;

            const updateDisplay = () => {
                display.textContent = currentInput;
                expressionDiv.textContent = expression.replace(/\*/g, '×').replace(/\//g, '÷') || ' ';
            };

            const updateHistory = () => {
                if (history.length === 0) {
                    historyList.innerHTML = '<p class="text-gray-400 dark:text-gray-500 text-center">No calculations yet.</p>';
                    return;
                }
                historyList.innerHTML = history.map(item => `
                    <div class="text-right">
                        <div class="text-gray-500 dark:text-gray-400 text-sm">${item.expression.replace(/\*/g, '×').replace(/\//g, '÷')}</div>
                        <div class="font-bold text-lg">${item.result}</div>
                    </div>
                `).join('<hr class="border-gray-200 dark:border-gray-700">');
            };

            


