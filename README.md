<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>خطة الوصول إلى مليون دولار - نسخة تفاعلية</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        
        body {
            background: linear-gradient(135deg, #1a2a6c, #2c3e50);
            color: #fff;
            padding: 20px;
            line-height: 1.6;
        }
        
        .container {
            max-width: 1200px;
            margin: 0 auto;
        }
        
        header {
            text-align: center;
            padding: 30px 0;
            background: rgba(0, 0, 0, 0.3);
            border-radius: 15px;
            margin-bottom: 30px;
            box-shadow: 0 10px 20px rgba(0, 0, 0, 0.3);
        }
        
        h1 {
            font-size: 2.8rem;
            margin-bottom: 15px;
            color: #ffd700;
            text-shadow: 0 2px 4px rgba(0, 0, 0, 0.5);
        }
        
        .subtitle {
            font-size: 1.4rem;
            max-width: 800px;
            margin: 0 auto;
            color: #f0f0f0;
        }
        
        .controls {
            background: rgba(255, 255, 255, 0.1);
            border-radius: 15px;
            padding: 30px;
            margin-bottom: 30px;
            box-shadow: 0 8px 16px rgba(0, 0, 0, 0.2);
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 20px;
        }
        
        .control-group {
            margin-bottom: 15px;
        }
        
        .control-group label {
            display: block;
            margin-bottom: 8px;
            font-weight: bold;
            color: #4fc3f7;
        }
        
        .control-group input {
            width: 100%;
            padding: 12px;
            border-radius: 8px;
            border: none;
            background: rgba(0, 0, 0, 0.3);
            color: white;
            font-size: 16px;
            transition: all 0.3s ease;
        }
        
        .control-group input:focus {
            outline: none;
            box-shadow: 0 0 0 3px rgba(79, 195, 247, 0.5);
            background: rgba(0, 0, 0, 0.5);
        }
        
        .btn-container {
            grid-column: 1 / -1;
            text-align: center;
            margin-top: 15px;
        }
        
        .btn {
            background: linear-gradient(90deg, #ff9800, #ff5722);
            color: white;
            border: none;
            padding: 14px 35px;
            font-size: 18px;
            border-radius: 50px;
            cursor: pointer;
            transition: all 0.3s ease;
            font-weight: bold;
            box-shadow: 0 5px 15px rgba(255, 87, 34, 0.4);
        }
        
        .btn:hover {
            transform: translateY(-3px);
            box-shadow: 0 8px 20px rgba(255, 87, 34, 0.6);
        }
        
        .result-cards {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 25px;
            margin-bottom: 40px;
        }
        
        .card {
            background: rgba(255, 255, 255, 0.1);
            border-radius: 15px;
            padding: 25px;
            box-shadow: 0 8px 16px rgba(0, 0, 0, 0.2);
            transition: transform 0.3s ease, box-shadow 0.3s ease;
            backdrop-filter: blur(10px);
            border: 1px solid rgba(255, 255, 255, 0.1);
        }
        
        .card:hover {
            transform: translateY(-10px);
            box-shadow: 0 12px 24px rgba(0, 0, 0, 0.3);
        }
        
        .card h2 {
            color: #4fc3f7;
            margin-bottom: 20px;
            font-size: 1.8rem;
            display: flex;
            align-items: center;
            gap: 10px;
        }
        
        .card h2 i {
            color: #ffd700;
        }
        
        .card ul {
            list-style-type: none;
            padding: 0;
        }
        
        .card li {
            padding: 12px 0;
            border-bottom: 1px dashed rgba(255, 255, 255, 0.2);
            display: flex;
            justify-content: space-between;
        }
        
        .card li:last-child {
            border-bottom: none;
        }
        
        .card li span.value {
            color: #ffd700;
            font-weight: bold;
        }
        
        .highlight {
            background: linear-gradient(90deg, #ff9800, #ff5722);
            padding: 5px 10px;
            border-radius: 5px;
            font-weight: bold;
        }
        
        .table-container {
            background: rgba(255, 255, 255, 0.05);
            border-radius: 15px;
            padding: 25px;
            margin-bottom: 40px;
            overflow-x: auto;
            box-shadow: 0 8px 16px rgba(0, 0, 0, 0.2);
        }
        
        table {
            width: 100%;
            border-collapse: collapse;
            text-align: center;
        }
        
        th {
            background: rgba(0, 100, 200, 0.3);
            padding: 15px;
            font-size: 1.1rem;
        }
        
        td {
            padding: 12px;
            border-bottom: 1px solid rgba(255, 255, 255, 0.1);
        }
        
        tr:nth-child(even) {
            background: rgba(255, 255, 255, 0.03);
        }
        
        tr:hover {
            background: rgba(50, 150, 250, 0.2);
        }
        
        .milestone {
            color: #4caf50;
            font-weight: bold;
        }
        
        .million-row {
            background: linear-gradient(90deg, rgba(76, 175, 80, 0.3), rgba(76, 175, 80, 0.1)) !important;
            font-weight: bold;
            color: #ffd700;
            font-size: 1.1rem;
        }
        
        .footer-note {
            background: rgba(255, 255, 255, 0.05);
            border-radius: 15px;
            padding: 25px;
            margin-top: 30px;
            box-shadow: 0 8px 16px rgba(0, 0, 0, 0.2);
        }
        
        .footer-note h2 {
            color: #ff9800;
            margin-bottom: 20px;
            font-size: 1.8rem;
            display: flex;
            align-items: center;
            gap: 10px;
        }
        
        .warning {
            color: #ff9800;
            font-weight: bold;
        }
        
        .error {
            color: #ff5252;
            font-weight: bold;
            margin-top: 5px;
            display: block;
        }
        
        @media (max-width: 768px) {
            h1 {
                font-size: 2.2rem;
            }
            
            .subtitle {
                font-size: 1.1rem;
            }
            
            .result-cards {
                grid-template-columns: 1fr;
            }
            
            th, td {
                padding: 10px 5px;
                font-size: 0.9rem;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <header>
            <h1><i class="fas fa-chart-line"></i> خطة الوصول إلى مليون دولار - نسخة تفاعلية</h1>
            <p class="subtitle">عدّل المعايير المالية حسب رغبتك وشاهد كيف يتطور رأس مالك مع كل صفقة</p>
        </header>
        
        <div class="controls">
            <div class="control-group">
                <label for="initialCapital"><i class="fas fa-wallet"></i> رأس المال الابتدائي ($)</label>
                <input type="number" id="initialCapital" value="" min="1" step="1">
            </div>
            
            <div class="control-group">
                <label for="winRate"><i class="fas fa-trophy"></i> نسبة الصفقات الرابحة (%)</label>
                <input type="number" id="winRate" value="" min="1" max="100" step="1">
            </div>
            
            <div class="control-group">
                <label for="profitPercent"><i class="fas fa-arrow-up"></i> معدل الربح لكل صفقة (%)</label>
                <input type="number" id="profitPercent" value="" min="0.1" step="0.1">
            </div>
            
            <div class="control-group">
                <label for="lossPercent"><i class="fas fa-arrow-down"></i> معدل الخسارة لكل صفقة (%)</label>
                <input type="number" id="lossPercent" value="" min="0.1" step="0.1">
            </div>
            
            <div class="control-group">
                <label for="tradeStep"><i class="fas fa-step-forward"></i> عدد الصفقات بين كل تحديث</label>
                <input type="number" id="tradeStep" value="" min="1" step="1">
            </div>
            
            <div class="control-group">
                <label for="target"><i class="fas fa-bullseye"></i> الهدف المالي ($)</label>
                <input type="number" id="target" value="" min="1000" step="1000">
            </div>
            
            <div class="btn-container">
                <button class="btn" id="calculateBtn">
                    <i class="fas fa-calculator"></i> احسب خطة الوصول
                </button>
            </div>
        </div>
        
        <div class="result-cards">
            <div class="card">
                <h2><i class="fas fa-chart-pie"></i> النسب المالية</h2>
                <ul>
                    <li>رأس المال الابتدائي: <span class="value" id="resInitialCapital">$20.00</span></li>
                    <li>نسبة الصفقات الرابحة: <span class="value" id="resWinRate">80%</span></li>
                    <li>نسبة الصفقات الخاسرة: <span class="value" id="resLossRate">20%</span></li>
                    <li>معدل الربح لكل صفقة: <span class="value" id="resProfitPercent">3%</span></li>
                    <li>معدل الخسارة لكل صفقة: <span class="value" id="resLossPercent">1%</span></li>
                    <li>نسبة الربح إلى الخسارة: <span class="value" id="resRiskReward">3:1</span></li>
                </ul>
            </div>
            
            <div class="card">
                <h2><i class="fas fa-calculator"></i> الحسابات الأساسية</h2>
                <ul>
                    <li>متوسط العائد لكل صفقة: <span class="value" id="resAvgReturn">2.20%</span></li>
                    <li>عدد الصفقات المطلوبة: <span class="value" id="resTotalTrades">510 صفقة</span></li>
                    <li>الزمن المتوقع (5 صفقات/يوم): <span class="value" id="resTime1">102 يوم</span></li>
                    <li>الزمن المتوقع (3 صفقات/يوم): <span class="value" id="resTime2">170 يوم</span></li>
                    <li>معدل النمو الإجمالي: <span class="value" id="resGrowthFactor">50,000x</span></li>
                </ul>
            </div>
            
        </div>
        
        <div class="table-container">
            <h2><i class="fas fa-table"></i> تطور رأس المال مع كل <span id="stepIndicator">10</span> صفقات</h2>
            <table>
                <thead>
                    <tr>
                        <th>عدد الصفقات</th>
                        <th>رأس المال (دولار)</th>
                        <th>معدل النمو</th>
                        <th>الملاحظات</th>
                    </tr>
                </thead>
                <tbody id="resultsTable">
                    <!-- سيتم ملئ الجدول بالجافاسكريبت -->
                </tbody>
            </table>
        </div>
        
    </div>

    <script>
        document.addEventListener('DOMContentLoaded', function() {
            // العناصر
            const initialCapitalInput = document.getElementById('initialCapital');
            const winRateInput = document.getElementById('winRate');
            const profitPercentInput = document.getElementById('profitPercent');
            const lossPercentInput = document.getElementById('lossPercent');
            const tradeStepInput = document.getElementById('tradeStep');
            const targetInput = document.getElementById('target');
            const calculateBtn = document.getElementById('calculateBtn');
            
            // عناصر النتائج
            const resInitialCapital = document.getElementById('resInitialCapital');
            const resWinRate = document.getElementById('resWinRate');
            const resLossRate = document.getElementById('resLossRate');
            const resProfitPercent = document.getElementById('resProfitPercent');
            const resLossPercent = document.getElementById('resLossPercent');
            const resRiskReward = document.getElementById('resRiskReward');
            const resAvgReturn = document.getElementById('resAvgReturn');
            const resTotalTrades = document.getElementById('resTotalTrades');
            const resTime1 = document.getElementById('resTime1');
            const resTime2 = document.getElementById('resTime2');
            const resGrowthFactor = document.getElementById('resGrowthFactor');
            const stepIndicator = document.getElementById('stepIndicator');
            const resultsTable = document.getElementById('resultsTable');
            
            // دالة لتنسيق الأرقام
            function formatNumber(num) {
                return new Intl.NumberFormat('en-US', {
                    minimumFractionDigits: 2,
                    maximumFractionDigits: 2
                }).format(num);
            }
            
            // دالة لتنسيق الأرقام الكبيرة
            function formatLargeNumber(num) {
                if (num >= 1000000) {
                    return (num / 1000000).toFixed(2) + 'M';
                }
                if (num >= 1000) {
                    return (num / 1000).toFixed(1) + 'K';
                }
                return formatNumber(num);
            }
            
            // دالة لحساب متوسط العائد
            function calculateAvgReturn(winRate, profitPercent, lossPercent) {
                const winDecimal = winRate / 100;
                const lossDecimal = 1 - winDecimal;
                return (winDecimal * (profitPercent / 100)) + (lossDecimal * (-lossPercent / 100));
            }
            
            // دالة لحساب عدد الصفقات المطلوبة
            function calculateTradesNeeded(initial, target, avgReturn) {
                if (avgReturn <= 0) return Infinity;
                return Math.log(target / initial) / Math.log(1 + avgReturn);
            }
            
            // دالة لتوليد الجدول
            function generateTable() {
                // الحصول على القيم من المدخلات
                const initialCapital = parseFloat(initialCapitalInput.value);
                const winRate = parseFloat(winRateInput.value);
                const profitPercent = parseFloat(profitPercentInput.value);
                const lossPercent = parseFloat(lossPercentInput.value);
                const tradeStep = parseInt(tradeStepInput.value);
                const target = parseFloat(targetInput.value);
                
                // حساب القيم المشتقة
                const lossRate = 100 - winRate;
                const riskRewardRatio = (profitPercent / lossPercent).toFixed(1);
                const avgReturn = calculateAvgReturn(winRate, profitPercent, lossPercent);
                const totalTrades = calculateTradesNeeded(initialCapital, target, avgReturn);
                
                // تحديث بطاقات النتائج
                resInitialCapital.textContent = `$${formatNumber(initialCapital)}`;
                resWinRate.textContent = `${winRate}%`;
                resLossRate.textContent = `${lossRate}%`;
                resProfitPercent.textContent = `${profitPercent}%`;
                resLossPercent.textContent = `${lossPercent}%`;
                resRiskReward.textContent = `${riskRewardRatio}:1`;
                resAvgReturn.textContent = `${(avgReturn * 100).toFixed(2)}%`;
                
                // تحديث مؤشر الخطوة في الجدول
                stepIndicator.textContent = tradeStep;
                
                // تحديث معلومات الوقت
                if (isFinite(totalTrades)) {
                    resTotalTrades.textContent = `${Math.ceil(totalTrades)} صفقة`;
                    resTime1.textContent = `${Math.ceil(totalTrades / 5)} يوم (5 صفقات/يوم)`;
                    resTime2.textContent = `${Math.ceil(totalTrades / 3)} يوم (3 صفقات/يوم)`;
                    resGrowthFactor.textContent = `${formatLargeNumber(target / initialCapital)}x`;
                } else {
                    resTotalTrades.textContent = "لا يمكن الوصول للهدف (متوسط عائد سلبي)";
                    resTime1.textContent = "---";
                    resTime2.textContent = "---";
                    resGrowthFactor.textContent = "---";
                }
                
                // إعادة تعيين الجدول
                resultsTable.innerHTML = '';
                
                // إضافة الصف الأول (رأس المال الابتدائي)
                addTableRow(0, initialCapital, initialCapital);
                
                // إذا كان متوسط العائد موجبًا
                if (avgReturn > 0 && isFinite(totalTrades)) {
                    let tradeCount = 0;
                    let capital = initialCapital;
                    
                    // إضافة الصفوف حتى الوصول للهدف
                    while (tradeCount < totalTrades) {
                        tradeCount += tradeStep;
                        if (tradeCount > totalTrades) tradeCount = Math.ceil(totalTrades);
                        
                        // حساب رأس المال بعد n صفقة
                        capital = initialCapital * Math.pow(1 + avgReturn, tradeCount);
                        
                        // إذا تجاوزنا الهدف، نضبطه على الهدف
                        if (capital > target) capital = target;
                        
                        // إضافة صف للجدول
                        addTableRow(tradeCount, capital, initialCapital);
                        
                        // إذا وصلنا للهدف، نخرج من الحلقة
                        if (capital >= target) break;
                    }
                } else {
                    // إضافة رسالة خطأ في الجدول
                    const row = document.createElement('tr');
                    row.innerHTML = `
                        <td colspan="4" style="color: #ff5252; font-weight: bold; padding: 20px;">
                            <i class="fas fa-exclamation-circle"></i> لا يمكن الوصول للهدف - متوسط العائد لكل صفقة غير كافٍ
                        </td>
                    `;
                    resultsTable.appendChild(row);
                }
            }
            
            // دالة لإضافة صف للجدول
            function addTableRow(trades, capital, initial) {
                const row = document.createElement('tr');
                
                // تحديد الملاحظات
                let notes = '';
                if (trades === 0) {
                    notes = 'رأس المال الابتدائي';
                } else if (capital >= 1000 && capital < 10000) {
                    notes = 'ألف دولار';
                } else if (capital >= 10000 && capital < 100000) {
                    notes = 'عشرة آلاف دولار';
                } else if (capital >= 100000 && capital < 1000000) {
                    notes = 'مائة ألف دولار';
                } else if (capital >= 1000000) {
                    notes = 'مليون دولار!';
                }
                
                // حساب معدل النمو الإجمالي
                const growthFactor = (capital / initial).toFixed(1);
                
                // تحديد إذا كان هذا الصف هو صف الهدف
                const target = parseFloat(targetInput.value);
                if (capital >= target) {
                    row.classList.add('million-row');
                }
                
                row.innerHTML = `
                    <td>${trades}</td>
                    <td class="${capital >= target ? 'milestone' : ''}">$${formatNumber(capital)}</td>
                    <td>${growthFactor}x</td>
                    <td>${notes}</td>
                `;
                
                resultsTable.appendChild(row);
            }
            
            // تعيين القيم الافتراضية عند التحميل
            generateTable();
            
            // إضافة مستمع الأحداث لزر الحساب
            calculateBtn.addEventListener('click', generateTable);
            
            // تحديث النتائج عند تغيير أي إدخال
            const inputs = document.querySelectorAll('.controls input');
            inputs.forEach(input => {
                input.addEventListener('input', generateTable);
            });
        });
    </script>
</body>
</html>
