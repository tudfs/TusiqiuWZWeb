[index.txt](https://github.com/user-attachments/files/27567973/index.txt)[Uploading index.txt…]<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>兔思秋的网站</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background-image: url('images/5586D01C0075F5892EF98C88A41345A8.jpg');
            background-size: cover;
            background-position: center;
            background-attachment: fixed;
            background-repeat: no-repeat;
            min-height: 100vh;
            color: white;
            position: relative;
            overflow-x: hidden;
        }

        #petal-canvas {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: 9999;
            pointer-events: none;
        }

        .glass-top {
            position: fixed;
            top: 0;
            left: 0;
            right: 0;
            height: 250px;
            background: linear-gradient(to bottom, rgba(0, 0, 0, 0.3), transparent);
            backdrop-filter: blur(20px);
            -webkit-backdrop-filter: blur(20px);
            z-index: 100;
        }

        .header-content {
            position: fixed;
            top: 0;
            left: 0;
            right: 0;
            padding: 20px 40px;
            display: flex;
            justify-content: space-between;
            align-items: flex-start;
            z-index: 101;
            height: 250px;
        }

        .quote-text {
            position: absolute;
            left: 50%;
            top: 40%;
            transform: translate(-50%, -50%);
            font-size: 24px;
            font-weight: 300;
            color: rgba(255, 255, 255, 0.95);
            text-shadow: 0 2px 15px rgba(0, 0, 0, 0.4);
            letter-spacing: 5px;
            font-style: italic;
        }

        .avatar {
            width: 100px;
            height: 100px;
            border-radius: 50%;
            overflow: hidden;
            border: 3px solid rgba(255, 255, 255, 0.3);
            box-shadow: 0 5px 20px rgba(0, 0, 0, 0.3);
        }

        .avatar img {
            width: 100%;
            height: 100%;
            object-fit: cover;
        }

        .time-panel {
            text-align: right;
            backdrop-filter: blur(10px);
            -webkit-backdrop-filter: blur(10px);
            background: rgba(255, 255, 255, 0.1);
            border: 1px solid rgba(255, 255, 255, 0.2);
            border-radius: 15px;
            padding: 15px 25px;
        }

        .time {
            font-size: 36px;
            font-weight: 300;
            letter-spacing: 3px;
        }

        .date {
            font-size: 14px;
            opacity: 0.8;
            margin-top: 5px;
        }

        .music-player {
            position: fixed;
            top: 160px;
            left: 40px;
            backdrop-filter: blur(15px);
            -webkit-backdrop-filter: blur(15px);
            background: rgba(255, 255, 255, 0.1);
            border: 1px solid rgba(255, 255, 255, 0.2);
            border-radius: 20px;
            padding: 20px;
            display: flex;
            flex-direction: column;
            align-items: center;
            gap: 12px;
            z-index: 101;
            width: 200px;
        }

        .music-cover {
            width: 100px;
            height: 100px;
            border-radius: 50%;
            background: rgba(255, 255, 255, 0.1);
            display: flex;
            justify-content: center;
            align-items: center;
        }

        .cover-circle {
            width: 80px;
            height: 80px;
            border-radius: 50%;
            background-image: url('images/ypzp.jpg');
            background-size: cover;
            background-position: center;
        }

        @keyframes rotate {
            from { transform: rotate(0deg); }
            to { transform: rotate(360deg); }
        }

        .music-info {
            text-align: center;
        }

        .music-title {
            font-size: 16px;
            font-weight: 600;
        }

        .music-artist {
            font-size: 12px;
            opacity: 0.7;
        }

        .music-time {
            font-size: 12px;
            opacity: 0.8;
            text-align: center;
        }

        .music-controls {
            display: flex;
            gap: 15px;
        }

        .play-btn {
            width: 40px;
            height: 40px;
            border-radius: 50%;
            border: none;
            background: rgba(255, 255, 255, 0.2);
            color: white;
            font-size: 16px;
            cursor: pointer;
            transition: all 0.3s;
        }

        .play-btn:hover {
            background: rgba(255, 255, 255, 0.3);
            transform: scale(1.1);
        }

        .music-progress {
            width: 100%;
        }

        .progress-bar-small {
            height: 3px;
            background: rgba(255, 255, 255, 0.2);
            border-radius: 2px;
            overflow: hidden;
        }

        .progress-small {
            height: 100%;
            background: linear-gradient(90deg, #667eea, #764ba2);
            width: 0%;
            transition: width 0.1s;
        }

        .music-lyrics {
            width: 100%;
            padding: 10px 0;
            text-align: center;
            overflow: hidden;
            height: 60px;
            display: flex;
            flex-direction: column;
            justify-content: center;
        }

        .lyric-line {
            font-size: 14px;
            color: rgba(255, 255, 255, 0.85);
            text-shadow: 0 1px 5px rgba(0, 0, 0, 0.3);
            transition: opacity 0.3s, transform 0.3s;
            line-height: 1.6;
            min-height: 24px;
        }

        .lyric-line.active {
            color: rgba(255, 255, 255, 0.95);
            font-size: 15px;
            font-weight: 500;
        }

        .lyric-line.prev {
            opacity: 0.5;
            font-size: 13px;
            transform: translateY(-10px);
        }

        .lyric-line.next {
            opacity: 0.5;
            font-size: 13px;
            transform: translateY(10px);
        }

        .content-grid {
            padding-top: 280px;
            padding-left: 35%;
            padding-right: 40px;
            padding-bottom: 120px;
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 20px;
            z-index: 1;
            position: relative;
            max-width: 1400px;
            margin: 0 auto;
        }

        .card {
            backdrop-filter: blur(15px);
            -webkit-backdrop-filter: blur(15px);
            background: rgba(255, 255, 255, 0.1);
            border: 1px solid rgba(255, 255, 255, 0.2);
            border-radius: 20px;
            padding: 25px;
            transition: transform 0.3s, box-shadow 0.3s;
            cursor: pointer;
        }

        .card:hover {
            transform: translateY(-5px);
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.3);
        }

        .card-icon {
            font-size: 32px;
            margin-bottom: 15px;
        }

        .card-title {
            font-size: 18px;
            font-weight: 600;
            margin-bottom: 8px;
        }

        .card-desc {
            font-size: 14px;
            opacity: 0.7;
            margin-bottom: 15px;
        }

        .card-footer {
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .card-btn {
            padding: 8px 16px;
            border-radius: 20px;
            border: none;
            background: rgba(255, 255, 255, 0.2);
            color: white;
            font-size: 13px;
            cursor: pointer;
            transition: all 0.3s;
        }

        .card-btn:hover {
            background: rgba(255, 255, 255, 0.3);
        }

        .card-arrow {
            font-size: 20px;
            opacity: 0.5;
        }

        @media (max-width: 1024px) {
            .content-grid {
                grid-template-columns: repeat(2, 1fr);
                padding-left: 280px;
            }
        }

        @media (max-width: 768px) {
            .content-grid {
                grid-template-columns: 1fr;
                padding-left: 40px;
            }
            
            .header-content {
                padding: 15px 20px;
            }
            
            .time-panel {
                padding: 10px 15px;
            }
            
            .time {
                font-size: 24px;
            }
            
            .quote-text {
                font-size: 18px;
            }
        }
    </style>
</head>
<body>
    <canvas id="petal-canvas"></canvas>
    <div class="glass-top"></div>
    
    <div class="header-content">
        <div class="avatar">
            <img src="images/touxiang.jpg" alt="我的头像">
        </div>
        
        <div class="quote-text">
            采得芝兰香满袖，携来月色照心明。
        </div>
        
        <div class="time-panel">
            <div class="time" id="time">16:22:09</div>
            <div class="date" id="date">2025年02月17日 星期一</div>
        </div>
    </div>

    <div class="content-grid">
        <div class="card">
            <div class="card-icon">👤</div>
            <div class="card-title">个人资料</div>
            <div class="card-desc">了解更多关于我</div>
            <div class="card-footer">
                <button class="card-btn">查看</button>
                <span class="card-arrow">›</span>
            </div>
        </div>

        <div class="card">
            <div class="card-icon">💼</div>
            <div class="card-title">技能</div>
            <div class="card-desc">掌握的技能和专长</div>
            <div class="card-footer">
                <button class="card-btn">查看</button>
                <span class="card-arrow">›</span>
            </div>
        </div>

        <div class="card">
            <div class="card-icon">🎮</div>
            <div class="card-title">游戏空间</div>
            <div class="card-desc">游戏成就和记录</div>
            <div class="card-footer">
                <button class="card-btn">进入</button>
                <span class="card-arrow">›</span>
            </div>
        </div>

        <div class="card">
            <div class="card-icon">🔍</div>
            <div class="card-title">个人探索</div>
            <div class="card-desc">探索我的兴趣世界</div>
            <div class="card-footer">
                <button class="card-btn">探索</button>
                <span class="card-arrow">›</span>
            </div>
        </div>

        <div class="card">
            <div class="card-icon">📤</div>
            <div class="card-title">分享</div>
            <div class="card-desc">分享我的生活点滴</div>
            <div class="card-footer">
                <button class="card-btn">查看</button>
                <span class="card-arrow">›</span>
            </div>
        </div>

        <div class="card">
            <div class="card-icon">💬</div>
            <div class="card-title">留言</div>
            <div class="card-desc">留下你的足迹</div>
            <div class="card-footer">
                <button class="card-btn">留言</button>
                <span class="card-arrow">›</span>
            </div>
        </div>
    </div>

    <div class="music-player">
        <div class="music-cover">
            <div class="cover-circle"></div>
        </div>
        <div class="music-info">
            <div class="music-title">知我</div>
            <div class="music-artist">背景音乐</div>
        </div>
        <div class="music-time">
            <span id="current-time">0:00</span> / <span id="total-time">0:00</span>
        </div>
        <div class="music-controls">
            <button class="play-btn" id="prev-btn">◀</button>
            <button class="play-btn" id="play-btn">▶</button>
            <button class="play-btn" id="next-btn">▶▶</button>
        </div>
        <div class="music-progress">
            <div class="progress-bar-small">
                <div class="progress-small" id="progress-small"></div>
            </div>
        </div>
        <div class="music-lyrics" id="music-lyrics">
            <div class="lyric-line">--</div>
        </div>
    </div>

    <audio id="audio-player">

    <script>
        function updateTime() {
            const now = new Date();
            const hours = String(now.getHours()).padStart(2, '0');
            const minutes = String(now.getMinutes()).padStart(2, '0');
            const seconds = String(now.getSeconds()).padStart(2, '0');
            document.getElementById('time').textContent = hours + ':' + minutes + ':' + seconds;
            
            const year = now.getFullYear();
            const month = String(now.getMonth() + 1).padStart(2, '0');
            const day = String(now.getDate()).padStart(2, '0');
            const weekDays = ['星期日', '星期一', '星期二', '星期三', '星期四', '星期五', '星期六'];
            const weekDay = weekDays[now.getDay()];
            document.getElementById('date').textContent = year + '年' + month + '月' + day + '日 ' + weekDay;
        }
        
        updateTime();
        setInterval(updateTime, 1000);

        const audioPlayer = document.getElementById('audio-player');
        const musicTitle = document.querySelector('.music-title');
        const playBtn = document.getElementById('play-btn');
        const prevBtn = document.getElementById('prev-btn');
        const nextBtn = document.getElementById('next-btn');
        const progressSmall = document.getElementById('progress-small');
        let isPlaying = false;
        let currentSongIndex = 0;

        const songs = [
            { title: '知我', src: 'music/song1.mp3' },
            { title: '时光卷轴', src: 'music/song2.mp3' },
            { title: '小嫦娥和小兔子', src: 'music/song3.mp3' },
        ];

        const lyricsContainer = document.getElementById('music-lyrics');
        let currentLyricIndex = -1;
        
        const songLyrics = [
            [
                { time: 0, text: '--' },
                { time: 36, text: '月夕江皱秋波' },
                { time: 39, text: '满船清梦压星河' },
                { time: 42, text: '但有夜雀无人和悲歌' },
                { time: 45, text: '削桐作琴看山色' },
                { time: 48, text: '忽闻有长歌' },
                { time: 51, text: '蓑衣沾露渔樵夜归客' },
                { time: 54, text: '和青山奏江河' },
                { time: 57, text: '我知青山江河乐' },
                { time: 60, text: '抚琴为人 无人知我乐' },
                { time: 63, text: '洋洋兮又复巍峨' },
                { time: 66, text: '来客忽笑我' },
                { time: 69, text: '声声所念 来人皆可得' },
                { time: 72, text: '徒余留 明月忆往昔' },
                { time: 75, text: '温酒会知音' },
                { time: 78, text: '借问人间 知我者能有几' },
                { time: 81, text: '三尺瑶琴碎骨兮' },
                { time: 84, text: '似绝弦断悲心' },
                { time: 87, text: '孑然一身 苍茫天地兮' },
                { time: 90, text: '天即亮 草霜凉' },
                { time: 93, text: '弦上心音为谁断' },
                { time: 96, text: '薄雾阑珊 不觉琴音乱' },
                { time: 99, text: '待至来年又月圆' },
                { time: 102, text: '海棠花烂漫' },
                { time: 105, text: '再抚七弦 阔阔与君谈' },
                { time: 108, text: '徒余留 明月忆往昔' },
                { time: 111, text: '温酒会知音' },
                { time: 114, text: '借问人间 知我者能有几' },
                { time: 117, text: '三尺瑶琴碎骨兮' },
                { time: 120, text: '似绝弦断悲心' },
                { time: 123, text: '孑然一身 苍茫天地兮' },
                { time: 126, text: '春秋转 旧人不在 孤冢寒' },
                { time: 129, text: '高山流水只为君挽' },
                { time: 132, text: '残梦回还 曲终不复弹' },
                { time: 135, text: '徒余留 明月忆往昔' },
                { time: 138, text: '温酒会知音' },
                { time: 141, text: '借问人间 知我者能有几' },
                { time: 144, text: '三尺瑶琴碎骨兮' },
                { time: 147, text: '似绝弦断悲心' },
                { time: 150, text: '孑然一身 苍茫天地兮' },
            ],
            [
                { time: 0, text: '--' },
                { time: 48, text: '镀金的树梢' },
                { time: 51, text: '蔷薇铺洒了满地' },
                { time: 54, text: '鸢尾高' },
                { time: 57, text: '水晶球中的世界' },
                { time: 60, text: '静悄悄' },
                { time: 63, text: '我抱琴而来' },
                { time: 66, text: '琉璃窗外试曲调' },
                { time: 69, text: '唱歌谣' },
                { time: 72, text: '墙壁斑驳的城堡依然不老' },
                { time: 75, text: '久别的公主啊' },
                { time: 78, text: '露珠缀满白裙角' },
                { time: 81, text: '在闪耀' },
                { time: 84, text: '城墙外有糖果屋' },
                { time: 87, text: '水晶桥' },
                { time: 90, text: '请满饮果酒' },
                { time: 93, text: '跟着肩上知更鸟' },
                { time: 96, text: '下古堡' },
                { time: 99, text: '这里花香馥郁' },
                { time: 102, text: '海潮奏叹咏调' },
                { time: 105, text: '夜风柔吹' },
                { time: 108, text: '星尘轻吻着海水' },
                { time: 111, text: '为你织金缀萤火花蕊' },
                { time: 114, text: '为你谱辰光熹微' },
                { time: 117, text: '乘着黑骏马看 古堡森巍' },
                { time: 120, text: '裙袖卷飞花染 山林苍翠' },
                { time: 123, text: '时光拨动竖琴' },
                { time: 126, text: '远古巨龙' },
                { time: 129, text: '侍守玫瑰' },
                { time: 132, text: '游吟诗人来' },
                { time: 135, text: '湛蓝双眸微微笑' },
                { time: 138, text: '簇波涛' },
                { time: 141, text: '臂上珠链窸窣摇' },
                { time: 144, text: '轻纱绕' },
                { time: 147, text: '狡黠的黑猫' },
                { time: 150, text: '卷着尾巴蹭袖角' },
                { time: 153, text: '像撒娇' },
                { time: 156, text: '你唱花野星火下坠夜雪上飘' },
                { time: 159, text: '夜风柔吹' },
                { time: 162, text: '星辰燃亮了海水' },
                { time: 165, text: '为你织金缀萤火花蕊' },
                { time: 168, text: '为你谱辰光熹微' },
                { time: 171, text: '乘着黑骏马看 古堡森巍' },
                { time: 174, text: '裙袖卷飞花染 山林苍翠' },
                { time: 177, text: '时光拨动竖琴' },
                { time: 180, text: '远古巨龙' },
                { time: 183, text: '侍守玫瑰' },
                { time: 186, text: '紫色风铃花催' },
                { time: 189, text: '月色它流连不回' },
                { time: 192, text: '等你拨弦唱时光幽微' },
                { time: 195, text: '等满园盛开蔷薇' },
                { time: 198, text: '风光恰正好轻拂过眼眉' },
                { time: 201, text: '笑靥如繁花映星月交辉' },
                { time: 204, text: '发梢蔓延年岁' },
                { time: 207, text: '你是宝藏 是世间的奇瑰' },
            ],
            [
                { time: 0, text: '--' },
                { time: 22, text: '（月兔）时辰尚早' },
                { time: 25, text: '（嫦娥）携手出逃' },
                { time: 28, text: '（月兔）天上宫阙' },
                { time: 31, text: '（嫦娥）世间万象' },
                { time: 34, text: '（月兔）夜市' },
                { time: 37, text: '（嫦娥）人潮' },
                { time: 40, text: '（合）熙熙攘攘凑热闹' },
                { time: 43, text: '（嫦娥）二十四桥明月满' },
                { time: 46, text: '天外别有江山' },
                { time: 49, text: '观潮 燃灯 猜谜不晚' },
                { time: 52, text: '（月兔）小和尚一心修禅' },
                { time: 55, text: '今儿个早早下山' },
                { time: 58, text: '提俗世一盏 饮杯清淡' },
                { time: 61, text: '（嫦娥）他都不能吃肉嘛' },
                { time: 64, text: '风卷 花前 公子好个摇扇' },
                { time: 67, text: '（月兔）这是在演杂耍么' },
                { time: 70, text: '（嫦娥）顾盼流连 下次何时再见' },
                { time: 73, text: '（月兔）时辰尚早' },
                { time: 76, text: '（嫦娥）携手出逃' },
                { time: 79, text: '（月兔）天上宫阙' },
                { time: 82, text: '（嫦娥）世间万象' },
                { time: 85, text: '（月兔）夜市' },
                { time: 88, text: '（嫦娥）人潮' },
                { time: 91, text: '（合）熙熙攘攘凑热闹' },
                { time: 94, text: '（嫦娥）烟雨行船' },
                { time: 97, text: '（月兔）一色潋滟' },
                { time: 100, text: '（嫦娥）花灯祈愿' },
                { time: 103, text: '（月兔）许下团圆' },
                { time: 106, text: '（合）赏花赏月赏你' },
                { time: 109, text: '赏此夜不记归期' },
                { time: 112, text: '（月兔）何求知己相逢晚' },
                { time: 115, text: '萍水侃侃而谈' },
                { time: 118, text: '唇角 眉间 兴致正酣' },
                { time: 121, text: '豆沙馅的最好吃啦' },
                { time: 124, text: '（嫦娥）百岁无忧多清欢' },
                { time: 127, text: '盛世一如从前' },
                { time: 130, text: '妙舞寻轻歌 烟花漫漫' },
                { time: 133, text: '（月兔）哇 好漂亮的烟花' },
                { time: 136, text: '（嫦娥）聊个新鲜 一宿留宿人间' },
                { time: 139, text: '（月兔）说道今日那少年郎啊 他' },
                { time: 142, text: '（嫦娥）嗯 怎么脸红啦' },
                { time: 145, text: '（月兔）计较个与谁并肩 共长河日月' },
                { time: 148, text: '（月兔）时辰尚早' },
                { time: 151, text: '（嫦娥）携手出逃' },
                { time: 154, text: '（月兔）天上宫阙' },
                { time: 157, text: '（嫦娥）世间万象' },
                { time: 160, text: '（月兔）夜市' },
                { time: 163, text: '（嫦娥）人潮' },
                { time: 166, text: '（合）熙熙攘攘凑热闹' },
                { time: 169, text: '（嫦娥）烟雨行船' },
                { time: 172, text: '（月兔）一色潋滟' },
                { time: 175, text: '（嫦娥）花灯祈愿' },
                { time: 178, text: '（月兔）许下团圆' },
                { time: 181, text: '（合）赏花赏月赏你' },
                { time: 184, text: '赏此夜不记归期' },
                { time: 187, text: '（嫦娥）喜欢这里吗' },
                { time: 190, text: '（月兔）喜欢' },
                { time: 193, text: '（嫦娥）别光顾着玩 明天回去还要捣药呢' },
                { time: 196, text: '（月兔）捣年糕行不行呀' },
                { time: 199, text: '（嫦娥）就知道吃' },
                { time: 202, text: '（月兔）嘻嘻 哇 快看那边' },
            ]
        ];

        let showDebugTime = false;
        const debugInfo = document.createElement('div');
        debugInfo.style.cssText = 'position:fixed;bottom:10px;left:10px;background:rgba(0,0,0,0.8);color:white;padding:10px;border-radius:5px;font-size:12px;z-index:10000;display:none;';
        document.body.appendChild(debugInfo);

        document.addEventListener('keydown', function(e) {
            if (e.key === 'd' || e.key === 'D') {
                showDebugTime = !showDebugTime;
                debugInfo.style.display = showDebugTime ? 'block' : 'none';
            }
        });

        function loadSong(index) {
            currentSongIndex = index;
            const song = songs[index];
            musicTitle.textContent = song.title;
            audioPlayer.src = song.src;
            currentLyricIndex = -1;
            
            audioPlayer.addEventListener('loadedmetadata', function() {
                playBtn.textContent = '▶';
                isPlaying = false;
                document.getElementById('total-time').textContent = formatTime(audioPlayer.duration);
            }, { once: true });
        }

        function formatTime(seconds) {
            if (isNaN(seconds)) return '0:00';
            const mins = Math.floor(seconds / 60);
            const secs = Math.floor(seconds % 60);
            return mins + ':' + (secs < 10 ? '0' : '') + secs;
        }

        function updateLyrics() {
            if (!audioPlayer.src) return;
            
            const currentTime = audioPlayer.currentTime;
            const currentSongLyrics = songLyrics[currentSongIndex] || songLyrics[0];
            let newIndex = -1;
            
            for (let i = currentSongLyrics.length - 1; i >= 0; i--) {
                if (currentTime >= currentSongLyrics[i].time) {
                    newIndex = i;
                    break;
                }
            }
            
            if (showDebugTime) {
                debugInfo.innerHTML = '当前时间: ' + currentTime.toFixed(1) + '秒<br>当前歌词: ' + (currentSongLyrics[newIndex] ? currentSongLyrics[newIndex].text : '无');
            }
            
            if (newIndex !== currentLyricIndex) {
                currentLyricIndex = newIndex;
                displayLyrics();
            }
        }

        function displayLyrics() {
            lyricsContainer.innerHTML = '';
            const currentSongLyrics = songLyrics[currentSongIndex] || songLyrics[0];
            
            const prevLyric = currentLyricIndex > 0 ? currentSongLyrics[currentLyricIndex - 1] : null;
            const currentLyric = currentLyricIndex >= 0 ? currentSongLyrics[currentLyricIndex] : null;
            const nextLyric = currentLyricIndex < currentSongLyrics.length - 1 ? currentSongLyrics[currentLyricIndex + 1] : null;
            
            if (prevLyric) {
                const prevLine = document.createElement('div');
                prevLine.className = 'lyric-line prev';
                prevLine.textContent = prevLyric.text;
                lyricsContainer.appendChild(prevLine);
            }
            
            if (currentLyric) {
                const currentLine = document.createElement('div');
                currentLine.className = 'lyric-line active';
                currentLine.textContent = currentLyric.text;
                lyricsContainer.appendChild(currentLine);
            }
            
            if (nextLyric) {
                const nextLine = document.createElement('div');
                nextLine.className = 'lyric-line next';
                nextLine.textContent = nextLyric.text;
                lyricsContainer.appendChild(nextLine);
            }
        }
        
        audioPlayer.addEventListener('timeupdate', function() {
            updateLyrics();
            if (audioPlayer.duration) {
                const progress = (audioPlayer.currentTime / audioPlayer.duration) * 100;
                progressSmall.style.width = progress + '%';
                document.getElementById('current-time').textContent = formatTime(audioPlayer.currentTime);
            }
        });

        audioPlayer.addEventListener('ended', function() {
            playNext();
        });

        audioPlayer.addEventListener('error', function() {
            console.log('音频加载失败，请确保 music 文件夹中存在 song1.mp3, song2.mp3, song3.mp3 文件');
        });

        playBtn.addEventListener('click', function() {
            if (!audioPlayer.src) {
                loadSong(0);
            }
            
            if (isPlaying) {
                audioPlayer.pause();
                playBtn.textContent = '▶';
                isPlaying = false;
            } else {
                audioPlayer.play();
                playBtn.textContent = '❚❚';
                isPlaying = true;
            }
        });

        function playNext() {
            currentSongIndex = (currentSongIndex + 1) % songs.length;
            loadSong(currentSongIndex);
            setTimeout(function() {
                audioPlayer.play();
                playBtn.textContent = '❚❚';
                isPlaying = true;
            }, 100);
        }

        function playPrev() {
            currentSongIndex = (currentSongIndex - 1 + songs.length) % songs.length;
            loadSong(currentSongIndex);
            setTimeout(function() {
                audioPlayer.play();
                playBtn.textContent = '❚❚';
                isPlaying = true;
            }, 100);
        }

        prevBtn.addEventListener('click', function() {
            playPrev();
        });

        nextBtn.addEventListener('click', function() {
            playNext();
        });

        const canvas = document.getElementById('petal-canvas');
        const ctx = canvas.getContext('2d');
        
        function resizeCanvas() {
            canvas.width = window.innerWidth;
            canvas.height = window.innerHeight;
        }
        
        resizeCanvas();
        window.addEventListener('resize', resizeCanvas);
        
        let petals = [];
        
        function initPetals() {
            petals = [];
            for (let i = 0; i < 50; i++) {
                petals.push({
                    x: canvas.width + Math.random() * 500,
                    y: Math.random() * canvas.height,
                    size: Math.random() * 15 + 8,
                    speedX: -(Math.random() * 1.5 + 0.5),
                    speedY: Math.random() * 0.5 + 0.2,
                    rotation: Math.random() * Math.PI * 2,
                    rotationSpeed: (Math.random() - 0.5) * 0.05,
                    opacity: Math.random() * 0.5 + 0.5,
                });
            }
        }
        
        function drawPetal(petal) {
            ctx.save();
            ctx.translate(petal.x, petal.y);
            ctx.rotate(petal.rotation);
            ctx.globalAlpha = petal.opacity;
            
            const gradient = ctx.createLinearGradient(0, -petal.size/2, 0, petal.size/2);
            gradient.addColorStop(0, 'rgba(255, 180, 220, 0.9)');
            gradient.addColorStop(0.5, 'rgba(255, 120, 180, 0.8)');
            gradient.addColorStop(1, 'rgba(255, 80, 150, 0.6)');
            
            ctx.fillStyle = gradient;
            ctx.beginPath();
            ctx.ellipse(0, 0, petal.size/2, petal.size, 0, 0, Math.PI * 2);
            ctx.fill();
            
            ctx.restore();
        }
        
        function animate() {
            ctx.clearRect(0, 0, canvas.width, canvas.height);
            
            petals.forEach(function(petal) {
                petal.x += petal.speedX;
                petal.y += petal.speedY + Math.sin(petal.x * 0.01) * 0.5;
                petal.rotation += petal.rotationSpeed;
                
                if (petal.x < -50 || petal.y > canvas.height + 50) {
                    petal.x = canvas.width + Math.random() * 100;
                    petal.y = -50 - Math.random() * 100;
                }
                
                drawPetal(petal);
            });
            
            requestAnimationFrame(animate);
        }
        
        initPetals();
        animate();
    </script>
</body>
</html>()
