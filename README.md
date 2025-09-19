𝔸𝕝𝕚 𝕄𝕒𝕙𝕞𝕠𝕦𝕕
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>حاسبة تطور رأس المال في التداول</title>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            border-radius: 0;
        }

        :root {
            --bg-color: #ffffff;
            --text-color: #333333;
            --input-bg: #f5f5f5;
            --input-border: #ddd;
            --button-bg: #007bff;
            --button-hover: #0056b3;
            --card-bg: #ffffff;
            --card-border: #e0e0e0;
        }

        [data-theme="dark"] {
            --bg-color: #1a1a1a;
            --text-color: #ffffff;
            --input-bg: #2d2d2d;
            --input-border: #444;
            --button-bg: #0d6efd;
            --button-hover: #0b5ed7;
            --card-bg: #2d2d2d;
            --card-border: #444;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background-color: var(--bg-color);
            color: var(--text-color);
            line-height: 1.6;
            transition: all 0.3s ease;
            min-height: 100vh;
        }

        .container {
            max-width: 1400px;
            margin: 0 auto;
            padding: 10px;
            min-height: 100vh;
        }

        .header {
            text-align: center;
            margin-bottom: 20px;
            padding: 10px;
        }

        .header h1 {
            font-size: clamp(1.5rem, 4vw, 2.5rem);
            margin-bottom: 5px;
        }

        .header p {
            font-size: clamp(0.9rem, 2vw, 1.1rem);
        }

        .theme-toggle {
            position: fixed;
            top: 10px;
            left: 10px;
            background: var(--button-bg);
            color: white;
            border: none;
            padding: 8px 12px;
            cursor: pointer;
            transition: background-color 0.3s ease;
            z-index: 1000;
            font-size: clamp(0.8rem, 2vw, 1rem);
        }

        .theme-toggle:hover {
            background: var(--button-hover);
        }

        .main-content {
            display: flex;
            flex-direction: column;
            gap: 15px;
        }

        .inputs-section {
            background: var(--card-bg);
            border: 1px solid var(--card-border);
            padding: 15px;
            width: 100%;
        }

        .chart-section {
            background: var(--card-bg);
            border: 1px solid var(--card-border);
            padding: 15px;
            min-height: 400px;
            width: 100%;
        }

        .input-grid {
            display: grid;
            grid-template-columns: 1fr;
            gap: 15px;
        }

        .input-group {
            display: flex;
            flex-direction: column;
        }

        .input-group label {
            margin-bottom: 5px;
            font-weight: 600;
            font-size: clamp(0.9rem, 2vw, 1rem);
        }

        .input-group input {
            width: 100%;
            padding: 10px;
            background: var(--input-bg);
            border: 1px solid var(--input-border);
            color: var(--text-color);
            font-size: clamp(0.9rem, 2vw, 1rem);
            transition: border-color 0.3s ease;
        }

        .input-group input:focus {
            outline: none;
            border-color: var(--button-bg);
        }

        .ratio-input-group {
            display: flex;
            align-items: center;
            gap: 8px;
        }

        .ratio-input {
            flex: 1;
            min-width: 60px;
        }

        .ratio-separator {
            font-weight: bold;
            font-size: 1.2rem;
        }

        .calculate-btn {
            width: 100%;
            padding: 12px;
            background: var(--button-bg);
            color: white;
            border: none;
            font-size: clamp(1rem, 2.5vw, 1.2rem);
            font-weight: 600;
            cursor: pointer;
            transition: background-color 0.3s ease;
            margin-top: 15px;
        }

        .calculate-btn:hover {
            background: var(--button-hover);
        }

        .results {
            margin-top: 15px;
            padding: 15px;
            background: var(--input-bg);
            border: 1px solid var(--input-border);
        }

        .results h3 {
            margin-bottom: 10px;
            font-size: clamp(1rem, 2.5vw, 1.2rem);
        }

        .result-item {
            display: flex;
            justify-content: space-between;
            margin-bottom: 8px;
            padding: 6px 0;
            border-bottom: 1px solid var(--input-border);
            font-size: clamp(0.9rem, 2vw, 1rem);
        }

        .result-item:last-child {
            border-bottom: none;
        }

        .result-label {
            font-weight: 600;
        }

        .result-value {
            font-weight: bold;
            color: var(--button-bg);
        }

        .chart-section h2 {
            margin-bottom: 15px;
            font-size: clamp(1.1rem, 2.5vw, 1.3rem);
        }

        #capitalChart {
            max-height: 350px;
            width: 100% !important;
            height: auto !important;
        }

        /* Tablet styles */
        @media (min-width: 768px) {
            .container {
                padding: 20px;
            }

            .main-content {
                flex-direction: row;
                gap: 20px;
            }

            .inputs-section {
                flex: 1;
                min-width: 300px;
                max-width: 400px;
            }

            .chart-section {
                flex: 2;
                min-height: 500px;
            }

            .input-grid {
                grid-template-columns: 1fr;
                gap: 18px;
            }

            .inputs-section,
            .chart-section {
                padding: 20px;
            }

            #capitalChart {
                max-height: 400px;
            }
        }

        /* Desktop styles */
        @media (min-width: 1024px) {
            .container {
                padding: 30px;
            }

            .main-content {
                gap: 30px;
            }

            .inputs-section {
                padding: 25px;
            }

            .chart-section {
                padding: 25px;
                min-height: 600px;
            }

            .input-grid {
                gap: 20px;
            }

            #capitalChart {
                max-height: 500px;
            }
        }

        /* Large desktop styles */
        @media (min-width: 1200px) {
            .input-grid {
                grid-template-columns: 1fr 1fr;
                gap: 15px 20px;
            }

            .calculate-btn {
                grid-column: 1 / -1;
            }

            .results {
                grid-column: 1 / -1;
            }
        }

        /* Small mobile adjustments */
        @media (max-width: 480px) {
            .container {
                padding: 8px;
            }

            .theme-toggle {
                position: relative;
                top: auto;
                left: auto;
                margin-bottom: 10px;
                width: 100%;
            }

            .inputs-section,
            .chart-section {
                padding: 12px;
            }

            .input-group input {
                padding: 8px;
            }

            .calculate-btn {
                padding: 10px;
            }

            #capitalChart {
                max-height: 250px;
            }
        }

        /* Very small screens */
        @media (max-width: 320px) {
            .ratio-input-group {
                flex-direction: column;
                gap: 5px;
            }

            .ratio-separator {
                display: none;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <button class="theme-toggle" onclick="toggleTheme()">🌙 الوضع الليلي</button>
        
        <div class="header">
            <h1>حاسبة تطور رأس المال في التداول</h1>
            <p>احسب تطور رأس مالك بناءً على استراتيجية التداول الخاصة بك</p>
        </div>

        <div class="main-content">
            <div class="inputs-section">
                <h2>المدخلات</h2>
                
                <div class="input-grid">
                    <div class="input-group">
                        <label for="initialCapital">رأس المال الابتدائي</label>
                        <input type="number" id="initialCapital" value="10000" min="1" step="0.01">
                    </div>

                    <div class="input-group">
                        <label for="targetCapital">الهدف النهائي</label>
                        <input type="number" id="targetCapital" value="50000" min="1" step="0.01">
                    </div>

                    <div class="input-group">
                        <label for="riskPercentage">نسبة المخاطرة لكل صفقة (%)</label>
                        <input type="number" id="riskPercentage" value="1" min="0.1" max="100" step="0.1">
                    </div>

                    <div class="input-group">
                        <label>نسبة الربح إلى المخاطرة</label>
                        <div class="ratio-input-group">
                            <input type="number" id="rewardRatio" class="ratio-input" value="2" min="0.1" max="100" step="0.1">
                            <span class="ratio-separator">:</span>
                            <input type="number" id="riskRatio" class="ratio-input" value="1" min="0.1" max="100" step="0.1">
                        </div>
                    </div>

                    <div class="input-group">
                        <label for="winRate">نسبة التداولات الناجحة (%)</label>
                        <input type="number" id="winRate" value="60" min="1" max="100" step="1">
                    </div>

                    <div class="input-group">
                        <label for="tradesPerDay">عدد التداولات اليومية</label>
                        <input type="number" id="tradesPerDay" value="5" min="1" max="100" step="1">
                    </div>

                    <button class="calculate-btn" onclick="calculateCapitalGrowth()">احسب التطور</button>

                    <div class="results" id="results" style="display: none;">
                        <h3>النتائج</h3>
                        <div class="result-item">
                            <span class="result-label">رأس المال النهائي:</span>
                            <span class="result-value" id="finalCapital">-</span>
                        </div>
                        <div class="result-item">
                            <span class="result-label">عدد الأيام:</span>
                            <span class="result-value" id="totalDays">-</span>
                        </div>
                        <div class="result-item">
                            <span class="result-label">إجمالي الصفقات:</span>
                            <span class="result-value" id="totalTrades">-</span>
                        </div>
                        <div class="result-item">
                            <span class="result-label">نسبة النمو:</span>
                            <span class="result-value" id="growthRate">-</span>
                        </div>
                    </div>
                </div>
            </div>

            <div class="chart-section">
                <h2>مخطط تطور رأس المال</h2>
                <canvas id="capitalChart"></canvas>
            </div>
        </div>
    </div>

    <script>
        let chart = null;
        let isDarkMode = false;

        function toggleTheme() {
            isDarkMode = !isDarkMode;
            const body = document.body;
            const button = document.querySelector('.theme-toggle');
            
            if (isDarkMode) {
                body.setAttribute('data-theme', 'dark');
                button.textContent = '☀️ الوضع النهاري';
            } else {
                body.removeAttribute('data-theme');
                button.textContent = '🌙 الوضع الليلي';
            }
            
            // Update chart colors if chart exists
            if (chart) {
                updateChartColors();
            }
        }

        function updateChartColors() {
            const textColor = isDarkMode ? '#ffffff' : '#333333';
            const gridColor = isDarkMode ? '#444' : '#e0e0e0';
            
            chart.options.scales.x.ticks.color = textColor;
            chart.options.scales.y.ticks.color = textColor;
            chart.options.scales.x.grid.color = gridColor;
            chart.options.scales.y.grid.color = gridColor;
            chart.options.plugins.legend.labels.color = textColor;
            chart.update();
        }

        function calculateCapitalGrowth() {
            // Get input values
            const initialCapital = parseFloat(document.getElementById('initialCapital').value);
            const targetCapital = parseFloat(document.getElementById('targetCapital').value);
            const riskPercentage = parseFloat(document.getElementById('riskPercentage').value) / 100;
            const rewardRatio = parseFloat(document.getElementById('rewardRatio').value);
            const riskRatio = parseFloat(document.getElementById('riskRatio').value);
            const winRate = parseFloat(document.getElementById('winRate').value) / 100;
            const tradesPerDay = parseInt(document.getElementById('tradesPerDay').value);

            // Validation
            if (initialCapital <= 0 || targetCapital <= initialCapital) {
                alert('يرجى التأكد من أن رأس المال الابتدائي أكبر من صفر والهدف النهائي أكبر من رأس المال الابتدائي');
                return;
            }

            if (rewardRatio <= 0 || riskRatio <= 0) {
                alert('يرجى التأكد من أن نسبة الربح إلى المخاطرة صحيحة');
                return;
            }

            // Calculate reward to risk ratio
            const rewardToRiskRatio = rewardRatio / riskRatio;

            // Initialize variables
            let currentCapital = initialCapital;
            let days = 0;
            const capitalHistory = [initialCapital];
            const maxDays = 1000; // Prevent infinite loops

            // Simulation
            while (currentCapital < targetCapital && days < maxDays && currentCapital > 0) {
                days++;
                
                // Daily trades simulation
                for (let trade = 0; trade < tradesPerDay; trade++) {
                    const riskAmount = currentCapital * riskPercentage;
                    const profitAmount = riskAmount * rewardToRiskRatio;
                    const randomValue = Math.random();
                    
                    if (randomValue <= winRate) {
                        // Winning trade
                        currentCapital += profitAmount;
                    } else {
                        // Losing trade
                        currentCapital -= riskAmount;
                    }
                    
                    // Stop if capital becomes zero or negative
                    if (currentCapital <= 0) {
                        currentCapital = 0;
                        break;
                    }
                }
                
                capitalHistory.push(currentCapital);
                
                // Stop if capital becomes zero
                if (currentCapital <= 0) {
                    break;
                }
            }

            // Display results
            displayResults(initialCapital, currentCapital, days, tradesPerDay * days);
            
            // Create chart
            createChart(capitalHistory, targetCapital);
        }

        function displayResults(initialCapital, finalCapital, days, totalTrades) {
            const growthRate = ((finalCapital - initialCapital) / initialCapital * 100).toFixed(2);
            
            document.getElementById('finalCapital').textContent = finalCapital.toLocaleString('ar-SA', {
                minimumFractionDigits: 2,
                maximumFractionDigits: 2
            });
            document.getElementById('totalDays').textContent = days.toLocaleString('ar-SA');
            document.getElementById('totalTrades').textContent = totalTrades.toLocaleString('ar-SA');
            document.getElementById('growthRate').textContent = growthRate + '%';
            
            document.getElementById('results').style.display = 'block';
        }

        function createChart(capitalHistory, targetCapital) {
            const ctx = document.getElementById('capitalChart').getContext('2d');
            
            // Destroy existing chart if it exists
            if (chart) {
                chart.destroy();
            }
            
            const labels = capitalHistory.map((_, index) => index);
            const textColor = isDarkMode ? '#ffffff' : '#333333';
            const gridColor = isDarkMode ? '#444' : '#e0e0e0';
            
            chart = new Chart(ctx, {
                type: 'line',
                data: {
                    labels: labels,
                    datasets: [{
                        label: 'رأس المال',
                        data: capitalHistory,
                        borderColor: '#007bff',
                        backgroundColor: 'rgba(0, 123, 255, 0.1)',
                        borderWidth: 2,
                        fill: true,
                        tension: 0.4
                    }, {
                        label: 'الهدف النهائي',
                        data: new Array(capitalHistory.length).fill(targetCapital),
                        borderColor: '#28a745',
                        backgroundColor: 'transparent',
                        borderWidth: 2,
                        borderDash: [5, 5],
                        fill: false,
                        pointRadius: 0
                    }]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    plugins: {
                        legend: {
                            labels: {
                                color: textColor
                            }
                        }
                    },
                    scales: {
                        x: {
                            title: {
                                display: true,
                                text: 'الأيام',
                                color: textColor
                            },
                            ticks: {
                                color: textColor
                            },
                            grid: {
                                color: gridColor
                            }
                        },
                        y: {
                            title: {
                                display: true,
                                text: 'رأس المال',
                                color: textColor
                            },
                            ticks: {
                                color: textColor,
                                callback: function(value) {
                                    return value.toLocaleString('ar-SA');
                                }
                            },
                            grid: {
                                color: gridColor
                            }
                        }
                    }
                }
            });
        }

        // Initialize with default calculation
        window.addEventListener('load', function() {
            calculateCapitalGrowth();
     
