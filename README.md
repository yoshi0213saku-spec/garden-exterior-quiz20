<!DOCTYPE html>
<html lang="ja">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>ガーデニング・エクステリア知識クイズ20選</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Kiwi+Maru:wght@400;500&display=swap');
        
        body {
            font-family: 'Kiwi Maru', serif;
            background-color: #f0f4f0;
            color: #2d4a22;
        }
        .quiz-card {
            background: rgba(255, 255, 255, 0.95);
            border-radius: 20px;
            box-shadow: 0 10px 25px rgba(0,0,0,0.1);
        }
        .btn-choice {
            transition: all 0.2s;
            border: 2px solid #e2e8f0;
            background-color: white;
        }
        .btn-choice:hover:not(:disabled) {
            border-color: #68d391;
            background-color: #f0fff4;
            transform: translateY(-2px);
        }
        .correct {
            background-color: #c6f6d5 !important;
            border-color: #48bb78 !important;
        }
        .incorrect {
            background-color: #fed7d7 !important;
            border-color: #f56565 !important;
        }
        .fade-in {
            animation: fadeIn 0.5s ease-in;
        }
        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(10px); }
            to { opacity: 1; transform: translateY(0); }
        }
        .footer-text {
            font-size: 0.7rem;
            color: #718096;
        }
    </style>
