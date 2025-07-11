
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>حاسبة تطور رأس المال في التداول</title>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 20px;
            background-color: #f5f5f5;
            color: #333;
        }
        .container {
            max-width: 1000px;
            margin: 0 auto;
            background-color: white;
            padding: 20px;
            border-radius: 8px;
            box-shadow: 0 0 10px rgba(0,0,0,0.1);
        }
        h1 {
            color: #2c3e50;
            text-align: center;
            margin-bottom: 30px;
        }
        .input-section {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 15px;
            margin-bottom: 20px;
        }
        .input-group {
            margin-bottom: 15px;
        }
        label {
            display: block;
            margin-bottom: 5px;
            font-weight: bold;
        }
        input {
            width: 100%;
            padding: 8px;
            border: 1px solid #ddd;
            border-radius: 4px;
            box-sizing: border-box;
        }
        button {
            background-color: #3498db;
            color: white;
            border: none;
            padding: 10px 15px;
            border-radius: 4px;
            cursor: pointer;
            font-size: 16px;
            display: block;
            margin: 20px auto;
            width: 200px;
        }
        button:hover {
            background-color: #2980b9;
        }
        .results {
            margin-top: 30px;
            padding: 15px;
            background-color: #f9f9f9;
            border-radius: 4px;
        }
        .results h2 {
            color: #2c3e50;
            border-bottom: 1px solid #eee;
            padding-bottom: 10px;
        }
        table {
            width: 100%;
            border-collapse: collapse;
            margin: 20px 0;
        }
        th, td {
            border: 1px solid #ddd;
            padding: 8px;
            text-align: center;
        }
        th {
            background-color: #f2f2f2;
        }
        tr:nth-child(even) {
            background-color: #f9f9f9;
        }
        .chart-container {
            position: relative;
            height: 400px;
            margin: 30px 0;
        }
        .summary {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 15px;
            margin-bottom: 20px;
        }
        .summary-item {
            background-color: #e8f4fc;
            padding: 15px;
            border-radius: 4px;
            text-align: center;
        }
        .summary-item h3 {
            margin-top: 0;
            color: #2c3e50;
        }
        .summary-value {
            font-size: 24px;
            font-weight: bold;
            color: #3498db;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>حاسبة تطور رأس المال في التداول</h1>
        
        <div class="input-section">
            <div class="input-group">
                <label for="initialCapital">رأس المال الأولي</label>
                <input type="number" id="initialCapital" placeholder="أدخل رأس المال الأولي">
            </div>
            
            <div class="input-group">
                <label for="winRate">نسبة الصفقات الرابحة (%)</label>
                <input type="number" id="winRate" placeholder="أدخل نسبة الصفقات الرابحة" min="0" max="100">
            </div>
            
            <div class="input-group">
                <label for="profitRate">معدل الربح لكل صفقة (%)</label>
                <input type="number" id="profitRate" placeholder="أدخل معدل الربح لكل صفقة">
            </div>
            
            <div class="input-group">
                <label for="lossRate">معدل الخسارة لكل صفقة (%)</label>
                <input type="number" id="lossRate" placeholder="أدخل معدل الخسارة لكل صفقة">
            </div>
            
            <div class="input-group">
                <label for="updateInterval">عدد الصفقات في كل تحديث عرض</label>
                <input type="number" id="updateInterval" placeholder="أدخل عدد الصفقات للتحديث" min="1">
            </div>
            
            <div class="input-group">
                <label for="targetCapital">الهدف النهائي</label>
                <input type="number" id="targetCapital" placeholder="أدخل الهدف النهائي">
            </div>
        </div>
        
        <button onclick="calculateGrowth()">حساب التطور</button>
        
        <div id="resultsSection" class="results" style="display: none;">
            <h2>النتائج</h2>
            
            <div class="summary">
                <div class="summary-item">
                    <h3>متوسط العائد لكل صفقة</h3>
                    <div class="summary-value" id="avgReturn">0%</div>
                </div>
                <div class="summary-item">
                    <h3>عدد الصفقات المطلوبة</h3>
                    <div class="summary-value" id="totalTrades">0</div>
                </div>
                <div class="summary-item">
                    <h3>معدل النمو الإجمالي</h3>
                    <div class="summary-value" id="totalGrowth">0%</div>
                </div>
            </div>
            
            <h3>تطور رأس المال</h3>
            <div class="chart-container">
                <canvas id="capitalChart"></canvas>
            </div>
            
            <h3>تفاصيل التطور</h3>
            <table id="resultsTable">
                <thead>
                    <tr>
                        <th>عدد الصفقات</th>
                        <th>رأس المال</th>
                        <th>التغير</th>
                        <th>نسبة النمو</th>
                    </tr>
                </thead>
                <tbody id="resultsBody">
                </tbody>
            </table>
        </div>
    </div>

    <script>
        let capitalChart = null;
        
        function calculateGrowth() {
            // الحصول على قيم المدخلات
            const initialCapital = parseFloat(document.getElementById('initialCapital').value);
            const winRate = parseFloat(document.getElementById('winRate').value) / 100;
            const profitRate = parseFloat(document.getElementById('profitRate').value) / 100;
            const lossRate = parseFloat(document.getElementById('lossRate').value) / 100;
            const updateInterval = parseInt(document.getElementById('updateInterval').value);
            const targetCapital = parseFloat(document.getElementById('targetCapital').value);
            
            // التحقق من صحة المدخلات
            if (isNaN(initialCapital) {
                alert("الرجاء إدخال رأس المال الأولي");
                return;
            }
            
            // حساب متوسط العائد لكل صفقة
            const avgReturn = (winRate * profitRate) - ((1 - winRate) * lossRate);
            
            // حساب عدد الصفقات المطلوبة للوصول إلى الهدف
            const totalTrades = Math.ceil(Math.log(targetCapital / initialCapital) / Math.log(1 + avgReturn));
            
            // عرض النتائج الأساسية
            document.getElementById('avgReturn').textContent = (avgReturn * 100).toFixed(2) + "%";
            document.getElementById('totalTrades').textContent = totalTrades;
            
            // محاكاة تطور رأس المال
            let capital = initialCapital;
            let trades = 0;
            const dataPoints = [];
            const tableData = [];
            
            // إضافة النقطة الأولى
            dataPoints.push({ trades: 0, capital: initialCapital });
            tableData.push({ trades: 0, capital: initialCapital, change: 0, growth: 0 });
            
            while (trades < totalTrades) {
                const tradesInThisStep = Math.min(updateInterval, totalTrades - trades);
                
                for (let i = 0; i < tradesInThisStep; i++) {
                    const isWin = Math.random() < winRate;
                    const change = isWin ? capital * profitRate : -capital * lossRate;
                    capital += change;
                }
                
                trades += tradesInThisStep;
                
                const change = capital - dataPoints[dataPoints.length - 1].capital;
                const growth = (capital / initialCapital - 1) * 100;
                
                dataPoints.push({ trades, capital });
                tableData.push({ trades, capital, change, growth });
            }
            
            // حساب معدل النمو الإجمالي
            const totalGrowth = ((capital / initialCapital) - 1) * 100;
            document.getElementById('totalGrowth').textContent = totalGrowth.toFixed(2) + "%";
            
            // عرض البيانات في الجدول
            const resultsBody = document.getElementById('resultsBody');
            resultsBody.innerHTML = '';
            
            tableData.forEach(point => {
                const row = document.createElement('tr');
                
                const tradesCell = document.createElement('td');
                tradesCell.textContent = point.trades;
                row.appendChild(tradesCell);
                
                const capitalCell = document.createElement('td');
                capitalCell.textContent = point.capital.toFixed(2);
                row.appendChild(capitalCell);
                
                const changeCell = document.createElement('td');
                changeCell.textContent = point.change.toFixed(2);
                changeCell.style.color = point.change >= 0 ? 'green' : 'red';
                row.appendChild(changeCell);
                
                const growthCell = document.createElement('td');
                growthCell.textContent = point.growth.toFixed(2) + "%";
                growthCell.style.color = point.growth >= 0 ? 'green' : 'red';
                row.appendChild(growthCell);
                
                resultsBody.appendChild(row);
            });
            
            // عرض القسم النتائج
            document.getElementById('resultsSection').style.display = 'block';
            
            // رسم المخطط البياني
            drawChart(dataPoints);
        }
        
        function drawChart(dataPoints) {
            const ctx = document.getElementById('capitalChart').getContext('2d');
            
            // إذا كان هناك مخطط موجود، قم بتدميره أولاً
            if (capitalChart) {
                capitalChart.destroy();
            }
            
            capitalChart = new Chart(ctx, {
                type: 'line',
                data: {
                    labels: dataPoints.map(point => point.trades),
                    datasets: [{
                        label: 'رأس المال',
                        data: dataPoints.map(point => point.capital),
                        borderColor: '#3498db',
                        backgroundColor: 'rgba(52, 152, 219, 0.1)',
                        borderWidth: 2,
                        fill: true,
                        tension: 0.1
                    }]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    plugins: {
                        title: {
                            display: true,
                            text: 'تطور رأس المال مع عدد الصفقات',
                            font: {
                                size: 16
                            }
                        },
                        tooltip: {
                            callbacks: {
                                label: function(context) {
                                    return 'رأس المال: ' + context.parsed.y.toFixed(2);
                                }
                            }
                        }
                    },
                    scales: {
                        x: {
                            title: {
                                display: true,
                                text: 'عدد الصفقات'
                            }
                        },
                        y: {
                            title: {
                                display: true,
                                text: 'رأس المال'
                            },
                            beginAtZero: false
                        }
                    }
                }
            });
        }
    </script>
</body>
</html>
