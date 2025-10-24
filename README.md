<!DOCTYPE html>
<html lang="zh-Hant">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>憲法知識挑戰</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Microsoft JhengHei', Arial, sans-serif;
        }
        
        body {
            background-color: #1e3a8a; /* 藍色背景 */
            color: #333;
            line-height: 1.6;
            padding: 20px;
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
        }
        
        .container {
            max-width: 900px;
            width: 100%;
            background-color: white;
            border-radius: 10px;
            padding: 30px;
            box-shadow: 0 4px 15px rgba(0, 0, 0, 0.2);
        }
        
        header {
            text-align: center;
            margin-bottom: 30px;
            padding-bottom: 20px;
            border-bottom: 2px solid #1e3a8a;
        }
        
        h1 {
            color: #1e3a8a;
            margin-bottom: 10px;
        }
        
        .description {
            color: #666;
            margin-bottom: 20px;
        }
        
        #start-screen, #scenario-selection, #game-screen, #result-screen {
            transition: opacity 0.3s ease;
        }
        
        #start-screen, #result-screen {
            text-align: center;
        }
        
        .btn {
            display: inline-block;
            background-color: #1e3a8a;
            color: white;
            border: none;
            padding: 12px 24px;
            border-radius: 5px;
            cursor: pointer;
            font-size: 16px;
            transition: background-color 0.3s;
            margin: 10px 5px;
        }
        
        .btn:hover {
            background-color: #2d4ba0;
        }
        
        .btn-option {
            width: 100%;
            text-align: left;
            margin: 8px 0;
            padding: 15px;
            background-color: #f8f9fa;
            border: 1px solid #dee2e6;
            border-radius: 5px;
            transition: all 0.2s;
            color: #000; /* 選項文字為黑色 */
        }
        
        .btn-option:hover {
            background-color: #e9ecef;
            border-color: #adb5bd;
        }
        
        .btn-option.correct {
            background-color: #d4edda;
            border-color: #c3e6cb;
        }
        
        .btn-option.incorrect {
            background-color: #f8d7da;
            border-color: #f5c6cb;
        }
        
        .scenario {
            background-color: white;
            padding: 20px;
            border-radius: 8px;
            margin-bottom: 20px;
            box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
        }
        
        .options {
            margin-top: 20px;
        }
        
        .feedback {
            margin-top: 20px;
            padding: 15px;
            border-radius: 5px;
            display: none;
        }
        
        .feedback.correct {
            background-color: #d4edda;
            color: #155724;
            border: 1px solid #c3e6cb;
        }
        
        .feedback.incorrect {
            background-color: #f8d7da;
            color: #721c24;
            border: 1px solid #f5c6cb;
        }
        
        .score {
            font-size: 24px;
            margin: 20px 0;
        }
        
        .hidden {
            display: none;
        }
        
        .scenario-number {
            font-size: 14px;
            color: #666;
            margin-bottom: 5px;
        }
        
        .scenario-list {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
            gap: 15px;
            margin-top: 20px;
        }
        
        .scenario-item {
            padding: 15px;
            background-color: #f8f9fa;
            border: 1px solid #dee2e6;
            border-radius: 5px;
            cursor: pointer;
            transition: all 0.2s;
        }
        
        .scenario-item:hover {
            background-color: #e9ecef;
            border-color: #adb5bd;
        }
        
        .scenario-title {
            font-weight: bold;
            margin-bottom: 5px;
        }
        
        .scenario-preview {
            font-size: 14px;
            color: #666;
            overflow: hidden;
            text-overflow: ellipsis;
            display: -webkit-box;
            -webkit-line-clamp: 2;
            -webkit-box-orient: vertical;
        }
        
        .navigation {
            display: flex;
            justify-content: space-between;
            margin-top: 20px;
        }
    </style>
