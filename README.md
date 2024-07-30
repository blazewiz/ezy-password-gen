# ezy-password-gen
i love AI it made this in like 30 secounds 


Password Generator
Overview
The Password Generator is a simple web-based tool designed to create strong, random passwords. It is built using HTML, CSS, and JavaScript. This tool allows users to generate passwords that can include uppercase letters, lowercase letters, numbers, and special characters based on user preferences.

Features
Length Selection: Users can specify the desired length of the password.
Character Types: Users can choose which types of characters to include in the password:
Uppercase Letters (A-Z)
Lowercase Letters (a-z)
Numbers (0-9)
Special Characters (!, @, #, $, etc.)
Generate Button: A button that triggers the generation of a password based on the selected options.
Copy to Clipboard: A feature that allows users to copy the generated password to the clipboard for easy use.
Technologies Used
HTML: Provides the structure and layout of the password generator interface.
CSS: Adds styling to the interface to make it visually appealing.
JavaScript: Implements the logic for password generation and interaction with the user interface.
Code Example
Here is an example of the code used for the Password Generator:

HTML

html
Kopier kode
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Password Generator</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <div class="container">
        <h1>Password Generator</h1>
        <label for="length">Password Length:</label>
        <input type="number" id="length" name="length" min="8" max="128" value="16">
        
        <div class="options">
            <label>
                <input type="checkbox" id="uppercase" checked> Include Uppercase Letters
            </label>
            <label>
                <input type="checkbox" id="lowercase" checked> Include Lowercase Letters
            </label>
            <label>
                <input type="checkbox" id="numbers" checked> Include Numbers
            </label>
            <label>
                <input type="checkbox" id="symbols" checked> Include Symbols
            </label>
        </div>
        
        <button id="generate">Generate Password</button>
        <div class="result">
            <textarea id="password" readonly></textarea>
            <button id="copy">Copy to Clipboard</button>
        </div>
    </div>

    <script src="script.js"></script>
</body>
</html>
CSS (styles.css)

css
Kopier kode
body {
    font-family: Arial, sans-serif;
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
    background-color: #f0f0f0;
    margin: 0;
}

.container {
    background-color: white;
    padding: 20px;
    border-radius: 8px;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
    width: 300px;
    text-align: center;
}

h1 {
    margin-bottom: 20px;
}

.options {
    text-align: left;
    margin-bottom: 20px;
}

button {
    padding: 10px;
    border: none;
    background-color: #007BFF;
    color: white;
    border-radius: 5px;
    cursor: pointer;
    margin-top: 10px;
}

button:disabled {
    background-color: #ccc;
}

.result {
    margin-top: 20px;
}

textarea {
    width: 100%;
    height: 50px;
    resize: none;
    margin-bottom: 10px;
}
JavaScript (script.js)

javascript
Kopier kode
const lengthElement = document.getElementById('length');
const uppercaseElement = document.getElementById('uppercase');
const lowercaseElement = document.getElementById('lowercase');
const numbersElement = document.getElementById('numbers');
const symbolsElement = document.getElementById('symbols');
const generateButton = document.getElementById('generate');
const passwordElement = document.getElementById('password');
const copyButton = document.getElementById('copy');

const randomFunc = {
    upper: getRandomUpper,
    lower: getRandomLower,
    number: getRandomNumber,
    symbol: getRandomSymbol
};

generateButton.addEventListener('click', () => {
    const length = +lengthElement.value;
    const hasUpper = uppercaseElement.checked;
    const hasLower = lowercaseElement.checked;
    const hasNumber = numbersElement.checked;
    const hasSymbol = symbolsElement.checked;

    passwordElement.value = generatePassword(hasUpper, hasLower, hasNumber, hasSymbol, length);
});

copyButton.addEventListener('click', () => {
    const textarea = document.createElement('textarea');
    const password = passwordElement.value;

    if (!password) { return; }

    textarea.value = password;
    document.body.appendChild(textarea);
    textarea.select();
    document.execCommand('copy');
    textarea.remove();
    alert('Password copied to clipboard!');
});

function generatePassword(upper, lower, number, symbol, length) {
    let generatedPassword = '';
    const typesCount = upper + lower + number + symbol;
    const typesArr = [{upper}, {lower}, {number}, {symbol}].filter(item => Object.values(item)[0]);

    if(typesCount === 0) {
        return '';
    }

    for(let i = 0; i < length; i += typesCount) {
        typesArr.forEach(type => {
            const funcName = Object.keys(type)[0];
            generatedPassword += randomFunc[funcName]();
        });
    }

    const finalPassword = generatedPassword.slice(0, length);
    return finalPassword;
}

function getRandomUpper() {
    return String.fromCharCode(Math.floor(Math.random() * 26) + 65);
}

function getRandomLower() {
    return String.fromCharCode(Math.floor(Math.random() * 26) + 97);
}

function getRandomNumber() {
    return String.fromCharCode(Math.floor(Math.random() * 10) + 48);
}

function getRandomSymbol() {
    const symbols = '!@#$%^&*(){}[]=<>/,.';
    return symbols[Math.floor(Math.random() * symbols.length)];
}
