
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>حاسبة تطور رأس المال في التداول</title>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <style>
        :root {
            --primary-color: #4361ee;
            --secondary-color: #3f37c9;
            --accent-color: #4895ef;
            --light-color: #f8f9fa;
            --dark-color: #212529;
            --success-color: #4cc9f0;
            --danger-color: #f72585;
        }
        
        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        
        body {
            background-color: #f5f7fa;
            color: var(--dark-color);
            line-height: 1.6;
        }
        
        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 2rem;
        }
        
        header {
            text-align: center;
            margin-bottom: 2rem;
            padding: 1rem;
            background: linear-gradient(135deg, var(--primary-color), var(--secondary-color));
            color: white;
            border-radius: 10px;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
        }
        
        h1 {
            font-size: 2rem;
            margin-bottom: 0.5rem;
        }
        
        .calculator {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 2rem;
            margin-bottom: 2rem;
        }
        
        @media (max-width: 768px) {
            .calculator {
                grid-template-columns: 1fr;
            }
        }
        
        .input-section, .result-section {
            background-color: white;
            padding: 1.5rem;
            border-radius: 10px;
            box-shadow: 0 2px 4px rgba(0, 0, 0, 0.05);
        }
        
        .form-group {
            margin-bottom: 1.5rem;
        }
        
        label {
            display: block;
            margin-bottom: 0.5rem;
            font-weight: 600;
            color: var(--dark-color);
        }
        
        input {
            width: 100%;
            padding: 0.75rem;
            border: 1px solid #ddd;
            border-radius: 5px;
            font-size: 1rem;
            transition: border-color 0.3s;
        }
        
        input:focus {
            outline: none;
            border-color: var(--accent-color);
            box-shadow: 0 0 0 2px rgba(67, 97, 238, 0.2);
        }
        
        button {
            background-color: var(--primary-color);
            color: white;
            border: none;
            padding: 0.75rem 1.5rem;
            border-radius: 5px;
            cursor: pointer;
            font-size: 1rem;
            font-weight: 600;
            transition: background-color 0.3s;
            width: 100%;
        }
        
        button:hover {
            background-color: var(--secondary-color);
        }
        
        .result-card {
            background-color: white;
            padding: 1rem;
            border-radius: 8px;
            margin-bottom: 1rem;
            box-shadow: 0 2px 4px rgba(0, 0, 0, 0.05);
            border-left: 4px solid var(--accent-color);
        }
        
        .result-title {
            font-size: 0.9rem;
            color: #6c757d;
            margin-bottom: 0.5rem;
        }
        
        .result-value {
            font-size: 1.5rem;
            font-weight: 700;
            color: var(--primary-color);
        }
        
        .chart-container {
            background-color: white;
            padding: 1.5rem;
            border-radius: 10px;
            box-shadow: 0 2px 4px rgba(0, 0, 0, 0.05);
            margin-top: 2rem;
        }
        
        .positive {
            color: var(--success-color);
        }
        
        .negative {
            color: var(--danger-color);
        }
    </style>
