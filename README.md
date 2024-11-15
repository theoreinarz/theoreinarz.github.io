<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Carbon Footprint Tracker</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 20px;
            padding: 20px;
            background-color: #f4f4f4;
            border-radius: 8px;
            max-width: 600px;
            margin: auto;
        }
        h2 {
            text-align: center;
        }
        .category {
            margin-bottom: 20px;
            padding: 15px;
            border: 1px solid #ccc;
            border-radius: 5px;
            background-color: #fff;
        }
        .slider-container {
            display: flex;
            flex-direction: column;
            margin-bottom: 10px;
        }
        .slider-label {
            margin-bottom: 5px;
        }
        .slider {
            width: 100%;
            max-width: 480px;
            appearance: none;
            height: 5px;
            background: #ddd;
            border-radius: 5px;
            transition: background 0.3s;
        }
        .slider::-webkit-slider-thumb {
            -webkit-appearance: none;
            appearance: none;
            width: 15px;
            height: 15px;
            background: #28a745;
            border-radius: 50%;
            cursor: pointer;
            margin-top: -5px;
        }
        .slider::-moz-range-thumb {
            width: 15px;
            height: 15px;
            background: #28a745;
            border-radius: 50%;
            cursor: pointer;
        }
        .button {
            display: block;
            width: 100%;
            padding: 15px;
            background-color: #28a745;
            color: white;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            font-size: 18px;
        }
        .button:hover {
            background-color: #218838;
        }
        .result {
            margin-top: 20px;
            font-weight: bold;
            text-align: center;
        }
        .feedback {
            margin-top: 20px;
            padding: 10px;
            border: 1px solid #ccc;
            border-radius: 5px;
            background-color: #e9ecef;
        }
        canvas {
            max-width: 100%;
            margin: 20px 0;
        }
    </style>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
