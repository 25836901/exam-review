<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=yes">
    <title>公共营养师三级 · 全题库复习刷题模型</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            -webkit-tap-highlight-color: transparent;
        }
        body {
            background: linear-gradient(145deg, #eef2f9 0%, #dce5f0 100%);
            font-family: 'Segoe UI', Roboto, system-ui, sans-serif;
            padding: 1.5rem 1rem;
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
        }
        .quiz-container {
            max-width: 880px;
            width: 100%;
            background: white;
            border-radius: 2rem;
            box-shadow: 0 20px 40px -12px rgba(0,0,0,0.2);
            overflow: hidden;
        }
        .quiz-header {
            background: #1e4a2f;
            padding: 1.2rem 1.8rem;
            color: white;
        }
        .title {
            display: flex;
            justify-content: space-between;
            align-items: baseline;
            flex-wrap: wrap;
            gap: 0.5rem;
        }
        .title h1 {
            font-size: 1.5rem;
            font-weight: 600;
        }
        .progress-badge {
            background: #ffda88;
            color: #2c4a1e;
            padding: 0.3rem 1rem;
            border-radius: 40px;
            font-weight: 700;
        }
        .stats {
            display: flex;
            justify-content: space-between;
            margin-top: 0.8rem;
            font-size: 0.85rem;
            opacity: 0.9;
        }
        .quiz-card {
            padding: 1.8rem;
        }
        .question-text {
            font-size: 1.35rem;
            font-weight: 600;
            line-height: 1.4;
            background: #f8fafc;
            padding: 0.8rem 1rem;
            border-radius: 1.5rem;
            border-left: 5px solid #2b8c4a;
            margin-bottom: 1.8rem;
        }
        .options-list {
            display: flex;
            flex-direction: column;
            gap: 0.8rem;
            margin-bottom: 1.8rem;
        }
        .option-item {
            background: #ffffff;
            border: 2px solid #e2e8f0;
            border-radius: 1.2rem;
            padding: 0.8rem 1.2rem;
            display: flex;
            align-items: center;
            cursor: pointer;
            transition: all 0.2s;
            font-weight: 500;
        }
        .option-item:hover {
            background: #eff6ee;
            border-color: #86b37b;
            transform: translateX(4px);
        }
        .option-prefix {
            font-weight: 800;
            background: #eef2f5;
            width: 32px;
            height: 32px;
            display: inline-flex;
            align-items: center;
            justify-content: center;
            border-radius: 50%;
            margin-right: 1rem;
            color: #2a6230;
        }
        .feedback-area {
            background: #fef7e0;
            border-radius: 1.2rem;
            padding: 1rem;
            margin: 0.5rem 0 1rem;
            border-left: 5px solid #f5a623;
            font-size: 0.95rem;
        }
        .correct-feedback {
            background: #e0f5e8;
            border-left-color: #2c8c4a;
            color: #145c2e;
        }
        .wrong-feedback {
            background: #ffeae9;
            border-left-color: #cf4444;
            color: #aa2e2e;
        }
        .next-btn {
            background: #2c7a4a;
            border: none;
            width: 100%;
            padding: 0.8rem;
            font-weight: 700;
            color: white;
            border-radius: 60px;
            cursor: pointer;
            font-size: 1rem;
            margin-top: 0.5rem;
        }
        .next-btn:hover {
            background: #1f623b;
        }
        .restart-btn {
            background: #445c66;
            margin-top: 0.6rem;
        }
        .restart-btn:hover {
            background: #2f454f;
        }
        footer {
            font-size: 0.7rem;
            text-align: center;
            padding: 1rem;
            border-top: 1px solid #e2e8e6;
            color: #6b8c6b;
        }
        @media (max-width: 550px) {
            .quiz-card { padding: 1.2rem; }
            .question-text { font-size: 1.1rem; }
        }
    </style>
</head>
<body>
<div class="quiz-container" id="app">
    <div class="quiz-header">
        <div class="title">
            <h1>📚 公共营养师三级 · 全题库</h1>
            <span class="progress-badge" id="progressText">✔️ 精校版</span>
        </div>
        <div class="stats">
            <span>✅ 选对自动下一题 &nbsp;|&nbsp; ❌ 选错显示正确答案</span>
            <span id="questionCounter" style="background:#2b5e3a; padding:0.2rem 0.8rem; border-radius:20px;">第1 / 0题</span>
        </div>
    </div>
    <div class="quiz-card">
        <div class="question-text" id="questionText">加载中…</div>
        <div class="options-list" id="optionsContainer"></div>
        <div id="feedbackArea" class="feedback-area" style="display: none;"></div>
        <button id="nextBtn" class="next-btn" style="display: none;">➡ 下一题</button>
        <button id="restartBtn" class="next-btn restart-btn">🔄 重新开始 / 重置</button>
    </div>
    <footer>⭐ 题目来源：技能考核知识 + 三级理论题库 + 理论知识题库（共186道单选题，答案严格对照官方标准）</footer>
</div>

<script>
// --------------------------------------------------------------
// 完整题库（整合三份文件中的所有单选题 + 部分案例题改编）
// 答案严格按照文件末尾的标准答案列表
// 总计 186 题，覆盖全部考点
// --------------------------------------------------------------
const FULL_QUESTIONS = [
    // ========== 第一部分：技能考核知识案例题（改编为单选）==========
    { id:1, text:"张先生，男，35岁，身高180cm，体重76kg，其标准体重(kg)是多少？", options:["75","78","80","85"], answer:"A", explanation:"标准体重(kg)=身高(cm)-105 =75kg。" },
    { id:2, text:"张先生的标准体重指数(实际体重-标准体重)/标准体重×100% 约为？", options:["4%","1.3%","20%","15%"], answer:"B", explanation:"(76-75)/75×100%=1.33%，约1.3%。" },
    { id:3, text:"张先生的体质指数(BMI)是？", options:["23.5","19.4","27.0","28.2"], answer:"A", explanation:"76÷(1.8²)=76÷3.24=23.46，约23.5。" },
    { id:4, text:"婴幼儿哭闹无法进行体重测量时可采用？", options:["减差法","扣除衣物法","直接称重法","间接测量法"], answer:"A", explanation:"减差法：抱婴儿总重减母亲体重。" },
    { id:5, text:"婴幼儿头围测量软尺零点应固定在头部？", options:["枕骨粗隆","左侧眉弓上缘","右侧眉弓上缘","右侧眉弓下缘"], answer:"C", explanation:"右侧眉弓上缘→枕骨粗隆→回至原点。" },
    { id:6, text:"测量婴幼儿胸围时，皮下脂肪较厚者软尺应？", options:["轻轻接触皮肤","与皮肤接触稍紧些","紧贴皮肤","松弛一些"], answer:"B", explanation:"稍紧以抵消脂肪层误差。" },
    // 缺铁性贫血计算题改编
    { id:7, text:"某街道60岁以上女性9608人，男性8000人，总17608人，女性构成比约为？", options:["45.4%","54.6%","50.2%","48.7%"], answer:"B", explanation:"9608/17608×100%=54.57%≈54.6%。" },
    { id:8, text:"A小区缺铁性贫血新病例546例，人口4532，发病率是？", options:["12.05%","10.85%","8.3%","15.2%"], answer:"A", explanation:"546/4532×100%=12.05%。" },
    // 人群能量计算（标准人系数）
    { id:9, text:"轻体力成年男性每日能量推荐量（kcal）是？", options:["2100","2200","2400","260
