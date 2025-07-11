
<html lang="ar">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>حاسبة تطور رأس المال</title>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <style>
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background-color: #f4f7f6;
            color: #333;
            line-height: 1.6;
            margin: 0;
            padding: 20px;
            direction: rtl; /* Right-to-left for Arabic */
            text-align: right;
        }
        .container {
            max-width: 900px;
            margin: 20px auto;
            background: #fff;
            padding: 30px;
            border-radius: 12px;
            box-shadow: 0 6px 20px rgba(0, 0, 0, 0.08);
            border: 1px solid #e0e0e0;
        }
        h1, h2 {
            color: #2c3e50;
            text-align: center;
            margin-bottom: 30px;
        }
        .input-group {
            margin-bottom: 18px;
            display: flex;
            flex-direction: column;
        }
        .input-group label {
            margin-bottom: 8px;
            font-weight: bold;
            color: #555;
            font-size: 1.05em;
        }
        .input-group input[type="number"] {
            padding: 12px 15px;
            border: 1px solid #ccc;
            border-radius: 8px;
            font-size: 1em;
            width: 100%;
            box-sizing: border-box; /* Ensures padding doesn't affect total width */
            transition: border-color 0.3s ease;
        }
        .input-group input[type="number"]:focus {
            border-color: #007bff;
            outline: none;
            box-shadow: 0 0 5px rgba(0, 123, 255, 0.2);
        }
        button {
            background-color: #007bff;
            color: white;
            padding: 14px 25px;
            border: none;
            border-radius: 8px;
            cursor: pointer;
            font-size: 1.1em;
            font-weight: bold;
            width: 100%;
            margin-top: 20px;
            transition: background-color 0.3s ease, transform 0.2s ease;
        }
        button:hover {
            background-color: #0056b3;
            transform: translateY(-2px);
        }
        .results {
            margin-top: 30px;
            padding: 25px;
            background-color: #e9f5ff;
            border: 1px solid #cce5ff;
            border-radius: 10px;
            display: none; /* Hidden by default */
        }
        .results p {
            font-size: 1.1em;
            margin-bottom: 10px;
            color: #333;
        }
        .results p strong {
            color: #0056b3;
            font-size: 1.15em;
        }
        table {
            width: 100%;
            border-collapse: collapse;
            margin-top: 25px;
            background-color: #fff;
            box-shadow: 0 2px 10px rgba(0,0,0,0.05);
            border-radius: 8px;
            overflow: hidden; /* Ensures rounded corners apply to content */
        }
        th, td {
            padding: 15px;
            text-align: center;
            border-bottom: 1px solid #eee;
        }
        th {
            background-color: #007bff;
            color: white;
            font-weight: bold;
            font-size: 1.05em;
        }
        tr:nth-child(even) {
            background-color: #f9f9f9;
        }
        tr:hover {
            background-color: #f1f8ff;
        }
        canvas {
            margin-top: 30px;
            background-color: #fff;
            border-radius: 10px;
            padding: 15px;
            box-shadow: 0 2px 10px rgba(0,0,0,0.05);
        }
        /* Responsive adjustments */
        @media (max-width: 768px) {
            .container {
                padding: 20px;
                margin: 10px;
            }
            button {
                padding: 12px 20px;
                font-size: 1em;
            }
            th, td {
                padding: 10px;
                font-size: 0.9em;
            }
        }
        @media (max-width: 480px) {
            body {
                padding: 10px;
            }
            .container {
                padding: 15px;
            }
            .input-group label {
                font-size: 0.95em;
            }
            .input-group input[type="number"] {
                padding: 10px;
                font-size: 0.9em;
            }
            .results p {
                font-size: 1em;
            }
            h1, h2 {
                font-size: 1.5em;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>حاسبة تطور رأس المال</h1>
        <div class="input-group">
            <label for="initialCapital">رأس المال الأولي ($):</label>
            <input type="number" id="initialCapital" value="10000" min="1">
        </div>
        <div class="input-group">
            <label for="winRate">نسبة الصفقات الرابحة (%):</label>
            <input type="number" id="winRate" value="60" min="0" max="100">
        </div>
        <div class="input-group">
            <label for="profitPerTrade">معدل الربح لكل صفقة (% من رأس المال):</label>
            <input type="number" id="profitPerTrade" value="2" min="0.01">
        </div>
        <div class="input-group">
            <label for="lossPerTrade">معدل الخسارة لكل صفقة (% من رأس المال):</label>
            <input type="number" id="lossPerTrade" value="1" min="0.01">
        </div>
        <div class="input-group">
            <label for="tradesPerUpdate">عدد الصفقات في كل تحديث عرض (X):</label>
            <input type="number" id="tradesPerUpdate" value="10" min="1">
        </div>
        <div class="input-group">
            <label for="finalTarget">الهدف النهائي لرأس المال ($):</label>
            <input type="number" id="finalTarget" value="20000" min="1">
        </div>
        <button onclick="calculateCapitalEvolution()">احسب تطور رأس المال</button>

        <div class="results" id="resultsSection">
            <h2>النتائج المحسوبة</h2>
            <p>متوسط العائد لكل صفقة: <strong><span id="avgReturnPerTrade"></span>%</strong></p>
            <p>عدد الصفقات المطلوبة للوصول إلى الهدف: <strong><span id="requiredTrades"></span> صفقة</strong></p>
            <p>معدل النمو الإجمالي المطلوب: <strong><span id="totalGrowthRate"></span>%</strong></p>

            ---
            <h2>تطور رأس المال</h2>
            <div style="overflow-x: auto;">
                <table id="capitalTable">
                    <thead>
                        <tr>
                            <th>عدد الصفقات</th>
                            <th>رأس المال</th>
                        </tr>
                    </thead>
                    <tbody>
                        </tbody>
                </table>
            </div>
            
            <canvas id="capitalChart"></canvas>
        </div>
    </div>

    <script>
        let capitalChart; // Declare chart globally to destroy and re-create

        function calculateCapitalEvolution() {
            const initialCapital = parseFloat(document.getElementById('initialCapital').value);
            const winRate = parseFloat(document.getElementById('winRate').value) / 100;
            const profitPerTrade = parseFloat(document.getElementById('profitPerTrade').value) / 100;
            const lossPerTrade = parseFloat(document.getElementById('lossPerTrade').value) / 100;
            const tradesPerUpdate = parseInt(document.getElementById('tradesPerUpdate').value);
            const finalTarget = parseFloat(document.getElementById('finalTarget').value);

            if (isNaN(initialCapital) || isNaN(winRate) || isNaN(profitPerTrade) || isNaN(lossPerTrade) || isNaN(tradesPerUpdate) || isNaN(finalTarget) || initialCapital <= 0 || tradesPerUpdate <= 0 || finalTarget <= 0) {
                alert('الرجاء إدخال قيم صحيحة وإيجابية لجميع الحقول.');
                return;
            }

            // متوسط العائد لكل صفقة
            const avgReturnPerTrade = (winRate * profitPerTrade) - ((1 - winRate) * lossPerTrade);
            document.getElementById('avgReturnPerTrade').textContent = (avgReturnPerTrade * 100).toFixed(2);

            // عدد الصفقات المطلوبة للوصول إلى الهدف
            let currentCapital = initialCapital;
            let tradesCount = 0;
            const capitalHistory = [];
            const tradesHistory = [];
            let reachedTarget = false;

            // Add initial state to history
            capitalHistory.push(initialCapital);
            tradesHistory.push(0);

            // Calculate growth until target is reached or a reasonable limit
            const maxIterations = 50000; // Prevent infinite loops
            for (let i = 0; i < maxIterations; i++) {
                tradesCount++;
                const isWin = Math.random() < winRate;
                if (isWin) {
                    currentCapital *= (1 + profitPerTrade);
                } else {
                    currentCapital *= (1 - lossPerTrade);
                }

                if (tradesCount % tradesPerUpdate === 0) {
                    capitalHistory.push(currentCapital);
                    tradesHistory.push(tradesCount);
                }
                
                if (currentCapital >= finalTarget) {
                    reachedTarget = true;
                    // Add final state if not already added by tradesPerUpdate
                    if (tradesCount % tradesPerUpdate !== 0) {
                        capitalHistory.push(currentCapital);
                        tradesHistory.push(tradesCount);
                    }
                    break;
                }
                if (currentCapital <= 0) { // Capital depleted
                    currentCapital = 0;
                    capitalHistory.push(0);
                    tradesHistory.push(tradesCount);
                    break;
                }
            }

            const requiredTrades = reachedTarget ? tradesCount : "لم يتم الوصول للهدف ضمن " + maxIterations + " صفقة (رأس المال الحالي: " + currentCapital.toFixed(2) + "$)";
            document.getElementById('requiredTrades').textContent = requiredTrades;

            // معدل النمو الإجمالي
            const totalGrowthRate = ((currentCapital - initialCapital) / initialCapital) * 100;
            document.getElementById('totalGrowthRate').textContent = totalGrowthRate.toFixed(2);

            // عرض الجدول
            const capitalTableBody = document.querySelector('#capitalTable tbody');
            capitalTableBody.innerHTML = ''; // Clear previous data
            for (let i = 0; i < capitalHistory.length; i++) {
                const row = capitalTableBody.insertRow();
                const cell1 = row.insertCell();
                const cell2 = row.insertCell();
                cell1.textContent = tradesHistory[i];
                cell2.textContent = capitalHistory[i].toFixed(2) + '$';
            }

            // عرض المخطط
            const ctx = document.getElementById('capitalChart').getContext('2d');
            if (capitalChart) {
                capitalChart.destroy(); // Destroy previous chart instance
            }
            capitalChart = new Chart(ctx, {
                type: 'line',
                data: {
                    labels: tradesHistory,
                    datasets: [{
                        label: 'تطور رأس المال ($)',
                        data: capitalHistory,
                        borderColor: '#007bff',
                        backgroundColor: 'rgba(0, 123, 255, 0.1)',
                        borderWidth: 2,
                        tension: 0.3,
                        pointRadius: 3,
                        pointBackgroundColor: '#007bff'
                    }]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    plugins: {
                        title: {
                            display: true,
                            text: 'مخطط تطور رأس المال مع عدد الصفقات',
                            font: {
                                size: 18
                            }
                        },
                        tooltip: {
                            callbacks: {
                                label: function(context) {
                                    return 'رأس المال: $' + context.parsed.y.toFixed(2);
                                },
                                title: function(context) {
                                    return 'العدد: ' + context[0].parsed.x + ' صفقة';
                                }
                            },
                            bodyFont: { size: 14 },
                            titleFont: { size: 14, weight: 'bold' }
                        }
                    },
                    scales: {
                        x: {
                            title: {
                                display: true,
                                text: 'عدد الصفقات',
                                font: {
                                    size: 16
                                }
                            },
                            ticks: {
                                font: { size: 12 }
                            }
                        },
                        y: {
                            title: {
                                display: true,
                                text: 'رأس المال ($)',
                                font: {
                                    size: 16
                                }
                            },
                            ticks: {
                                callback: function(value) {
                                    return '$' + value.toFixed(0);
                                },
                                font: { size: 12 }
                            },
                            beginAtZero: true
                        }
                    }
                }
            });

            document.getElementById('resultsSection').style.display = 'block';
        }
    </script>
</body>
</html>