</head>
<body>

    <h2>Carbon Footprint Tracker</h2>

    <div class="category">
        <h3>Transport (km)</h3>
        <div class="slider-container">
            <span class="slider-label">Car:</span>
            <input type="range" class="slider" id="car" min="0" max="500" value="0">
            <span class="slider-value" id="carValue">0</span> km
        </div>
        <div class="slider-container">
            <span class="slider-label">Bus:</span>
            <input type="range" class="slider" id="bus" min="0" max="500" value="0">
            <span class="slider-value" id="busValue">0</span> km
        </div>
        <div class="slider-container">
            <span class="slider-label">Train:</span>
            <input type="range" class="slider" id="train" min="0" max="500" value="0">
            <span class="slider-value" id="trainValue">0</span> km
        </div>
        <div class="slider-container">
            <span class="slider-label">Bicycle:</span>
            <input type="range" class="slider" id="bicycle" min="0" max="100" value="0">
            <span class="slider-value" id="bicycleValue">0</span> km
        </div>
        <div class="slider-container">
            <span class="slider-label">Walking:</span>
            <input type="range" class="slider" id="walking" min="0" max="20" value="0">
            <span class="slider-value" id="walkingValue">0</span> km
        </div>
        <div class="slider-container">
            <span class="slider-label">Plane:</span>
            <input type="range" class="slider" id="plane" min="0" max="2000" value="0">
            <span class="slider-value" id="planeValue">0</span> km
        </div>
    </div>

    <div class="category">
        <h3>Household Energy (m²)</h3>
        <button id="flat">Flat</button>
        <button id="house">House</button>
        <button id="bungalow">Bungalow</button>
        <div class="slider-container">
            <span class="slider-label">Energy:</span>
            <input type="range" class="slider" id="energy" min="0" max="200" value="0">
            <span class="slider-value" id="energyValue">0</span> m²
        </div>
    </div>

    <div class="category">
        <h3>Diet (grams)</h3>
        <div class="slider-container">
            <span class="slider-label">Meat:</span>
            <input type="range" class="slider" id="meat" min="0" max="1000" value="0">
            <span class="slider-value" id="meatValue">0</span>
        </div>
        <div class="slider-container">
            <span class="slider-label">Dairy:</span>
            <input type="range" class="slider" id="dairy" min="0" max="1000" value="0">
            <span class="slider-value" id="dairyValue">0</span>
        </div>
        <div class="slider-container">
            <span class="slider-label">Grains:</span>
            <input type="range" class="slider" id="grains" min="0" max="1000" value="0">
            <span class="slider-value" id="grainsValue">0</span>
        </div>
        <div class="slider-container">
            <span class="slider-label">Fruits & Veggies:</span>
            <input type="range" class="slider" id="fruits" min="0" max="1000" value="0">
            <span class="slider-value" id="fruitsValue">0</span>
        </div>
        <div class="slider-container">
            <span class="slider-label">Processed Foods:</span>
            <input type="range" class="slider" id="processed" min="0" max="1000" value="0">
            <span class="slider-value" id="processedValue">0</span>
        </div>
    </div>

    <div class="category">
        <h3>Water Usage (units)</h3>
        <div class="slider-container">
            <span class="slider-label">Glasses of Water:</span>
            <input type="range" class="slider" id="water" min="0" max="20" value="0">
            <span class="slider-value" id="waterValue">0</span>
        </div>
        <div class="slider-container">
            <span class="slider-label">Showers:</span>
            <input type="range" class="slider" id="showers" min="0" max="10" value="0">
            <span class="slider-value" id="showersValue">0</span>
        </div>
        <div class="slider-container">
            <span class="slider-label">Baths:</span>
            <input type="range" class="slider" id="baths" min="0" max="10" value="0">
            <span class="slider-value" id="bathsValue">0</span>
        </div>
        <div class="slider-container">
            <span class="slider-label">Dishwasher Cycles:</span>
            <input type="range" class="slider" id="dishwasher" min="0" max="10" value="0">
            <span class="slider-value" id="dishwasherValue">0</span>
        </div>
        <div class="slider-container">
            <span class="slider-label">Laundry Cycles:</span>
            <input type="range" class="slider" id="laundry" min="0" max="10" value="0">
            <span class="slider-value" id="laundryValue">0</span>
        </div>
    </div>

    <div class="category">
        <h3>Purchases (units)</h3>
        <div class="slider-container">
            <span class="slider-label">Clothing Items:</span>
            <input type="range" class="slider" id="clothing" min="0" max="20" value="0">
            <span class="slider-value" id="clothingValue">0</span>
        </div>
        <div class="slider-container">
            <span class="slider-label">Electronic Items:</span>
            <input type="range" class="slider" id="electronics" min="0" max="20" value="0">
            <span class="slider-value" id="electronicsValue">0</span>
        </div>
        <div class="slider-container">
            <span class="slider-label">Single-Use Items:</span>
            <input type="range" class="slider" id="singleUse" min="0" max="20" value="0">
            <span class="slider-value" id="singleUseValue">0</span>
        </div>
    </div>

    <div class="category">
        <h3>Household Waste (bags)</h3>
        <div class="slider-container">
            <span class="slider-label">Waste Bags:</span>
            <input type="range" class="slider" id="waste" min="0" max="10" value="0">
            <span class="slider-value" id="wasteValue">0</span>
        </div>
    </div>

    <button class="button" id="calculate">Calculate Total Carbon Output</button>

    <div class="result" id="result"></div>
    <canvas id="emissionsChart"></canvas>
    <div class="feedback" id="feedback"></div>

    <script>
        const sliders = document.querySelectorAll('.slider');
        
        sliders.forEach(slider => {
            slider.addEventListener('input', function() {
                const value = this.value;
                const max = this.max;
                const percentage = (value / max) * 100;
                this.style.background = `linear-gradient(to right, #28a745 ${percentage}%, #ddd ${percentage}%)`;
                document.getElementById(slider.id + 'Value').textContent = value;
            });

            const initialValue = slider.value;
            const initialMax = slider.max;
            const initialPercentage = (initialValue / initialMax) * 100;
            slider.style.background = `linear-gradient(to right, #28a745 ${initialPercentage}%, #ddd ${initialPercentage}%)`;
        });

        document.getElementById('calculate').addEventListener('click', function() {
            const car = parseInt(document.getElementById('car').value) * 120; // g CO2/km
            const bus = parseInt(document.getElementById('bus').value) * 30; // g CO2/km
            const train = parseInt(document.getElementById('train').value) * 40; // g CO2/km
            const bicycle = parseInt(document.getElementById('bicycle').value) * 0; // g CO2/km
            const walking = parseInt(document.getElementById('walking').value) * 0; // g CO2/km
            const plane = parseInt(document.getElementById('plane').value) * 250; // g CO2/km

            const energy = parseInt(document.getElementById('energy').value) * 
                (document.getElementById('flat').style.backgroundColor === 'rgb(0, 123, 255)' ? 150 : 
                (document.getElementById('house').style.backgroundColor === 'rgb(0, 123, 255)' ? 200 : 180)); // g CO2/m²

            const meat = parseInt(document.getElementById('meat').value) * 7; // g CO2/g
            const dairy = parseInt(document.getElementById('dairy').value) * 1.5; // g CO2/g
            const grains = parseInt(document.getElementById('grains').value) * 0.5; // g CO2/g
            const fruits = parseInt(document.getElementById('fruits').value) * 0.2; // g CO2/g
            const processed = parseInt(document.getElementById('processed').value) * 3; // g CO2/g

            const water = (parseInt(document.getElementById('water').value) * 0.5) + 
                          (parseInt(document.getElementById('showers').value) * 150) + 
                          (parseInt(document.getElementById('baths').value) * 200) + 
                          (parseInt(document.getElementById('dishwasher').value) * 100) + 
                          (parseInt(document.getElementById('laundry').value) * 50); // g CO2

            const clothing = parseInt(document.getElementById('clothing').value) * 20; // g CO2
            const electronics = parseInt(document.getElementById('electronics').value) * 50; // g CO2
            const singleUse = parseInt(document.getElementById('singleUse').value) * 30; // g CO2

            const waste = parseInt(document.getElementById('waste').value) * 1000; // Daily emissions per bag

            const total = car + bus + train + bicycle + walking + plane + energy + meat + dairy + grains + fruits + processed + water + clothing + electronics + singleUse + waste;

            document.getElementById('result').textContent = `Total Carbon Output: ${total} grams`;

            // Emissions breakdown
            const emissionsBreakdown = {
                Transport: car + bus + train + bicycle + walking + plane,
                Energy: energy,
                Diet: meat + dairy + grains + fruits + processed,
                Water: water,
                Purchases: clothing + electronics + singleUse,
                Waste: waste
            };

            // Create doughnut chart
            const ctx = document.getElementById('emissionsChart').getContext('2d');
            const chart = new Chart(ctx, {
                type: 'doughnut',
                data: {
                    labels: Object.keys(emissionsBreakdown),
                    datasets: [{
                        label: 'Emissions Breakdown',
                        data: Object.values(emissionsBreakdown),
                        backgroundColor: ['#ff6384', '#36a2eb', '#cc65fe', '#ffce56', '#4bc0c0', '#ff9f40'],
                    }]
                },
                options: {
                    responsive: true,
                    plugins: {
                        legend: {
                            position: 'top',
                        },
                    }
                }
            });

            // Feedback
            const feedback = generateFeedback(emissionsBreakdown);
            document.getElementById('feedback').innerHTML = feedback;
        });

        function generateFeedback(breakdown) {
            const sortedBreakdown = Object.entries(breakdown).sort((a, b) => b[1] - a[1]).slice(0, 3);
            let feedback = '<h4>Your Top Emission Sources:</h4><ul>';
            sortedBreakdown.forEach(([category, amount]) => {
                feedback += `<li>${category}: ${amount} grams CO2</li>`;
                if (category === 'Purchases') {
                    feedback += `
                        <ul>
                            <li>Choose sustainable brands.</li>
                            <li>Consider second-hand options.</li>
                            <li>Avoid fast fashion.</li>
                        </ul>`;
                } else if (category === 'Transport') {
                    feedback += `
                        <ul>
                            <li>Use public transport whenever possible.</li>
                            <li>Walk or bike for short distances.</li>
                            <li>Carpool to reduce the number of vehicles on the road.</li>
                        </ul>`;
                } else if (category === 'Energy') {
                    feedback += `
                        <ul>
                            <li>Switch to energy-efficient appliances.</li>
                            <li>Consider renewable energy sources.</li>
                            <li>Improve insulation to reduce heating costs.</li>
                        </ul>`;
                }
            });
            feedback += '</ul>';
            return feedback;
        }

        const houseButtons = document.querySelectorAll('button[id="flat"], button[id="house"], button[id="bungalow"]');
        houseButtons.forEach(button => {
            button.addEventListener('click', function() {
                houseButtons.forEach(btn => btn.style.backgroundColor = '');
                button.style.backgroundColor = '#007bff';
                document.getElementById('energy').max = button.id === 'flat' ? 100 : (button.id === 'house' ? 150 : 80);
            });
        });
    </script>

</body>
</html>
