[egnunitcon.html(styling).txt](https://github.com/user-attachments/files/18501470/egnunitcon.html.styling.txt)# Engineering-Unit-Converter
[Uploadingbody {
    font-f<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Engineering Unit Converter</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <div class="container">
        <h1>Engineering Unit Converter</h1>
        <form id="converterForm">
            <!-- Input Value -->
            <div class="form-group">
                <label for="inputValue">Enter Value:</label>
                <input type="number" id="inputValue" placeholder="Enter a number" required>
            </div>

            <!-- Unit Type -->
            <div class="form-group">
                <label for="unitType">Select Unit Type:</label>
                <select id="unitType" onchange="updateUnits()">
                    <option value="length">Length</option>
                    <option value="mass">Mass</option>
                    <option value="temperature">Temperature</option>
                </select>
            </div>

            <!-- From Unit -->
            <div class="form-group">
                <label for="fromUnit">From:</label>
                <select id="fromUnit"></select>
            </div>

            <!-- To Unit -->
            <div class="form-group">
                <label for="toUnit">To:</label>
                <select id="toUnit"></select>
            </div>

            <button type="button" onclick="convert()">Convert</button>
        </form>

        <div id="result"></div>
    </div>
    <script src="script.js"></script>
</body>
</html>
amily: Arial, sans-serif;
    background-color: #f8f9fa;
    margin: 0;
    padding: 20px;
}

.container {
    max-width: 400px;
    margin: auto;
    background: #ffffff;
    padding: 20px;[egnunitcon.html(script).txt](https://github.com/user-attachments/files/18501475/egnunitcon.html.script.txt)// Units and conversion factors
const units = {
    length: {
        meter: 1,
        kilometer: 0.001,
        mile: 0.000621371,
        inch: 39.3701,
        foot: 3.28084
    },
    mass: {
        kilogram: 1,
        gram: 1000,
        pound: 2.20462,
        ounce: 35.274
    },
    temperature: {
        celsius: 'C',
        fahrenheit: 'F',
        kelvin: 'K'
    }
};

// Update unit dropdowns based on the selected type
function updateUnits() {
    const unitType = document.getElementById('unitType').value;
    const fromUnit = document.getElementById('fromUnit');
    const toUnit = document.getElementById('toUnit');

    // Clear existing options
    fromUnit.innerHTML = '';
    toUnit.innerHTML = '';

    // Populate dropdowns with relevant units
    for (let unit in units[unitType]) {
        const option1 = document.createElement('option');
        const option2 = document.createElement('option');
        option1.value = unit;
        option1.textContent = unit;
        option2.value = unit;
        option2.textContent = unit;
        fromUnit.appendChild(option1);
        toUnit.appendChild(option2);
    }
}

// Convert function
function convert() {
    const unitType = document.getElementById('unitType').value;
    const inputValue = parseFloat(document.getElementById('inputValue').value);
    const fromUnit = document.getElementById('fromUnit').value;
    const toUnit = document.getElementById('toUnit').value;

    if (isNaN(inputValue)) {
        document.getElementById('result').textContent = 'Please enter a valid number.';
        return;
    }

    let result;

    if (unitType === 'temperature') {
        // Handle temperature conversions separately
        if (fromUnit === toUnit) {
            result = inputValue;
        } else if (fromUnit === 'celsius' && toUnit === 'fahrenheit') {
            result = (inputValue * 9) / 5 + 32;
        } else if (fromUnit === 'celsius' && toUnit === 'kelvin') {
            result = inputValue + 273.15;
        } else if (fromUnit === 'fahrenheit' && toUnit === 'celsius') {
            result = ((inputValue - 32) * 5) / 9;
        } else if (fromUnit === 'fahrenheit' && toUnit === 'kelvin') {
            result = ((inputValue - 32) * 5) / 9 + 273.15;
        } else if (fromUnit === 'kelvin' && toUnit === 'celsius') {
            result = inputValue - 273.15;
        } else if (fromUnit === 'kelvin' && toUnit === 'fahrenheit') {
            result = ((inputValue - 273.15) * 9) / 5 + 32;
        }
    } else {
        // Handle length and mass conversions
        result = inputValue * (units[unitType][toUnit] / units[unitType][fromUnit]);
    }

    document.getElementById('result').textContent = `Converted Value: ${result.toFixed(2)}`;
}

// Initialize unit dropdowns
window.onload = updateUnits;


    border-radius: 8px;
    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
}

h1 {
    text-align: center;
    margin-bottom: 20px;
}

.form-group {
    margin-bottom: 15px;
}

label {
    display: block;
    margin-bottom: 5px;
    font-weight: bold;
}

input, select, button {
    width: 100%;
    padding: 8px;
    border: 1px solid #ccc;
    border-radius: 4px;
    box-sizing: border-box;
}

button {
    background-color: #007bff;
    color: white;
    font-size: 16px;
    cursor: pointer;
    margin-top: 10px;
}

button:hover {
    background-color: #0056b3;
}

#result {
    margin-top: 20px;
    text-align: center;
    font-size: 18px;
    color: #007bff;
}
 egnunitcon.html(styling).txt…]()