</head>
<body class="min-h-screen flex items-center justify-center p-4">

    <div id="app" class="w-full max-w-2xl">
        <!-- トップページ -->
        <div id="start-screen" class="quiz-card p-8 text-center fade-in">
            <div id="hero-image-container" class="mb-6 rounded-xl overflow-hidden h-64 bg-green-100 flex items-center justify-center">
                <!-- GitHubでも確実に表示される高品質なガーデニング画像 -->
                <img src="https://images.unsplash.com/photo-1585320806297-9794b3e4eeae?auto=format&fit=crop&w=800&q=80" 
                     alt="Gardening" 
                     class="w-full h-full object-cover"
                     onerror="this.parentElement.innerHTML='<div class=\'text-4xl\'>🌿</div>'">
            </div>
            <h1 class="text-2xl md:text-3xl font-bold mb-4 text-green-800">ガーデニング・エクステリア<br>知識クイズ20選</h1>
            <p class="mb-8 text-gray-600">お庭づくりや植物に関する知識を試してみましょう！全20問に挑戦！</p>
            <button onclick="startQuiz()" class="bg-green-600 hover:bg-green-700 text-white font-bold py-3 px-10 rounded-full text-lg shadow-lg transition-transform active:scale-95">
                クイズを始める
            </button>
            <footer class="mt-8 pt-6 border-t border-gray-100">
                <p class="footer-text">監修 中島義健</p>
            </footer>
        </div>

        <!-- クイズ画面 -->
        <div id="quiz-screen" class="hidden quiz-card p-6 md:p-10 fade-in">
            <div class="flex justify-between items-center mb-6">
                <span id="progress" class="bg-green-100 text-green-800 px-3 py-1 rounded-full text-sm font-bold">第 1 問 / 20</span>
                <span id="score-counter" class="text-sm text-gray-500 font-bold">正解: 0</span>
            </div>
            
            <h2 id="question-text" class="text-xl font-bold mb-8 leading-relaxed"></h2>

            <div id="choices" class="grid grid-cols-1 gap-4 mb-8"></div>

            <div id="feedback" class="hidden mb-6 p-4 rounded-lg border-2 text-center">
                <p id="feedback-message" class="font-bold text-lg mb-2"></p>
                <p id="explanation" class="text-sm text-gray-700 leading-relaxed"></p>
            </div>

            <div class="flex justify-center">
                <button id="next-btn" onclick="nextQuestion()" class="hidden bg-blue-600 hover:bg-blue-700 text-white font-bold py-3 px-10 rounded-full shadow-md transition-all">
                    次の問題へ
                </button>
            </div>
        </div>

        <!-- 結果画面 -->
        <div id="result-screen" class="hidden quiz-card p-10 text-center fade-in">
            <h2 class="text-3xl font-bold mb-4 text-green-800">クイズ終了！</h2>
            <div class="text-6xl mb-6">🏆</div>
            <p class="text-xl mb-2">あなたのスコア</p>
            <div class="text-5xl font-bold text-green-600 mb-6"><span id="final-score">0</span> / 20</div>
            <p id="result-message" class="mb-8 text-gray-600"></p>
            <button onclick="location.reload()" class="bg-gray-600 hover:bg-gray-700 text-white font-bold py-3 px-10 rounded-full shadow-md">
                トップに戻る
            </button>
        </div>
    </div>

    <script>
        const quizData = [
            { q: "玄関前や庭のシンボルとして人気の高い落葉高木で、春には白やピンクの花が咲き、秋には赤い実や紅葉が楽しめる樹木はどれですか？", c: ["シラカシ", "ハナミズキ", "ゴールドクレスト", "オリーブ"], a: 1, e: "ハナミズキは四季折々の表情が楽しめるため、シンボルツリーとして非常に人気があります。" },
            { q: "日当たりが悪い庭（シェードガーデン）でも育ち、美しい葉（カラーリーフ）が庭のアクセントになる植物はどれですか？", c: ["ペチュニア", "マリーゴールド", "ギボウシ（ホスタ）", "ラベンダー"], a: 2, e: "ギボウシは半日陰や日陰を好む宿根草で、シェードガーデンの代表的な植物です。" },
            { q: "つる性の植物を絡ませたり、日陰を作ってくつろぎの空間を演出したりするために設置される、藤棚のような洋風の構造物を何と呼びますか？", c: ["パーゴラ", "トレリス", "フェンス", "ウッドデッキ"], a: 0, e: "パーゴラはつる植物を絡ませて日陰をつくるのに適しており、下のスペースを活用できます。" },
            { q: "コンクリート敷きの駐車場の目地に植えるのによく利用される、踏圧に強く丈夫な植物はどれですか？", c: ["パンジー", "リュウノヒゲ（タマリュウ）", "チューリップ", "アジサイ"], a: 1, e: "リュウノヒゲは非常に丈夫で、駐車場の目地を緑化するのによく使われます。" },
            { q: "「イングリッシュガーデン」の特徴として最も適切なものはどれですか？", c: ["石庭と松を配置した静寂な空間", "幾何学模様に刈り込まれたトピアリー中心", "自然の風景を活かし、多年草やレンガを用いたナチュラルな雰囲気", "コンクリートとガラスを用いた都会的なデザイン"], a: 2, e: "イングリッシュガーデンは、自然の風景を模してナチュラルに演出するのが特徴です。" },
            { q: "壁面や狭いスペースを有効活用して、つる植物を立体的に飾るために使われる格子状のパネルを何と呼びますか？", c: ["コンテナ", "トレリス（ラティス）", "バードバス", "枕木"], a: 1, e: "トレリスやつる性植物を絡ませて目隠しにしたり、壁面を飾ったりするのに欠かせません。" },
            { q: "「香りの庭」を作るのにおすすめで、紫色の花と素晴らしい香りが特徴のハーブはどれですか？", c: ["アイビー", "ラベンダー", "ワイヤープランツ", "コニファー"], a: 1, e: "ラベンダーは香りが良く、ポプリなどにも利用される人気のハーブです。" },
            { q: "春に花を楽しむために、前年の秋（10月〜11月頃）に植え付ける球根植物はどれですか？", c: ["チューリップ", "グラジオラス", "ダリア", "カンナ"], a: 0, e: "チューリップは秋植え球根の代表格です。冬の寒さに当たることで開花します。" },
            { q: "地面を覆うように広がり、雑草の繁殖を抑えたり土の乾燥を防いだりするために植える植物の総称は何ですか？", c: ["シンボルツリー", "寄生植物", "グランドカバープランツ", "ハンギング"], a: 2, e: "アジュガやタイムなど地面を這う植物は、庭の緑化や雑草対策に利用されます。" },
            { q: "庭に設置する、立ったまま使える高さのある水道設備のことを何と呼びますか？", c: ["散水栓", "立水栓", "井戸", "貯水タンク"], a: 1, e: "立水栓は屈まずに水やりができ、デザイン性の高いものは庭のアクセントになります。" },
            { q: "寒さに強く、冬から春にかけての庭を彩る、スミレ科の一年草はどれですか？", c: ["アサガオ", "ヒマワリ", "パンジー（ビオラ）", "サルビア"], a: 2, e: "パンジーやビオラは耐寒性が強く、冬のガーデニングに欠かせない植物です。" },
            { q: "アンティークな雰囲気や温かみを出すために、アプローチや花壇によく使われる焼き固められた土の素材は何ですか？", c: ["御影石", "レンガ", "コンクリートブロック", "プラスチック"], a: 1, e: "レンガは洋風の庭によく合い、時が経つにつれて味わいが出る素材です。" },
            { q: "庭の土がない場所や壁面を利用して、バスケットを吊るす手法を何と呼びますか？", c: ["ロックガーデン", "ハンギングバスケット", "寄せ植え", "地植え"], a: 1, e: "ハンギングバスケットは空中を利用して植物を飾るため、狭い場所でも楽しめます。" },
            { q: "日本の園芸で基本の土として最も多く使われる「赤い粒状の土」は何ですか？", c: ["腐葉土", "赤玉土", "鹿沼土", "ピートモス"], a: 1, e: "赤玉土は清潔でバランスが良く、多くの植物の基本用土として使われます。" },
            { q: "咲き終わった花を摘み取り、株の消耗を防いで次の花を咲かせやすくする作業を何と言いますか？", c: ["剪定", "施肥", "花がら摘み", "マルチング"], a: 2, e: "花がら摘みは病気を防いだり、開花期間を長くしたりする大切な作業です。" },
            { q: "門扉や塀を設けず、道路と敷地を遮断しない開放的な外構スタイルのことを何と呼びますか？", c: ["クローズドスタイル", "オープンスタイル", "セミクローズドスタイル", "和風スタイル"], a: 1, e: "オープンスタイルは街並みに開放感を与え、植物で柔らかく仕切るデザインです。" },
            { q: "夜の庭で樹木を下から照らしたり、足元の安全を確保したりするアイテムは何ですか？", c: ["バードバス", "ガーデンライト", "トレリス", "アーチ"], a: 1, e: "ライトアップは防犯だけでなく、夜の庭を幻想的に演出する効果があります。" },
            { q: "秋になると葉が赤く色づき、紅葉狩りの対象としても親しまれているカエデ科の落葉樹は何ですか？", c: ["シラカシ", "オリーブ", "モミジ", "ユーカリ"], a: 2, e: "モミジは和洋問わず庭の季節感を演出するのに非常に適した樹木です。" },
            { q: "針葉樹の総称で、種類が豊富で常緑のため冬でも庭に緑を提供してくれる植物群は何ですか？", c: ["ハーブ", "バラ", "コニファー", "多肉植物"], a: 2, e: "コニファーは多様な色や樹形があり、洋風ガーデンの目隠し等にも利用されます。" },
            { q: "初夏に赤い実をつけ、生食やジャムにでき、花や紅葉も美しい人気の果樹はどれですか？", c: ["アオキ", "ジューンベリー", "コニファー", "ハナミズキ"], a: 1, e: "ジューンベリーは四季を通じて楽しめるため、シンボルツリーとして人気です。" }
        ];

        let currentQuestion = 0;
        let score = 0;

        // オーディオ合成
        const audioCtx = new (window.AudioContext || window.webkitAudioContext)();
        function playSound(type) {
            if (audioCtx.state === 'suspended') audioCtx.resume();
            const osc = audioCtx.createOscillator();
            const gain = audioCtx.createGain();
            osc.connect(gain);
            gain.connect(audioCtx.destination);
            const now = audioCtx.currentTime;

            if (type === 'correct') {
                osc.type = 'sine';
                osc.frequency.setValueAtTime(523.25, now);
                osc.frequency.exponentialRampToValueAtTime(659.25, now + 0.1);
                gain.gain.setValueAtTime(0.1, now);
                gain.gain.exponentialRampToValueAtTime(0.01, now + 0.4);
                osc.start(now);
                osc.stop(now + 0.4);
            } else {
                osc.type = 'sawtooth';
                osc.frequency.setValueAtTime(110.00, now);
                gain.gain.setValueAtTime(0.05, now);
                gain.gain.exponentialRampToValueAtTime(0.01, now + 0.5);
                osc.start(now);
                osc.stop(now + 0.5);
            }
        }

        function startQuiz() {
            document.getElementById('start-screen').classList.add('hidden');
            document.getElementById('quiz-screen').classList.remove('hidden');
            showQuestion();
        }

        function showQuestion() {
            const data = quizData[currentQuestion];
            document.getElementById('progress').innerText = `第 ${currentQuestion + 1} 問 / ${quizData.length}`;
            document.getElementById('question-text').innerText = data.q;
            
            const choicesContainer = document.getElementById('choices');
            choicesContainer.innerHTML = '';
            
            data.c.forEach((choice, index) => {
                const btn = document.createElement('button');
                btn.className = "btn-choice text-left p-4 rounded-xl font-medium shadow-sm";
                btn.innerText = `${index + 1}. ${choice}`;
                btn.onclick = () => selectChoice(index);
                choicesContainer.appendChild(btn);
            });

            document.getElementById('feedback').classList.add('hidden');
            document.getElementById('next-btn').classList.add('hidden');
        }

        function selectChoice(index) {
            const data = quizData[currentQuestion];
            const buttons = document.querySelectorAll('.btn-choice');
            buttons.forEach(btn => btn.disabled = true);

            const feedback = document.getElementById('feedback');
            const feedbackMsg = document.getElementById('feedback-message');
            const explanation = document.getElementById('explanation');
            feedback.classList.remove('hidden');
            
            if (index === data.a) {
                score++;
                document.getElementById('score-counter').innerText = `正解: ${score}`;
                buttons[index].classList.add('correct');
                feedbackMsg.innerText = "✨ 正解！";
                feedbackMsg.className = "font-bold text-lg mb-2 text-green-600";
                feedback.style.borderColor = "#48bb78";
                playSound('correct');
            } else {
                buttons[index].classList.add('incorrect');
                buttons[data.a].classList.add('correct');
                feedbackMsg.innerText = "❌ 残念！";
                feedbackMsg.className = "font-bold text-lg mb-2 text-red-600";
                feedback.style.borderColor = "#f56565";
                playSound('incorrect');
            }

            explanation.innerText = data.e;
            document.getElementById('next-btn').classList.remove('hidden');
        }

        function nextQuestion() {
            currentQuestion++;
            if (currentQuestion < quizData.length) {
                showQuestion();
            } else {
                showResult();
            }
        }

        function showResult() {
            document.getElementById('quiz-screen').classList.add('hidden');
            document.getElementById('result-screen').classList.remove('hidden');
            document.getElementById('final-score').innerText = score;
            
            let message = "";
            if (score === 20) message = "完璧です！あなたはお庭マスターですね！";
            else if (score >= 15) message = "素晴らしい！かなりのガーデニング通です。";
            else if (score >= 10) message = "合格点です！もっとお庭を楽しんでくださいね。";
            else message = "もう少しお庭の勉強をしてみましょう！";
            
            document.getElementById('result-message').innerText = message;
        }
    </script>
</body>
</html>
