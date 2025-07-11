
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>حاسبة تطور رأس المال في التداول</title>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <link href="https://fonts.googleapis.com/css2?family=Tajawal:wght@400;500;700&display=swap" rel="stylesheet">
    <style>
        :root {
            --primary: #4361ee;
            --secondary: #3f37c9;
            --accent: #4895ef;
            --success: #4cc9f0;
            --danger: #f72585;
            --light: #f8f9fa;
            --dark: #212529;
            --gray: #6c757d;
            --white: #ffffff;
        }
        
        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
        }
        
        body {
            font-family: 'Tajawal', sans-serif;
            background-color: #f5f7fa;
            color: var(--dark);
            line-height: 1.6;
        }
        
        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 20px;
        }
        
        header {
            text-align: center;
            margin-bottom: 30px;
            padding: 20px 0;
            background: linear-gradient(135deg, var(--primary), var(--secondary));
            color: white;
            border-radius: 10px;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
        }
        
        h1 {
            font-size: 2rem;
            font-weight: 700;
            margin-bottom: 10px;
        }
        
        .card {
            background-color: var(--white);
            border-radius: 10px;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.05);
            padding: 25px;
            margin-bottom: 25px;
        }
        
        .card-title {
            font-size: 1.3rem;
            color: var(--primary);
            margin-bottom: 20px;
            padding-bottom: 10px;
            border-bottom: 2px solid #eee;
        }
        
        .form-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 20px;
        }
        
        .form-group {
            margin-bottom: 15px;
        }
        
        label {
            display: block;
            margin-bottom: 8px;
            font-weight: 500;
            color: var(--dark);
        }
        
        input {
            width: 100%;
            padding: 12px 15px;
            border: 1px solid #ddd;
            border-radius: 8px;
            font-family: 'Tajawal', sans-serif;
            font-size: 1rem;
            transition: all 0.3s ease;
        }
        
        input:focus {
            border-color: var(--accent);
            outline: none;
            box-shadow: 0 0 0 3px rgba(67, 97, 238, 0.2);
        }
        
        .btn {
            display: inline-block;
            background: linear-gradient(to right, var(--primary), var(--accent));
            color: white;
            border: none;
            padding: 12px 30px;
            border-radius: 8px;
            font-size: 1rem;
            font-weight: 500;
            cursor: pointer;
            transition: all 0.3s ease;
            text-align: center;
            margin: 20px auto;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
        }
        
        .btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 6px 8px rgba(0, 0, 0, 0.15);
        }
        
        .btn:active {
            transform: translateY(0);
        }
        
        .results-section {
            display: none;
        }
        
        .summary-cards {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 20px;
            margin-bottom: 30px;
        }
        
        .summary-card {
            background: white;
            border-radius: 10px;
            padding: 20px;
            text-align: center;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.05);
            transition: transform 0.3s ease;
        }
        
        .summary-card:hover {
            transform: translateY(-5px);
        }
        
        .summary-card h3 {
            color: var(--gray);
            font-size: 1rem;
            margin-bottom: 10px;
        }
        
        .summary-value {
            font-size: 1.8rem;
            font-weight: 700;
            color: var(--primary);
        }
        
        .positive {
            color: var(--success);
        }
        
        .negative {
            color: var(--danger);
        }
        
        .chart-container {
            position: relative;
            height: 400px;
            margin: 30px 0;
            background: white;
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.05);
        }
        
        table {
            width: 100%;
            border-collapse: collapse;
            margin: 20px 0;
            background: white;
            border-radius: 10px;
            overflow: hidden;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.05);
        }
        
        th, td {
            padding: 12px 15px;
            text-align: center;
            border-bottom: 1px solid #eee;
        }
        
        th {
            background-color: var(--primary);
            color: white;
            font-weight: 500;
        }
        
        tr:nth-child(even) {
            background-color: #f8f9fa;
        }
        
        tr:hover {
            background-color: #f1f3ff;
        }
        
        @media (max-width: 768px) {
            .form-grid {
                grid-template-columns: 1fr;
            }
            
            .summary-cards {
                grid-template-columns: 1fr;
            }
            
            .chart-container {
                height: 300px;
            }
            
            h1 {
                font-size: 1.5rem;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <header>
            <h1>حاسبة تطور رأس المال في التداول</h1>
            <p>أدخل بياناتك لمعرفة تطور رأس مالك مع مرور الوقت</p>
        </header>
        
        <div class="card">
            <h2 class="card-title">بيانات الإدخال</h2>
            <div class="form-grid">
                <div class="form-group">
                    <label for="initialCapital">رأس المال الأولي</label>
                    <input type="number" id="initialCapital" placeholder="مثال: 10000">
                </div>
                
                <div class="form-group">
                    <label for="winRate">نسبة الصفقات الرابحة (%)</label>
                    <input type="number" id="winRate" placeholder="مثال: 60" min="0" max="100">
                </div>
                
                <div class="form-group">
                    <label for="profitRate">معدل الربح لكل صفقة (%)</label>
                    <input type="number" id="profitRate" placeholder="مثال: 5">
                </div>
                
                <div class="form-group">
                    <label for="lossRate">معدل الخسارة لكل صفقة (%)</label>
                    <input type="number" id="lossRate" placeholder="مثال: 2">
                </div>
                
                <div class="form-group">
                    <label for="updateInterval">عدد الصفقات في كل تحديث</label>
                    <input type="number" id="updateInterval" placeholder="مثال: 10" min="1">
                </div>
                
                <div class="form-group">
                    <label for="targetCapital">الهدف النهائي</label>
                    <input type="number" id="targetCapital" placeholder="مثال: 20000">
                </div>
            </div>
            
            <button class="btn" onclick="calculateGrowth()">حساب التطور</button>
        </div>
        
        <div id="resultsSection" class="results-section">
            <div class="card">
                <h2 class="card-title">النتائج الرئيسية</h2>
                
                <div class="summary-cards">
                    <div class="summary-card">
                        <h3>متوسط العائد لكل صفقة</h3>
                        <div class="summary-value" id="avgReturn">0%</div>
                    </div>
                    
                    <div class="summary-card">
                        <h3>عدد الصفقات المطلوبة</h3>
                        <div class="summary-value" id="totalTrades">0</div>
                    </div>
                    
                    <div class="summary-card">
                        <h3>معدل النمو الإجمالي</h3>
                        <div class="summary-value" id="totalGrowth">0%</div>
                    </div>
                </div>
                
                <div class="chart-container">
                    <canvas id="capitalChart"></canvas>
                </div>
            </div>
            
            <div class="card">
                <h2 class="card-title">تفاصيل التطور</h2>
                <div style="overflow-x: auto;">
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
            document.getElementById('avgReturn').className = avgReturn >= 0 ? "summary-value positive" : "summary-value negative";
            
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
            document.getElementById('totalGrowth').className = totalGrowth >= 0 ? "summary-value positive" : "summary-value negative";
            
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
                changeCell.className = point.change >= 0 ? "positive" : "negative";
                row.appendChild(changeCell);
                
                const growthCell = document.createElement('td');
                growthCell.textContent = point.growth.toFixed(2) + "%";
                growthCell.className = point.growth >= 0 ? "positive" : "negative";
                row.appendChild(growthCell);
                
                resultsBody.appendChild(row);
            });
            
            // عرض القسم النتائج
            document.getElementById('resultsSection').style.display = 'block';
            
            // رسم المخطط البياني
            drawChart(dataPoints);
            
            // التمرير إلى قسم النتائج
            document.getElementById('resultsSection').scrollIntoView({ behavior: 'smooth' });
        }
        
        function drawChart(dataPoints) {
            const ctx = document.getElementById('capitalChart').getContext('2d');
            
            // إذا كان هناك مخطط موجود، قم بتدميره أولاً
            if (capitalChart) {
                capitalChart.destroy();
            }
            
            // تحديد لون الخط بناءً على النتيجة النهائية
            const finalGrowth = ((dataPoints[dataPoints.length-1].capital / dataPoints[0].capital) - 1) * 100;
            const lineColor = finalGrowth >= 0 ? '#4cc9f0' : '#f72585';
            
            capitalChart = new Chart(ctx, {
                type: 'line',
                data: {
                    labels: dataPoints.map(point => point.trades),
                    datasets: [{
                        label: 'رأس المال',
                        data: dataPoints.map(point => point.capital),
                        borderColor: lineColor,
                        backgroundColor: finalGrowth >= 0 ? 'rgba(76, 201, 240, 0.1)' : 'rgba(247, 37, 133, 0.1)',
                        borderWidth: 3,
                        fill: true,
                        tension: 0.4,
                        pointRadius: 0,
                        pointHoverRadius: 5
                    }]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    plugins: {
                        legend: {
                            display: false
                        },
                        tooltip: {
                            callbacks: {
                                label: function(context) {
                                    return 'رأس المال: ' + context.parsed.y.toFixed(2);
                                },
                                afterLabel: function(context) {
                                    const growth = ((context.parsed.y / dataPoints[0].capital) - 1) * 100;
                                    return 'نسبة النمو: ' + growth.toFixed(2) + '%';
                                }
                            }
                        }
                    },
                    scales: {
                        x: {
                            title: {
                                display: true,
                                text: 'عدد الصفقات',
                                color: '#6c757d'
                            },
                            grid: {
                                display: false
                            }
                        },
                        y: {
                            title: {
                                display: true,
                                text: 'رأس المال',
                                color: '#6c757d'
                            },
                            beginAtZero: false,
                            grid: {
                                color: '#eee'
                            }
                        }
                    },
                    interaction: {
                        intersect: false,
                        mode: 'index'
                    }
                }
            });
        }
    </script>
</body>
</html>