</head>
<body>
    <div class="container">
        <header>
            <h1>حاسبة تطور رأس المال في التداول</h1>
            <p>قم بإدخال بيانات التداول الخاصة بك لرؤية تطور رأس المال المتوقع</p>
        </header>
        
        <div class="calculator">
            <div class="input-section">
                <div class="form-group">
                    <label for="initialCapital">رأس المال الأولي ($)</label>
                    <input type="number" id="initialCapital" placeholder="أدخل رأس المال الأولي">
                </div>
                
                <div class="form-group">
                    <label for="winRate">نسبة الصفقات الرابحة (%)</label>
                    <input type="number" id="winRate" placeholder="أدخل نسبة الصفقات الرابحة" min="0" max="100">
                </div>
                
                <div class="form-group">
                    <label for="profitRate">معدل الربح لكل صفقة (%)</label>
                    <input type="number" id="profitRate" placeholder="أدخل معدل الربح لكل صفقة">
                </div>
                
                <div class="form-group">
                    <label for="lossRate">معدل الخسارة لكل صفقة (%)</label>
                    <input type="number" id="lossRate" placeholder="أدخل معدل الخسارة لكل صفقة">
                </div>
                
                <div class="form-group">
                    <label for="numTrades">عدد الصفقات لكل تحديث</label>
                    <input type="number" id="numTrades" placeholder="أدخل عدد الصفقات">
                </div>
                
                <div class="form-group">
                    <label for="target">الهدف النهائي ($)</label>
                    <input type="number" id="target" placeholder="أدخل الهدف النهائي">
                </div>
                
                <button id="calculateBtn">حساب التطور</button>
            </div>
            
            <div class="result-section">
                <h2 style="margin-bottom: 1.5rem; color: var(--secondary-color);">النتائج</h2>
                
                <div class="result-card">
                    <div class="result-title">متوسط العائد لكل صفقة</div>
                    <div class="result-value" id="avgReturn">-</div>
                </div>
                
                <div class="result-card">
                    <div class="result-title">عدد الصفقات المطلوبة</div>
                    <div class="result-value" id="requiredTrades">-</div>
                </div>
                
                <div class="result-card">
                    <div class="result-title">معدل النمو الإجمالي</div>
                    <div class="result-value" id="growthRate">-</div>
                </div>
            </div>
        </div>
        
        <div class="chart-container">
            <h2 style="margin-bottom: 1rem; color: var(--secondary-color);">مخطط تطور رأس المال</h2>
            <canvas id="capitalChart"></canvas>
        </div>
    </div>

    <script>
        document.addEventListener('DOMContentLoaded', function() {
            const calculateBtn = document.getElementById('calculateBtn');
            calculateBtn.addEventListener('click', calculateGrowth);
            
            let capitalChart = null;
            
            function calculateGrowth() {
                // Get input values
                const initialCapital = parseFloat(document.getElementById('initialCapital').value);
                const winRate = parseFloat(document.getElementById('winRate').value) / 100;
                const profitRate = parseFloat(document.getElementById('profitRate').value) / 100;
                const lossRate = parseFloat(document.getElementById('lossRate').value) / 100;
                const numTrades = parseInt(document.getElementById('numTrades').value);
                const target = parseFloat(document.getElementById('target').value);
                
                // Validate inputs
                if (isNaN(initialCapital) || isNaN(winRate) || isNaN(profitRate) || 
                    isNaN(lossRate) || isNaN(numTrades) || isNaN(target)) {
                    alert('الرجاء إدخال جميع القيم المطلوبة');
                    return;
                }
                
                // Calculate average return per trade
                const avgReturn = (winRate * profitRate) - ((1 - winRate) * lossRate);
                document.getElementById('avgReturn').textContent = (avgReturn * 100).toFixed(2) + '%';
                document.getElementById('avgReturn').className = avgReturn >= 0 ? 'result-value positive' : 'result-value negative';
                
                // Calculate required trades to reach target
                const requiredTrades = Math.ceil(Math.log(target / initialCapital) / Math.log(1 + avgReturn));
                document.getElementById('requiredTrades').textContent = requiredTrades;
                
                // Calculate total growth rate
                const growthRate = ((target - initialCapital) / initialCapital) * 100;
                document.getElementById('growthRate').textContent = growthRate.toFixed(2) + '%';
                document.getElementById('growthRate').className = growthRate >= 0 ? 'result-value positive' : 'result-value negative';
                
                // Generate capital growth data for chart
                const capitalData = [];
                const tradeNumbers = [];
                let currentCapital = initialCapital;
                
                // Calculate up to required trades or 1000 trades max (for performance)
                const maxTrades = Math.min(requiredTrades, 1000);
                
                for (let i = 0; i <= maxTrades; i += Math.max(1, Math.floor(maxTrades / 100))) {
                    tradeNumbers.push(i);
                    capitalData.push(currentCapital);
                    
                    // Calculate next capital value
                    if (i < maxTrades) {
                        const tradesInStep = Math.min(numTrades, maxTrades - i);
                        currentCapital = initialCapital * Math.pow(1 + avgReturn, i + tradesInStep);
                    }
                }
                
                // Add final target point if not already included
                if (tradeNumbers[tradeNumbers.length - 1] < requiredTrades) {
                    tradeNumbers.push(requiredTrades);
                    capitalData.push(target);
                }
                
                // Update or create chart
                updateChart(tradeNumbers, capitalData, initialCapital, target);
            }
            
            function updateChart(tradeNumbers, capitalData, initialCapital, target) {
                const ctx = document.getElementById('capitalChart').getContext('2d');
                
                if (capitalChart) {
                    capitalChart.destroy();
                }
                
                capitalChart = new Chart(ctx, {
                    type: 'line',
                    data: {
                        labels: tradeNumbers,
                        datasets: [{
                            label: 'رأس المال',
                            data: capitalData,
                            borderColor: '#4361ee',
                            backgroundColor: 'rgba(67, 97, 238, 0.1)',
                            borderWidth: 3,
                            fill: true,
                            tension: 0.4
                        },
                        {
                            label: 'رأس المال الأولي',
                            data: Array(tradeNumbers.length).fill(initialCapital),
                            borderColor: '#6c757d',
                            borderWidth: 1,
                            borderDash: [5, 5],
                            pointRadius: 0
                        },
                        {
                            label: 'الهدف النهائي',
                            data: Array(tradeNumbers.length).fill(target),
                            borderColor: '#4cc9f0',
                            borderWidth: 1,
                            borderDash: [5, 5],
                            pointRadius: 0
                        }]
                    },
                    options: {
                        responsive: true,
                        plugins: {
                            legend: {
                                position: 'top',
                                rtl: true
                            },
                            tooltip: {
                                callbacks: {
                                    label: function(context) {
                                        return context.dataset.label + ': ' + context.parsed.y.toFixed(2) + '$';
                                    }
                                }
                            }
                        },
                        scales: {
                            x: {
                                title: {
                                    display: true,
                                    text: 'عدد الصفقات',
                                    font: {
                                        weight: 'bold'
                                    }
                                }
                            },
                            y: {
                                title: {
                                    display: true,
                                    text: 'رأس المال ($)',
                                    font: {
                                        weight: 'bold'
                                    }
                                },
                                beginAtZero: false
                            }
                        },
                        interaction: {
                            intersect: false,
                            mode: 'index'
                        }
                    }
                });
            }
        });
    </script>
</body>
</html>
