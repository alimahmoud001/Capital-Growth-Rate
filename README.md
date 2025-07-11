
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>حاسبة تطور رأس المال</title>
    <link href="https://fonts.googleapis.com/css2?family=Cairo:wght@400;700&display=swap" rel="stylesheet">
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <style>
        :root {
            --primary-color: #4CAF50; /* Green */
            --secondary-color: #2196F3; /* Blue */
            --background-color: #f4f7f6;
            --card-background: #ffffff;
            --text-color: #333;
            --border-radius: 12px;
            --shadow: 0 6px 20px rgba(0, 0, 0, 0.08);
        }

        body {
            font-family: 'Cairo', sans-serif;
            background-color: var(--background-color);
            color: var(--text-color);
            display: flex;
            justify-content: center;
            align-items: flex-start;
            min-height: 100vh;
            padding: 40px 20px;
            margin: 0;
            box-sizing: border-box;
            line-height: 1.6;
        }

        .container {
            display: flex;
            flex-wrap: wrap;
            gap: 30px;
            max-width: 1300px;
            width: 100%;
        }

        .card {
            background-color: var(--card-background);
            border-radius: var(--border-radius);
            box-shadow: var(--shadow);
            padding: 30px;
            transition: transform 0.3s ease, box-shadow 0.3s ease;
            flex: 1;
            min-width: 300px;
        }

        .card:hover {
            transform: translateY(-5px);
            box-shadow: 0 10px 25px rgba(0, 0, 0, 0.12);
        }

        .input-section {
            flex: 1;
            min-width: 350px;
            max-width: 450px;
        }

        .results-section {
            flex: 1;
            min-width: 350px;
            max-width: 450px;
        }

        .chart-section {
            flex-basis: 100%;
            min-height: 450px;
        }

        h1, h2 {
            color: var(--primary-color);
            text-align: center;
            margin-bottom: 30px;
            font-weight: 700;
        }

        .form-group {
            margin-bottom: 20px;
        }

        label {
            display: block;
            margin-bottom: 8px;
            font-weight: 600;
            color: #555;
        }

        input[type="number"] {
            width: calc(100% - 24px);
            padding: 12px;
            border: 1px solid #e0e0e0;
            border-radius: 8px;
            font-size: 16px;
            background-color: #fdfdfd;
            transition: border-color 0.3s ease, box-shadow 0.3s ease;
        }

        input[type="number"]:focus {
            outline: none;
            border-color: var(--secondary-color);
            box-shadow: 0 0 0 3px rgba(33, 150, 243, 0.2);
        }

        button {
            display: block;
            width: 100%;
            padding: 15px;
            background-color: var(--primary-color);
            color: white;
            border: none;
            border-radius: var(--border-radius);
            font-size: 18px;
            font-weight: 700;
            cursor: pointer;
            transition: background-color 0.3s ease, transform 0.2s ease;
            margin-top: 30px;
        }

        button:hover {
            background-color: #43A047; /* Darker green */
            transform: translateY(-2px);
        }

        .results-output p {
            background-color: #e8f5e9; /* Light green background */
            padding: 15px;
            border-radius: 8px;
            margin-bottom: 15px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            font-size: 17px;
            font-weight: 600;
            color: #2e7d32; /* Darker green text */
        }

        .results-output span {
            color: var(--secondary-color);
            font-weight: 700;
        }

        canvas {
            background-color: var(--card-background);
            border-radius: var(--border-radius);
            padding: 20px;
        }

        @media (max-width: 768px) {
            .container {
                flex-direction: column;
                align-items: center;
            }
            .input-section, .results-section, .chart-section {
                width: 100%;
                max-width: 600px;
            }
            body {
                padding: 20px 15px;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="card input-section">
            <h2>المدخلات</h2>
            <div class="form-group">
                <label for="initialCapital">رأس المال الأولي ($)</label>
                <input type="number" id="initialCapital" value="10000" min="1">
            </div>
            <div class="form-group">
                <label for="winRate">نسبة الصفقات الرابحة (%)</label>
                <input type="number" id="winRate" value="55" min="0" max="100">
            </div>
            <div class="form-group">
                <label for="profitPerTrade">معدل الربح لكل صفقة (% من رأس المال)</label>
                <input type="number" id="profitPerTrade" value="2" min="0">
            </div>
            <div class="form-group">
                <label for="lossPerTrade">معدل الخسارة لكل صفقة (% من رأس المال)</label>
                <input type="number" id="lossPerTrade" value="1" min="0">
            </div>
            <div class="form-group">
                <label for="tradesPerUpdate">عدد الصفقات (x) في كل تحديث عرض</label>
                <input type="number" id="tradesPerUpdate" value="50" min="1">
            </div>
            <div class="form-group">
                <label for="targetCapital">الهدف النهائي ($)</label>
                <input type="number" id="targetCapital" value="20000" min="0">
            </div>
            <button onclick="calculateGrowth()">حساب ورسم التطور</button>
        </div>

        <div class="card results-section">
            <h2>النتائج</h2>
            <div class="results-output">
                <p>متوسط العائد لكل صفقة: <span id="averageReturn">0%</span></p>
                <p>عدد الصفقات المطلوبة للهدف: <span id="requiredTrades">0</span></p>
                <p>معدل النمو الإجمالي (لعدد الصفقات المعروضة): <span id="totalGrowth">0%</span></p>
            </div>
        </div>

        <div class="card chart-section">
            <h2>مخطط تطور رأس المال</h2>
            <canvas id="capitalGrowthChart"></canvas>
        </div>
    </div>

    <script>
        let capitalChart;

        function calculateGrowth() {
            const initialCapital = parseFloat(document.getElementById('initialCapital').value);
            const winRate = parseFloat(document.getElementById('winRate').value) / 100;
            const profitPerTrade = parseFloat(document.getElementById('profitPerTrade').value) / 100;
            const lossPerTrade = parseFloat(document.getElementById('lossPerTrade').value) / 100;
            const tradesPerUpdate = parseInt(document.getElementById('tradesPerUpdate').value);
            const targetCapital = parseFloat(document.getElementById('targetCapital').value);

            if (isNaN(initialCapital) || isNaN(winRate) || isNaN(profitPerTrade) || isNaN(lossPerTrade) || isNaN(tradesPerUpdate) || isNaN(targetCapital) || initialCapital <= 0) {
                alert('الرجاء إدخال قيم صحيحة لجميع الحقول. رأس المال الأولي يجب أن يكون أكبر من صفر.');
                return;
            }

            // حساب متوسط العائد لكل صفقة
            const averageReturnPerTrade = (winRate * profitPerTrade) - ((1 - winRate) * lossPerTrade);
            document.getElementById('averageReturn').textContent = `${(averageReturnPerTrade * 100).toFixed(2)}%`;

            // حساب تطور رأس المال ورسم المخطط
            let currentCapital = initialCapital;
            const capitalHistory = [initialCapital];
            const tradeCounts = [0];
            let tradesNeededForTarget = 0;
            let targetReached = false;
            const maxIterations = 2000; // لمنع الحلقات اللانهائية في حال عدم الوصول للهدف

            for (let i = 1; i <= maxIterations * tradesPerUpdate; i++) {
                if (Math.random() < winRate) {
                    currentCapital *= (1 + profitPerTrade);
                } else {
                    currentCapital *= (1 - lossPerTrade);
                }

                if (i % tradesPerUpdate === 0) {
                    capitalHistory.push(currentCapital);
                    tradeCounts.push(i);
                }

                if (!targetReached && currentCapital >= targetCapital) {
                    tradesNeededForTarget = i;
                    targetReached = true;
                }
            }

            // إذا لم يتم الوصول للهدف بعد الحد الأقصى للصفقات، يتم تحديث القيمة إلى "غير محدد" أو قيمة كبيرة
            document.getElementById('requiredTrades').textContent = targetReached ? tradesNeededForTarget : 'غير محدد (يتطلب صفقات أكثر)';

            // معدل النمو الإجمالي للعدد الحالي من الصفقات المعروضة
            const totalGrowthPercentage = ((currentCapital - initialCapital) / initialCapital) * 100;
            document.getElementById('totalGrowth').textContent = `${totalGrowthPercentage.toFixed(2)}%`;

            renderChart(tradeCounts, capitalHistory, initialCapital, targetCapital);
        }

        function renderChart(labels, data, initialCapital, targetCapital) {
            const ctx = document.getElementById('capitalGrowthChart').getContext('2d');

            if (capitalChart) {
                capitalChart.destroy(); // Destroy existing chart before creating a new one
            }

            capitalChart = new Chart(ctx, {
                type: 'line',
                data: {
                    labels: labels,
                    datasets: [{
                        label: 'تطور رأس المال',
                        data: data,
                        borderColor: 'var(--primary-color)',
                        backgroundColor: 'rgba(76, 175, 80, 0.2)',
                        fill: true,
                        tension: 0.3,
                        pointRadius: 0
                    },
                    {
                        label: 'رأس المال الأولي',
                        data: Array(labels.length).fill(initialCapital),
                        borderColor: '#FFC107', /* Amber */
                        borderDash: [5, 5],
                        pointRadius: 0,
                        fill: false
                    },
                    {
                        label: 'الهدف النهائي',
                        data: Array(labels.length).fill(targetCapital),
                        borderColor: '#F44336', /* Red */
                        borderDash: [5, 5],
                        pointRadius: 0,
                        fill: false
                    }
                ]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    plugins: {
                        legend: {
                            display: true,
                            position: 'top',
                            labels: {
                                font: {
                                    family: 'Cairo',
                                    size: 14
                                }
                            }
                        },
                        tooltip: {
                            callbacks: {
                                title: function(context) {
                                    return `الصفقات: ${context[0].label}`;
                                },
                                label: function(context) {
                                    let label = context.dataset.label || '';
                                    if (label) {
                                        label += ': ';
                                    }
                                    if (context.parsed.y !== null) {
                                        label += `$${context.parsed.y.toFixed(2)}`;
                                    }
                                    return label;
                                }
                            },
                            bodyFont: {
                                family: 'Cairo'
                            },
                            titleFont: {
                                family: 'Cairo'
                            }
                        }
                    },
                    scales: {
                        x: {
                            title: {
                                display: true,
                                text: 'عدد الصفقات',
                                font: {
                                    family: 'Cairo',
                                    size: 16,
                                    weight: 'bold'
                                }
                            },
                            ticks: {
                                font: {
                                    family: 'Cairo'
                                }
                            }
                        },
                        y: {
                            title: {
                                display: true,
                                text: 'رأس المال ($)',
                                font: {
                                    family: 'Cairo',
                                    size: 16,
                                    weight: 'bold'
                                }
                            },
                            ticks: {
                                callback: function(value) {
                                    return `$${value.toFixed(0)}`;
                                },
                                font: {
                                    family: 'Cairo'
                                }
                            }
                        }
                    }
                }
            });
        }

        // Initial calculation on load
        window.onload = calculateGrowth;
    </script>
</body>
</html>
