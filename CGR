

<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>حاسبة تطور رأس المال في التداول</title>
    <style>
        :root {
            --primary: #2c3e50;
            --secondary: #3498db;
            --success: #27ae60;
            --warning: #f39c12;
            --danger: #e74c3c;
            --light: #27ae60;
            --dark: #2c3e50;
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
            padding: 20px;
            line-height: 1.6;
        }
        
        .container {
            max-width: 1200px;
            margin: 0 auto;
        }
        
        header {
            text-align: center;
            padding: 20px 0;
            margin-bottom: 30px;
            background: rgba(0, 0, 0, 0.3);
            border-radius: 10px;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.3);
        }
        
        header h1 {
            font-size: 2.5rem;
            margin-bottom: 10px;
            color: var(--light);
            text-shadow: 0 2px 4px rgba(0, 0, 0, 0.5);
        }
        
        header p {
            font-size: 1.2rem;
            max-width: 800px;
            margin: 0 auto;
            color: #bdc3c7;
        }
        
        .main-content {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 30px;
            margin-bottom: 40px;
        }
        
        @media (max-width: 900px) {
            .main-content {
                grid-template-columns: 1fr;
            }
        }
        
        .card {
            background: rgba(44, 62, 80, 0.7);
            border-radius: 10px;
            padding: 25px;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.3);
            transition: transform 0.3s ease, box-shadow 0.3s ease;
            border: 1px solid rgba(255, 255, 255, 0.1);
        }
        
        .card:hover {
            transform: translateY(-5px);
            box-shadow: 0 10px 25px rgba(0, 0, 0, 0.4);
        }
        
        .card-title {
            font-size: 1.5rem;
            margin-bottom: 20px;
            padding-bottom: 15px;
            border-bottom: 2px solid var(--secondary);
            color: var(--light);
        }
        
        .input-group {
            margin-bottom: 20px;
        }
        
        label {
            display: block;
            margin-bottom: 8px;
            font-weight: 500;
            color: #bdc3c7;
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
            padding: 14px 25px;
            border-radius: 6px;
            cursor: pointer;
            font-size: 1.1rem;
            font-weight: 600;
            transition: all 0.3s ease;
            width: 100%;
            margin-top: 10px;
            letter-spacing: 1px;
        }
        
        button:hover {
            background: #2980b9;
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.3);
        }
        
        .results-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 20px;
            margin-top: 25px;
        }
        
        .result-box {
            background: rgba(0, 0, 0, 0.3);
            border-radius: 8px;
            padding: 20px;
            text-align: center;
            border: 1px solid rgba(255, 255, 255, 0.1);
        }
        
        .result-value {
            font-size: 2rem;
            font-weight: 700;
            margin: 10px 0;
            color: var(--success);
        }
        
        .result-label {
            font-size: 1.1rem;
            color: #bdc3c7;
        }
        
        table {
            width: 100%;
            border-collapse: collapse;
            margin-top: 20px;
            background: rgba(0, 0, 0, 0.2);
            border-radius: 8px;
            overflow: hidden;
        }
        
        th, td {
            padding: 15px;
            text-align: center;
            border-bottom: 1px solid rgba(255, 255, 255, 0.1);
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
            margin-top: 30px;
        }
        
        footer {
            text-align: center;
            padding: 20px;
            margin-top: 40px;
            color: #7f8c8d;
            border-top: 1px solid rgba(255, 255, 255, 0.1);
        }
        
        .info-icon {
            display: inline-block;
            width: 18px;
            height: 18px;
            background: var(--secondary);
            color: white;
            border-radius: 50%;
            text-align: center;
            line-height: 18px;
            font-size: 12px;
            margin-left: 5px;
            cursor: help;
        }
    </style>
