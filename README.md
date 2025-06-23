<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>حاسبة تطور رأس المال في التداول</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        :root {
            --primary: #2c3e50;
            --secondary: #3498db;
            --success: #27ae60;
            --warning: #f39c12;
            --danger: #e74c3c;
            --light: #ecf0f1;
            --dark: #2c3e50;
            --mobile-breakpoint: 768px;
        }
        
        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        
        body {
            background: linear-gradient(135deg, #1a2a3a, #2c3e50);
            color: var(--light);
            min-height: 100vh;
            padding: 15px;
            line-height: 1.6;
            overflow-x: hidden;
            -webkit-tap-highlight-color: transparent;
        }
        
        .container {
            max-width: 1200px;
            margin: 0 auto;
        }
        
        header {
            text-align: center;
            padding: 15px;
            margin-bottom: 20px;
            background: rgba(0, 0, 0, 0.3);
            border-radius: 10px;
            box-shadow: 0 4px 10px rgba(0, 0, 0, 0.3);
            position: relative;
        }
        
        .mobile-menu-btn {
            position: absolute;
            left: 15px;
            top: 50%;
            transform: translateY(-50%);
            background: none;
            border: none;
            color: white;
            font-size: 1.5rem;
            display: none;
            cursor: pointer;
        }
        
        header h1 {
            font-size: 1.8rem;
            margin-bottom: 8px;
            color: var(--light);
            text-shadow: 0 2px 4px rgba(0, 0, 0, 0.5);
        }
        
        header p {
            font-size: 1rem;
            color: #bdc3c7;
            max-width: 100%;
        }
        
        .main-content {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 20px;
            margin-bottom: 30px;
        }
        
        @media (max-width: 900px) {
            .main-content {
                grid-template-columns: 1fr;
            }
        }
        
        .card {
            background: rgba(44, 62, 80, 0.7);
            border-radius: 10px;
            padding: 20px;
            box-shadow: 0 4px 10px rgba(0, 0, 0, 0.3);
            border: 1px solid rgba(255, 255, 255, 0.1);
            transition: transform 0.3s ease;
        }
        
        .card-title {
            font-size: 1.4rem;
            margin-bottom: 15px;
            padding-bottom: 12px;
            border-bottom: 2px solid var(--secondary);
            color: var(--light);
            display: flex;
            align-items: center;
            gap: 10px;
        }
        
        .card-title i {
            font-size: 1.2rem;
        }
        
        .input-group {
            margin-bottom: 15px;
        }
        
        label {
            display: block;
            margin-bottom: 6px;
            font-weight: 500;
            color: #bdc3c7;
            font-size: 0.95rem;
        }
        
        input {
            width: 100%;
            padding: 12px 15px;
            border: none;
            border-radius: 6px;
            background: rgba(255, 255, 255, 0.1);
            color: white;
            font-size: 1rem;
            border: 1px solid rgba(255, 255, 255, 0.2);
        }
        
        input:focus {
            outline: none;
            border-color: var(--secondary);
            background: rgba(255, 255, 255, 0.15);
        }
        
        button {
            background: var(--secondary);
            color: white;
            border: none;
            padding: 14px;
            border-radius: 6px;
            cursor: pointer;
            font-size: 1.1rem;
            font-weight: 600;
            transition: all 0.3s ease;
            width: 100%;
            margin-top: 10px;
            display: flex;
            justify-content: center;
            align-items: center;
            gap: 10px;
        }
        
        button:hover {
            background: #2980b9;
        }
        
        .results-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
            gap: 15px;
            margin-top: 20px;
        }
        
        .result-box {
            background: rgba(0, 0, 0, 0.3);
            border-radius: 8px;
            padding: 15px;
            text-align: center;
            border: 1px solid rgba(255, 255, 255, 0.1);
        }
        
        .result-value {
            font-size: 1.5rem;
            font-weight: 700;
            margin: 8px 0;
            color: var(--success);
        }
        
        .result-label {
            font-size: 0.95rem;
            color: #bdc3c7;
        }
        
        .table-container {
            overflow-x: auto;
            margin-top: 15px;
            border-radius: 8px;
            border: 1px solid rgba(255, 255, 255, 0.1);
        }
        
        table {
            width: 100%;
            border-collapse: collapse;
            min-width: 500px;
        }
        
        th, td {
            padding: 12px 10px;
            text-align: center;
            border-bottom: 1px solid rgba(255, 255, 255, 0.1);
            font-size: 0.95rem;
        }
        
        th {
            background: rgba(52, 152, 219, 0.3);
            color: white;
            font-weight: 600;
        }
        
        tr:last-child td {
            border-bottom: none;
        }
        
        tr:hover {
            background: rgba(255, 255, 255, 0.05);
        }
        
        .positive {
            color: var(--success);
            font-weight: bold;
        }
        
        .negative {
            color: var(--danger);
            font-weight: bold;
        }
        
        .chart-container {
            height: 300px;
            margin-top: 20px;
        }
        
        footer {
            text-align: center;
            padding: 15px;
            margin-top: 30px;
            color: #7f8c8d;
            border-top: 1px solid rgba(255, 255, 255, 0.1);
            font-size: 0.9rem;
        }
        
        /* تحسينات خاصة بالجوال */
        @media (max-width: 768px) {
            body {
                padding: 10px;
            }
            
            header {
                padding: 12px;
                margin-bottom: 15px;
            }
            
            header h1 {
                font-size: 1.5rem;
                padding: 0 30px;
            }
            
            header p {
                font-size: 0.9rem;
            }
            
            .mobile-menu-btn {
                display: block;
            }
            
            .card {
                padding: 15px;
            }
            
            .card-title {
                font-size: 1.3rem;
            }
            
            input {
                padding: 10px 12px;
                font-size: 0.95rem;
            }
            
            button {
                padding: 12px;
                font-size: 1rem;
            }
            
            .results-grid {
                grid-template-columns: 1fr;
                gap: 10px;
            }
            
            .result-box {
                padding: 12px;
            }
            
            .result-value {
                font-size: 1.3rem;
            }
            
            .result-label {
                font-size: 0.9rem;
            }
            
            .chart-container {
                height: 250px;
            }
        }
        
        @media (max-width: 480px) {
            header h1 {
                font-size: 1.3rem;
                padding: 0 20px;
            }
            
            .card-title {
                font-size: 1.2rem;
            }
            
            .result-value {
                font-size: 1.2rem;
            }
            
            th, td {
                padding: 10px 8px;
                font-size: 0.85rem;
            }
        }
        
        /* تحسينات لوضعية الأفقي (Landscape) */
        @media (max-height: 500px) and (orientation: landscape) {
            .main-content {
                grid-template-columns: 1fr 1fr;
            }
            
            .card {
                padding: 12px;
            }
            
            .input-group {
                margin-bottom: 10px;
            }
            
            input {
                padding: 8px 10px;
                font-size: 0.9rem;
            }
            
            button {
                padding: 10px;
                font-size: 0.95rem;
            }
            
            .chart-container {
                height: 200px;
            }
        }
        
        /* تحسينات للوضع الليلي وتجربة اللمس */
        .touch-optimized {
            -webkit-user-select: none;
            -moz-user-select: none;
            user-select: none;
        }
        
        input, button {
            -webkit-appearance: none;
            -moz-appearance: none;
            appearance: none;
        }
        
        button:active {
            transform: scale(0.98);
        }
        
        /* تحسينات للوضع الليلي */
        @media (prefers-color-scheme: light) {
            body {
                background: linear-gradient(135deg, #f5f7fa, #e4e7eb);
                color: #2c3e50;
            }
            
            header {
                background: rgba(255, 255, 255, 0.7);
            }
            
            header h1 {
                color: #2c3e50;
            }
            
            header p {
                color: #7f8c8d;
            }
            
            .card {
                background: rgba(255, 255, 255, 0.7);
            }
            
            .card-title {
                color: #2c3e50;
            }
            
            label {
                color: #2c3e50;
            }
            
            input {
                background: rgba(255, 255, 255, 0.8);
                color: #2c3e50;
                border: 1px solid #d1d8e0;
            }
            
            input:focus {
                background: rgba(255, 255, 255, 0.9);
            }
            
            .result-box {
                background: rgba(255, 255, 255, 0.8);
            }
            
            .result-label {
                color: #2c3e50;
            }
            
            table {
                background: rgba(255, 255, 255, 0.8);
            }
            
            th {
                background: rgba(52, 152, 219, 0.2);
                color: #2c3e50;
            }
            
            th, td {
                border-bottom: 1px solid #d1d8e0;
            }
            
            tr:hover {
                background: rgba(52, 152, 219, 0.1);
            }
            
            footer {
                color: #7f8c8d;
                border-top: 1px solid #d1d8e0;
            }
        }
    </style>
</head>
<body class="touch-optimized">
    <div class="container">
        <header>
            <button class="mobile-menu-btn">
                <i class="fas fa-bars"></i>
            </button>
            <h1>حاسبة تطور رأس المال في التداول</h1>
            <p>أدخل بيانات التداول الخاصة بك لحساب معدل نمو رأس المال المتوقع</p>
        </header>
        
        <div class="main-content">
            <div class="card">
                <h2 class="card-title"><i class="fas fa-calculator"></i> بيانات التداول</h2>
                
                <div class="input-group">
                    <label for="initialCapital"><i class="fas fa-coins"></i> رأس المال الأولي ($)</label>
                    <input type="number" id="initialCapital" value="10000" min="1">
                </div>
                
                <div class="input-group">
                    <label for="winRate"><i class="fas fa-chart-line"></i> نسبة الصفقات الرابحة (%)</label>
                    <input type="number" id="winRate" value="60" min="0" max="100" step="1">
                </div>
                
                <div class="input-group">
                    <label for="profitRate"><i class="fas fa-trophy"></i> معدل الربح لكل صفقة (% من رأس المال)</label>
                    <input type="number" id="profitRate" value="2" min="0" step="0.1">
                </div>
                
                <div class="input-group">
                    <label for="lossRate"><i class="fas fa-exclamation-triangle"></i> معدل الخسارة لكل صفقة (% من رأس المال)</label>
                    <input type="number" id="lossRate" value="1" min="0" step="0.1">
                </div>
                
                <div class="input-group">
                    <label for="updateInterval"><i class="fas fa-sync-alt"></i> عدد الصفقات في كل تحديث</label>
                    <input type="number" id="updateInterval" value="10" min="1">
                </div>
                
                <div class="input-group">
                    <label for="targetCapital"><i class="fas fa-bullseye"></i> الهدف النهائي ($)</label>
                    <input type="number" id="targetCapital" value="15000" min="1">
                </div>
                
                <button id="calculateBtn">
                    <i class="fas fa-calculator"></i> حساب تطور رأس المال
                </button>
            </div>
            
            <div class="card">
                <h2 class="card-title"><i class="fas fa-chart-bar"></i> النتائج</h2>
                
                <div class="results-grid">
                    <div class="result-box">
                        <div class="result-label">متوسط العائد لكل صفقة</div>
                        <div id="avgReturn" class="result-value">0.80%</div>
                    </div>
                    
                    <div class="result-box">
                        <div class="result-label">عدد الصفقات المطلوبة</div>
                        <div id="tradesRequired" class="result-value">52</div>
                    </div>
                    
                    <div class="result-box">
                        <div class="result-label">معدل النمو الإجمالي</div>
                        <div id="overallGrowth" class="result-value">50.00%</div>
                    </div>
                </div>
                
                <h3 style="margin-top: 20px; margin-bottom: 12px; display: flex; align-items: center; gap: 8px;">
                    <i class="fas fa-table"></i> تطور رأس المال
                </h3>
                
                <div class="table-container">
                    <table id="resultsTable">
                        <thead>
                            <tr>
                                <th>عدد الصفقات</th>
                                <th>رأس المال</th>
                                <th>نسبة النمو</th>
                            </tr>
                        </thead>
                        <tbody>
                            <tr>
                                <td>0</td>
                                <td>10,000.00 $</td>
                                <td class="positive">0.00%</td>
                            </tr>
                            <tr>
                                <td>10</td>
                                <td>10,830.00 $</td>
                                <td class="positive">8.30%</td>
                            </tr>
                            <tr>
                                <td>20</td>
                                <td>11,730.00 $</td>
                                <td class="positive">17.30%</td>
                            </tr>
                            <tr>
                                <td>30</td>
                                <td>12,708.00 $</td>
                                <td class="positive">27.08%</td>
                            </tr>
                            <tr>
                                <td>40</td>
                                <td>13,764.00 $</td>
                                <td class="positive">37.64%</td>
                            </tr>
                            <tr>
                                <td>50</td>
                                <td>14,913.00 $</td>
                                <td class="positive">49.13%</td>
                            </tr>
                        </tbody>
                    </table>
                </div>
            </div>
        </div>
        
        <div class="card">
            <h2 class="card-title"><i class="fas fa-chart-line"></i> مخطط تطور رأس المال</h2>
            <div class="chart-container">
                <canvas id="growthChart"></canvas>
            </div>
        </div>
        
        <footer>
            <p>تم تطوير هذه الحاسبة باستخدام HTML وCSS وJavaScript - تعمل على GitHub</p>
            <p>© 2023 حاسبة تطور رأس المال في التداول</p>
        </footer>
    </div>
    
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <script>
        document.addEventListener('DOMContentLoaded', function() {
            const calculateBtn = document.getElementById('calculateBtn');
            const ctx = document.getElementById('growthChart').getContext('2d');
            let growthChart;
            
            // Initialize chart
            function initChart() {
                growthChart = new Chart(ctx, {
                    type: 'line',
                    data: {
                        labels: ['0', '10', '20', '30', '40', '50'],
                        datasets: [{
                            label: 'رأس المال',
                            data: [10000, 10830, 11730, 12708, 13764, 14913],
                            borderColor: '#3498db',
                            backgroundColor: 'rgba(52, 152, 219, 0.1)',
                            borderWidth: 3,
                            pointBackgroundColor: '#fff',
                            pointRadius: 5,
                            pointHoverRadius: 7,
                            fill: true,
                            tension: 0.3
                        }]
                    },
                    options: {
                        responsive: true,
                        maintainAspectRatio: false,
                        plugins: {
                            legend: {
                                labels: {
                                    color: '#ecf0f1',
                                    font: {
                                        size: 14
                                    }
                                }
                            },
                            tooltip: {
                                backgroundColor: 'rgba(44, 62, 80, 0.9)',
                                titleColor: '#ecf0f1',
                                bodyColor: '#ecf0f1',
                                titleFont: {
                                    size: 16
                                },
                                bodyFont: {
                                    size: 14
                                },
                                padding: 12,
                                displayColors: false
                            }
                        },
                        scales: {
                            x: {
                                title: {
                                    display: true,
                                    text: 'عدد الصفقات',
                                    color: '#bdc3c7',
                                    font: {
                                        size: 14,
                                        weight: 'bold'
                                    }
                                },
                                grid: {
                                    color: 'rgba(255, 255, 255, 0.1)'
                                },
                                ticks: {
                                    color: '#ecf0f1'
                                }
                            },
                            y: {
                                title: {
                                    display: true,
                                    text: 'رأس المال ($)',
                                    color: '#bdc3c7',
                                    font: {
                                        size: 14,
                                        weight: 'bold'
                                    }
                                },
                                grid: {
                                    color: 'rgba(255, 255, 255, 0.1)'
                                },
                                ticks: {
                                    color: '#ecf0f1',
                                    callback: function(value) {
                                        return '$' + value.toLocaleString();
                                    }
                                }
                            }
                        }
                    }
                });
            }
            
            // Initialize the chart
            initChart();
            
            calculateBtn.addEventListener('click', calculate);
            
            // Calculate on page load
            calculate();
            
            function calculate() {
                // Get input values
                const initialCapital = parseFloat(document.getElementById('initialCapital').value) || 10000;
                const winRate = parseFloat(document.getElementById('winRate').value) || 60;
                const profitRate = parseFloat(document.getElementById('profitRate').value) || 2;
                const lossRate = parseFloat(document.getElementById('lossRate').value) || 1;
                const updateInterval = parseInt(document.getElementById('updateInterval').value) || 10;
                const targetCapital = parseFloat(document.getElementById('targetCapital').value) || 15000;
                
                // Convert percentages to decimals
                const winRateDecimal = winRate / 100;
                const profitRateDecimal = profitRate / 100;
                const lossRateDecimal = lossRate / 100;
                
                // Calculate expected return per trade
                const expectedReturn = (winRateDecimal * profitRateDecimal) - ((1 - winRateDecimal) * lossRateDecimal);
                document.getElementById('avgReturn').textContent = (expectedReturn * 100).toFixed(2) + '%';
                
                // Calculate required trades
                let nTrades;
                if (expectedReturn <= 0) {
                    nTrades = '∞ (لا يمكن تحقيق الهدف)';
                } else {
                    nTrades = Math.ceil(Math.log(targetCapital / initialCapital) / Math.log(1 + expectedReturn));
                }
                document.getElementById('tradesRequired').textContent = nTrades;
                
                // Calculate overall growth
                const overallGrowth = ((targetCapital - initialCapital) / initialCapital) * 100;
                document.getElementById('overallGrowth').textContent = overallGrowth.toFixed(2) + '%';
                
                // Calculate capital evolution
                const results = [];
                let tradeCount = 0;
                let currentCapital = initialCapital;
                
                while (tradeCount <= (typeof nTrades === 'number' ? nTrades : 1000)) {
                    results.push({
                        trades: tradeCount,
                        capital: currentCapital,
                        growth: ((currentCapital - initialCapital) / initialCapital) * 100
                    });
                    
                    if (currentCapital >= targetCapital || tradeCount > 1000) break;
                    
                    tradeCount += updateInterval;
                    currentCapital = initialCapital * Math.pow(1 + expectedReturn, tradeCount);
                }
                
                // Update table
                updateTable(results);
                
                // Update chart
                updateChart(results);
            }
            
            function updateTable(results) {
                const tableBody = document.querySelector('#resultsTable tbody');
                tableBody.innerHTML = '';
                
                results.forEach(result => {
                    const row = document.createElement('tr');
                    
                    const tradesCell = document.createElement('td');
                    tradesCell.textContent = result.trades;
                    
                    const capitalCell = document.createElement('td');
                    capitalCell.textContent = result.capital.toLocaleString('en-US', {
                        maximumFractionDigits: 2,
                        minimumFractionDigits: 2
                    }) + ' $';
                    
                    const growthCell = document.createElement('td');
                    growthCell.textContent = result.growth.toFixed(2) + '%';
                    growthCell.className = result.growth >= 0 ? 'positive' : 'negative';
                    
                    row.appendChild(tradesCell);
                    row.appendChild(capitalCell);
                    row.appendChild(growthCell);
                    
                    tableBody.appendChild(row);
                });
            }
            
            function updateChart(results) {
                const labels = results.map(r => r.trades);
                const data = results.map(r => r.capital);
                
                growthChart.data.labels = labels;
                growthChart.data.datasets[0].data = data;
                growthChart.update();
            }
            
            // Handle mobile menu button
            const mobileMenuBtn = document.querySelector('.mobile-menu-btn');
            mobileMenuBtn.addEventListener('click', function() {
                alert('استخدم زر الحساب لتحديث النتائج. قم بتعديل البيانات ثم اضغط "حساب تطور رأس المال"');
            });
            
            // Prevent zooming on mobile
            document.addEventListener('touchmove', function(event) {
                if (event.scale !== 1) { event.preventDefault(); }
            }, { passive: false });
        });
    </script>
</body>
</html>