</head>
<body>
    <div class="container">
        <header>
            <h1>憲法知識挑戰</h1>
            <p class="description">測試您對憲法和基本法知識的理解</p>
        </header>
        
        <div id="start-screen">
            <h2>遊戲規則</h2>
            <p>您可以選擇任意情景，根據憲法和基本法知識選擇正確的答案。</p>
            <p>每個情景有3個選項，只有一個是正確的。</p>
            <button id="start-btn" class="btn">開始遊戲</button>
        </div>
        
        <div id="scenario-selection" class="hidden">
            <h2>選擇情景</h2>
            <p>請選擇一個情景開始挑戰：</p>
            <div class="scenario-list" id="scenario-list">
                <!-- 情景列表將通過JavaScript動態添加 -->
            </div>
            <div class="navigation">
                <button id="back-to-start" class="btn">返回主頁</button>
            </div>
        </div>
        
        <div id="game-screen" class="hidden">
            <div class="scenario">
                <div class="scenario-number">情景 <span id="scenario-number">1</span></div>
                <h2 id="scenario-text">情景內容將顯示在這裡</h2>
            </div>
            
            <div class="options" id="options-container">
                <!-- 選項將通過JavaScript動態添加 -->
            </div>
            
            <div id="feedback" class="feedback">
                <!-- 反饋信息將顯示在這裡 -->
            </div>
            
            <div class="navigation">
                <button id="back-to-selection" class="btn">返回情景選擇</button>
                <button id="next-scenario" class="btn">下一個情景</button>
            </div>
        </div>
        
        <div id="result-screen" class="hidden">
            <h2>答題結果</h2>
            <p class="score">您答對了 <span id="final-score">0</span> 題，共 <span id="final-total">0</span> 題</p>
            <div class="navigation">
                <button id="back-to-selection-from-result" class="btn">返回情景選擇</button>
                <button id="restart-btn" class="btn">重新開始</button>
            </div>
        </div>
    </div>

    <script>
        // 情景數據
        const scenarios = [
            {
                id: 1,
                scenario: "某超市懷疑顧客偷竊，在無證據情況下強制搜查其身體",
                options: [
                    "合法，超市為維護秩序可自主搜查",
                    "不合法，公民人身自由不受非法侵犯（依據憲法第三十七條）",
                    "合法，若顧客拒絕則可認定為偷竊"
                ],
                correct: 1
            },
            {
                id: 2,
                scenario: "學生因是少數民族，被學校以「管理不便」為由拒絕入學",
                options: [
                    "合法，學校可自主決定招生對象",
                    "不合法，公民有平等受教育權（依據憲法第四十六條、澳門基本法第二十四條）",
                    "合法，少數民族應去專門學校就讀"
                ],
                correct: 1
            },
            {
                id: 3,
                scenario: "公司在招聘啓事中標注「僅限男性」，拒絕女性應聘某行政崗位",
                options: [
                    "合法，公司可根據崗位需求限定性別",
                    "不合法，公民有平等就業權（依據憲法第四十八條）",
                    "合法，行政崗位更適合男性"
                ],
                correct: 1
            },
            {
                id: 4,
                scenario: "澳門居民李先生在珠海參與社區居委會主任選舉",
                options: [
                    "不合法，澳門居民不能參與內地選舉",
                    "合法，李先生依法享有選舉權（依據憲法第三十四條、澳門基本法第二十一條）",
                    "合法，但需提前辦理特殊手續"
                ],
                correct: 1
            },
            {
                id: 5,
                scenario: "出版社因某書籍涉及「敏感內容」，未經作者同意擅自銷毀全部稿件",
                options: [
                    "合法，出版社為遵守規定可自主處理",
                    "不合法，公民有出版自由（依據憲法第三十五條）",
                    "合法，若內容違法則銷毀合理"
                ],
                correct: 1
            },
            {
                id: 6,
                scenario: "居民住宅因「城市規劃」，在未達成補償協議前被強制拆除",
                options: [
                    "合法，政府規劃優先於個人財產",
                    "不合法，公民合法財產不受非法侵犯（依據憲法第十三條、澳門基本法第一百零三條）",
                    "合法，居民應無條件配合規劃"
                ],
                correct: 1
            },
            {
                id: 7,
                scenario: "某社交媒體平台隨意公開用戶個人住址、聯繫方式等隱私信息",
                options: [
                    "合法，用戶註冊時已同意信息共享",
                    "不合法，公民人格尊嚴不受侵犯（依據憲法第三十八條）",
                    "合法，平台可用於商業推廣"
                ],
                correct: 1
            },
            {
                id: 8,
                scenario: "宗教團體在學校操場組織大規模宗教儀式，影響正常教學",
                options: [
                    "合法，公民有宗教信仰自由（依據憲法第三十六條）",
                    "不合法，不得在公共教育場所開展宗教活動（依據憲法第三十六條）",
                    "合法，只要學生自願參與即可"
                ],
                correct: 1
            },
            {
                id: 9,
                scenario: "用人單位以「員工懷孕會影響工作」為由將其辭退",
                options: [
                    "合法，企業可根據經營需要裁員",
                    "不合法，婦女在孕期受特殊保護（依據憲法第四十八條）",
                    "合法，懷孕員工無法勝任工作"
                ],
                correct: 1
            },
            {
                id: 10,
                scenario: "某地政府為舉辦活動，臨時徵用公民私有車輛，事後未給予任何補償",
                options: [
                    "合法，政府徵用無需補償",
                    "不合法，公民財產被徵用應獲補償（依據憲法第十三條）",
                    "合法，公民應無條件配合政府工作"
                ],
                correct: 1
            },
            {
                id: 11,
                scenario: "學校要求學生必須參加某宗教教義學習活動",
                options: [
                    "合法，有助於學生瞭解多元文化",
                    "不合法，公民有宗教信仰自由，不得強制他人信教（依據憲法第三十六條）",
                    "合法，宗教教育是特色課程"
                ],
                correct: 1
            },
            {
                id: 12,
                scenario: "澳門居民在本地申請成立非營利性公益組織，被有關部門無故拒絕",
                options: [
                    "合法，政府可自主審批社會組織",
                    "不合法，公民有結社自由（依據憲法第三十五條、澳門基本法第二十七條）",
                    "合法，公益組織需特殊資質"
                ],
                correct: 1
            },
            {
                id: 13,
                scenario: "某企業在產品包裝上標注「最佳」「最有效」等絕對化用語",
                options: [
                    "合法，企業可自主宣傳產品",
                    "不合法，公民有知情權，廣告不得虛假宣傳（憲法保障公民權利延伸出的市場規制邏輯）",
                    "合法，只要產品確實有效即可標注"
                ],
                correct: 1
            },
            {
                id: 14,
                scenario: "圖書館因讀者是殘疾人，限制其進入部分閱覽區域",
                options: [
                    "合法，為保障其他讀者權益",
                    "不合法，公民有平等文化權利（依據憲法第四十七條）",
                    "合法，殘疾人應使用專用區域"
                ],
                correct: 1
            },
            {
                id: 15,
                scenario: "某醫院因患者未繳納押金，拒絕為其進行緊急手術治療",
                options: [
                    "合法，醫院需保障運營成本",
                    "不合法，公民有生命健康權（依據憲法第三十三條）",
                    "合法，緊急手術需家屬同意"
                ],
                correct: 1
            },
            {
                id: 16,
                scenario: "某小區物業禁止租戶參與業主委員會選舉",
                options: [
                    "合法，租戶不是業主無選舉資格",
                    "不合法，公民有平等選舉權（依據憲法第三十四條）",
                    "合法，業主委員會僅業主可參與"
                ],
                correct: 1
            },
            {
                id: 17,
                scenario: "政府部門在未告知公民的情況下，公開其個人納稅信息",
                options: [
                    "合法，納稅信息屬於公共信息",
                    "不合法，公民隱私權受保護（依據憲法第三十八條）",
                    "合法，公開納稅信息利於監督"
                ],
                correct: 1
            },
            {
                id: 18,
                scenario: "某快遞公司因「貨物涉嫌違規」，在無執法權情況下拆開客戶包裹",
                options: [
                    "合法，快遞公司可自查貨物",
                    "不合法，公民通信秘密受保護（依據憲法第四十條）",
                    "合法，若懷疑違規可自主查驗"
                ],
                correct: 1
            }
        ];

        // 遊戲狀態
        let gameState = {
            currentScenarioIndex: -1,
            score: 0,
            answeredQuestions: 0,
            totalQuestions: scenarios.length
        };

        // DOM元素
        const startScreen = document.getElementById('start-screen');
        const scenarioSelection = document.getElementById('scenario-selection');
        const gameScreen = document.getElementById('game-screen');
        const resultScreen = document.getElementById('result-screen');
        const startBtn = document.getElementById('start-btn');
        const backToStart = document.getElementById('back-to-start');
        const backToSelection = document.getElementById('back-to-selection');
        const backToSelectionFromResult = document.getElementById('back-to-selection-from-result');
        const nextScenario = document.getElementById('next-scenario');
        const restartBtn = document.getElementById('restart-btn');
        const scenarioList = document.getElementById('scenario-list');
        const scenarioText = document.getElementById('scenario-text');
        const scenarioNumber = document.getElementById('scenario-number');
        const optionsContainer = document.getElementById('options-container');
        const feedback = document.getElementById('feedback');
        const finalScore = document.getElementById('final-score');
        const finalTotal = document.getElementById('final-total');

        // 初始化總題數
        finalTotal.textContent = scenarios.length;

        // 事件監聽
        startBtn.addEventListener('click', showScenarioSelection);
        backToStart.addEventListener('click', showStartScreen);
        backToSelection.addEventListener('click', showScenarioSelection);
        backToSelectionFromResult.addEventListener('click', showScenarioSelection);
        nextScenario.addEventListener('click', showScenarioSelection);
        restartBtn.addEventListener('click', restartGame);

        // 顯示情景選擇界面
        function showScenarioSelection() {
            startScreen.classList.add('hidden');
            gameScreen.classList.add('hidden');
            resultScreen.classList.add('hidden');
            scenarioSelection.classList.remove('hidden');
            
            // 生成情景列表
            scenarioList.innerHTML = '';
            scenarios.forEach((scenario, index) => {
                const scenarioItem = document.createElement('div');
                scenarioItem.className = 'scenario-item';
                scenarioItem.innerHTML = `
                    <div class="scenario-title">情景 ${scenario.id}</div>
                    <div class="scenario-preview">${scenario.scenario}</div>
                `;
                scenarioItem.addEventListener('click', () => startScenario(index));
                scenarioList.appendChild(scenarioItem);
            });
        }

        // 顯示開始界面
        function showStartScreen() {
            scenarioSelection.classList.add('hidden');
            gameScreen.classList.add('hidden');
            resultScreen.classList.add('hidden');
            startScreen.classList.remove('hidden');
        }

        // 開始特定情景
        function startScenario(index) {
            scenarioSelection.classList.add('hidden');
            gameScreen.classList.remove('hidden');
            
            gameState.currentScenarioIndex = index;
            const currentScenario = scenarios[index];
            
            // 顯示情景
            scenarioText.textContent = currentScenario.scenario;
            scenarioNumber.textContent = currentScenario.id;
            
            // 清除選項和反饋
            optionsContainer.innerHTML = '';
            feedback.classList.add('hidden');
            
            // 顯示選項
            currentScenario.options.forEach((option, optionIndex) => {
                const button = document.createElement('button');
                button.className = 'btn btn-option';
                button.textContent = `${String.fromCharCode(65 + optionIndex)}. ${option}`;
                button.addEventListener('click', () => checkAnswer(optionIndex));
                optionsContainer.appendChild(button);
            });
        }

        // 檢查答案
        function checkAnswer(selectedIndex) {
            const currentScenario = scenarios[gameState.currentScenarioIndex];
            const options = document.querySelectorAll('.btn-option');
            
            // 禁用所有選項
            options.forEach(option => {
                option.disabled = true;
            });
            
            // 標記正確和錯誤答案
            options[currentScenario.correct].classList.add('correct');
            if (selectedIndex !== currentScenario.correct) {
                options[selectedIndex].classList.add('incorrect');
            }
            
            // 顯示反饋
            feedback.classList.remove('hidden');
            if (selectedIndex === currentScenario.correct) {
                feedback.textContent = "回答正確！";
                feedback.classList.add('correct');
                feedback.classList.remove('incorrect');
                gameState.score++;
            } else {
                feedback.textContent = "回答錯誤。正確答案是選項 " + String.fromCharCode(65 + currentScenario.correct);
                feedback.classList.add('incorrect');
                feedback.classList.remove('correct');
            }
            
            // 更新答題計數
            gameState.answeredQuestions++;
        }

        // 顯示結果
        function showResult() {
            gameScreen.classList.add('hidden');
            resultScreen.classList.remove('hidden');
            finalScore.textContent = gameState.score;
        }

        // 重新開始遊戲
        function restartGame() {
            gameState = {
                currentScenarioIndex: -1,
                score: 0,
                answeredQuestions: 0,
                totalQuestions: scenarios.length
            };
            resultScreen.classList.add('hidden');
            startScreen.classList.remove('hidden');
        }

        // 初始化
        showStartScreen();
    </script>
</body>
</html>