</head>
<body>
    <div class="container">
        <header>
            <h1>حاسبة تطور رأس المال في التداول</h1>
            <p>أدخل بيانات التداول الخاصة بك لحساب معدل نمو رأس المال المتوقع بناءً على نسبة الصفقات الرابحة والخاسرة</p>
        </header>
        
        <div class="main-content">
            <div class="card">
                <h2 class="card-title">بيانات التداول</h2>
                
                <div class="input-group">
                    <label for="initialCapital">رأس المال الأولي ($)</label>
                    <input type="number" id="initialCapital" value="" min="1">
                </div>
                
                <div class="input-group">
                    <label for="winRate">نسبة الصفقات الرابحة (%)</label>
                    <input type="number" id="winRate" value="" min="0" max="100" step="1">
                </div>
                
                <div class="input-group">
                    <label for="profitRate">معدل الربح لكل صفقة (% من رأس المال)</label>
                    <input type="number" id="profitRate" value="" min="0" step="0.1">
                </div>
                
                <div class="input-group">
                    <label for="lossRate">معدل الخسارة لكل صفقة (% من رأس المال)</label>
                    <input type="number" id="lossRate" value="" min="0" step="0.1">
                </div>
                
                <div class="input-group">
                    <label for="updateInterval">عدد الصفقات في كل يوم</label>
                    <input type="number" id="updateInterval" value="" min="1">
                </div>
                
                <div class="input-group">
                    <label for="targetCapital">الهدف النهائي ($)</label>
                    <input type="number" id="targetCapital" value="" min="1">
                </div>
                
                <button id="calculateBtn">حساب تطور رأس المال</button>
            </div>
            
            <div class="card">
                <h2 class="card-title">النتائج</h2>
                
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
                
                <h3 style="margin-top: 30px; margin-bottom: 15px;">تطور رأس المال</h3>
                
                <div class="table-responsive">
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
            <h2 class="card-title">مخطط تطور رأس المال</h2>
            <div class="chart-container">
                <canvas id="growthChart"></canvas>
            </div>
        </div>
        
        <footer>
            <p>DIRECTED BY ALI MAHMOUD</p>
            <p>حاسبة تطور رأس المال في التداول</p>
        </footer>
    </div>
    
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <script>
        document.addEventListener('DOMContentLoaded', function() {
            const calculateBtn = document.getElementById('calculateBtn');
            const ctx = document.getElementById('growthChart').getContext('2d');
            
            // نموذج بيانات الرسم البياني
            let growthChart = new Chart(ctx, {
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
            
            calculateBtn.addEventListener('click', calculate);
            
            // حساب النتائج عند التحميل
            calculate();
            
            function calculate() {
                // الحصول على القيم من حقول الإدخال
                const initialCapital = parseFloat(document.getElementById('initialCapital').value);
                const winRate = parseFloat(document.getElementById('winRate').value) / 100;
                const profitRate = parseFloat(document.getElementById('profitRate').value) / 100;
                const lossRate = parseFloat(document.getElementById('lossRate').value) / 100;
                const updateInterval = parseInt(document.getElementById('updateInterval').value);
                const targetCapital = parseFloat(document.getElementById('targetCapital').value);
                
                // حساب متوسط العائد لكل صفقة
                const expectedReturn = (winRate * profitRate) - ((1 - winRate) * lossRate);
                document.getElementById('avgReturn').textContent = (expectedReturn * 100).toFixed(2) + '%';
                
                // حساب عدد الصفقات المطلوبة
                let nTrades;
                if (expectedReturn <= 0) {
                    nTrades = '∞ (لا يمكن تحقيق الهدف)';
                } else {
                    nTrades = Math.ceil(Math.log(targetCapital / initialCapital) / Math.log(1 + expectedReturn));
                }
                document.getElementById('tradesRequired').textContent = nTrades;
                
                // حساب معدل النمو الإجمالي
                const overallGrowth = ((targetCapital - initialCapital) / initialCapital) * 100;
                document.getElementById('overallGrowth').textContent = overallGrowth.toFixed(2) + '%';
                
                // حساب تطور رأس المال
                const results = [];
                let tradeCount = 0;
                let currentCapital = initialCapital;
                
                while (tradeCount <= (typeof nTrades === 'number' ? nTrades : 1000)) {
                    // إضافة النتيجة الحالية
                    results.push({
                        trades: tradeCount,
                        capital: currentCapital,
                        growth: ((currentCapital - initialCapital) / initialCapital) * 100
                    });
                    
                    // التوقف عند الوصول أو تجاوز الهدف
                    if (currentCapital >= targetCapital || tradeCount > 1000) break;
                    
                    // الانتقال إلى الدفعة التالية من الصفقات
                    tradeCount += updateInterval;
                    
                    // حساب رأس المال الجديد
                    currentCapital = initialCapital * Math.pow(1 + expectedReturn, tradeCount);
                }
                
                // تحديث الجدول
                updateTable(results);
                
                // تحديث الرسم البياني
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
        });
    </script>
</body>
</html>
