<!DOCTYPE html>
<html lang="ja">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no, viewport-fit=cover">
    <title>Spider Climb - 蜘蛛の糸登り</title>
    <style>
        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            user-select: none;
            -webkit-user-select: none;
            touch-action: none; /* スマホのスクロール・ピンチイン防止 */
        }
        html, body {
            width: 100%;
            height: 100dvh; /* スマホのアドレスバー対策 */
            overflow: hidden;
            background-color: #050510;
            font-family: monospace, sans-serif;
            position: fixed; /* バナーや画面の揺れを固定 */
            left: 0;
            top: 0;
        }
        #gameCanvas {
            display: block;
            width: 100vw;
            height: 100dvh;
        }
    </style>
</head>
<body>

<canvas id="gameCanvas"></canvas>

<script>
const canvas = document.getElementById('gameCanvas');
const ctx = canvas.getContext('2d');

function resizeCanvas() {
    canvas.width = window.innerWidth;
    canvas.height = window.innerHeight;
}
window.addEventListener('resize', resizeCanvas);
resizeCanvas();

// --- ふわふわ感の物理定数 ---
const GRAVITY = 0.10;         // 重力を小さくしてふわっと浮遊感
const AIR_RESISTANCE = 0.991;  // 空気抵抗をやや強くして滑らかに
const ARROW_SPEED = 0.045;     // 矢印回転速度
const ROPE_SPEED = 22;        // 糸の発射速度
const ROPE_PULL_SPEED = 4.5;  // 糸を巻き取る速度（ふわっと引く）
const MIN_ROPE_LENGTH = 120;  // 巻き取り後の糸の長さ

let gameState = 'START';
let cameraY = 0;
let maxAltitude = 0;
let stars = [];

let player = {
    x: 0,
    y: 0,
    vx: 0,
    vy: 0,
    radius: 12,
    angle: 0,
    ropeState: 'IDLE', // 'IDLE', 'SHOOTING', 'ATTACHED'
    ropeX: 0,
    ropeY: 0,
    ropeVx: 0,
    ropeVy: 0,
    currentRopeLen: 0,
    targetFirefly: null
};

let fireflies = [];

function initStars() {
    stars = [];
    for (let i = 0; i < 150; i++) {
        stars.push({
            x: Math.random() * canvas.width,
            y: Math.random() * -10000,
            size: Math.random() * 2 + 1,
            alpha: Math.random()
        });
    }
}

function initGame() {
    player.x = canvas.width / 2;
    player.y = canvas.height - 100;
    player.vx = 0;
    player.vy = 0;
    player.angle = -Math.PI / 2;
    player.ropeState = 'IDLE';
    player.targetFirefly = null;

    cameraY = 0;
    maxAltitude = 0;

    fireflies = [];
    // スタート真上の巨大ホタル（直径約3倍 = 半径60〜75前後）
    fireflies.push({ x: canvas.width / 2, y: canvas.height - 280, radius: 65, pulse: 0 });
    
    generateFireflies(-5000);
    initStars();
    gameState = 'PLAYING';
}

// 左右に広く散らばる超大型ホタルを生成
function generateFireflies(upToY) {
    let startY = fireflies.length > 0 ? fireflies[fireflies.length - 1].y - 180 : canvas.height - 480;
    while (startY > upToY) {
        // 画面の左右ギリギリまで広く配置
        const minX = 70;
        const maxX = canvas.width - 70;
        const x = minX + Math.random() * (maxX - minX);
        
        fireflies.push({
            x: x,
            y: startY,
            radius: 55 + Math.random() * 25, // 直径110px〜160pxの超巨大サイズ
            pulse: Math.random() * Math.PI * 2
        });
        startY -= 140 + Math.random() * 110;
    }
}

function handleTap() {
    if (gameState === 'START' || gameState === 'GAMEOVER') {
        initGame();
        return;
    }

    if (player.ropeState === 'IDLE') {
        player.ropeState = 'SHOOTING';
        player.ropeX = player.x;
        player.ropeY = player.y;
        player.ropeVx = Math.cos(player.angle) * ROPE_SPEED;
        player.ropeVy = Math.sin(player.angle) * ROPE_SPEED;
    } else if (player.ropeState === 'ATTACHED' || player.ropeState === 'SHOOTING') {
        // 糸を切断してふわっと飛び出す
        player.ropeState = 'IDLE';
        player.targetFirefly = null;
    }
}

// タップ・クリックイベント（ダブルタップズーム防止）
window.addEventListener('pointerdown', (e) => {
    e.preventDefault();
    handleTap();
}, { passive: false });

function update() {
    if (gameState !== 'PLAYING') return;

    if (player.ropeState === 'IDLE') {
        player.angle += ARROW_SPEED;
    }

    // 糸の発射
    if (player.ropeState === 'SHOOTING') {
        player.ropeX += player.ropeVx;
        player.ropeY += player.ropeVy;

        const distFromPlayer = Math.hypot(player.ropeX - player.x, player.ropeY - player.y);
        if (distFromPlayer > 800) {
            player.ropeState = 'IDLE';
        }

        // ホタルとの当たり判定（大型化に伴い判定拡大）
        for (let ff of fireflies) {
            const d = Math.hypot(player.ropeX - ff.x, player.ropeY - ff.y);
            if (d < ff.radius + 15) {
                player.ropeState = 'ATTACHED';
                player.targetFirefly = ff;
                player.ropeX = ff.x;
                player.ropeY = ff.y;
                player.currentRopeLen = Math.hypot(player.x - ff.x, player.y - ff.y);
                break;
            }
        }
    }

    // 重力加算（ふわっとした落下）
    player.vy += GRAVITY;

    if (player.ropeState === 'ATTACHED' && player.targetFirefly) {
        const ff = player.targetFirefly;

        // ふわっと滑らかに巻き取る
        if (player.currentRopeLen > MIN_ROPE_LENGTH) {
            player.currentRopeLen = Math.max(MIN_ROPE_LENGTH, player.currentRopeLen - ROPE_PULL_SPEED);
        }

        let nextX = player.x + player.vx;
        let nextY = player.y + player.vy;

        let dx = nextX - ff.x;
        let dy = nextY - ff.y;
        let dist = Math.hypot(dx, dy);

        // 張力処理（たわみを意識した慣性物理）
        if (dist > player.currentRopeLen) {
            let nx = dx / dist;
            let ny = dy / dist;

            player.x = ff.x + nx * player.currentRopeLen;
            player.y = ff.y + ny * player.currentRopeLen;

            let dot = player.vx * nx + player.vy * ny;
            if (dot > 0) {
                player.vx -= dot * nx;
                player.vy -= dot * ny;
            }
        } else {
            player.x = nextX;
            player.y = nextY;
        }

        player.vx *= AIR_RESISTANCE;
        player.vy *= AIR_RESISTANCE;

    } else {
        // 通常の浮遊・落下移動
        player.x += player.vx;
        player.y += player.vy;
        player.vx *= AIR_RESISTANCE;
    }

    // 壁バウンド
    if (player.x - player.radius < 0) {
        player.x = player.radius;
        player.vx *= -0.7;
    } else if (player.x + player.radius > canvas.width) {
        player.x = canvas.width - player.radius;
        player.vx *= -0.7;
    }

    // 地面
    const groundY = canvas.height - 30;
    if (player.y + player.radius > groundY) {
        player.y = groundY - player.radius;
        player.vy = 0;
        player.vx *= 0.85;
    }

    // スムーズなカメラ追従
    const targetCameraY = player.y - canvas.height * 0.6;
    if (targetCameraY < cameraY) {
        cameraY += (targetCameraY - cameraY) * 0.08;
    }

    // 高度計算
    const currentAltitude = Math.floor((canvas.height - 30 - player.y) / 10);
    if (currentAltitude > maxAltitude) {
        maxAltitude = currentAltitude;
    }

    // 先行生成
    if (player.y - 1200 < fireflies[fireflies.length - 1].y) {
        generateFireflies(player.y - 2200);
    }

    // 落下ゲームオーバー
    if (player.y - cameraY > canvas.height + 150) {
        gameState = 'GAMEOVER';
    }

    fireflies.forEach(ff => ff.pulse += 0.03);
}

function drawSpider(x, y, radius) {
    ctx.save();
    ctx.translate(x, y);

    ctx.fillStyle = '#111';
    ctx.beginPath();
    ctx.arc(0, 4, radius * 0.7, 0, Math.PI * 2);
    ctx.fill();

    ctx.beginPath();
    ctx.arc(0, -4, radius * 0.5, 0, Math.PI * 2);
    ctx.fill();

    ctx.fillStyle = '#e74c3c';
    ctx.fillRect(-2, 2, 4, 4);

    ctx.strokeStyle = '#222';
    ctx.lineWidth = 2.5;
    const legSpreads = [-0.8, -0.3, 0.3, 0.8];
    legSpreads.forEach(angle => {
        ctx.beginPath();
        ctx.moveTo(-3, -2);
        ctx.lineTo(-12, -2 + angle * 10);
        ctx.lineTo(-16, 4 + angle * 12);
        ctx.stroke();

        ctx.beginPath();
        ctx.moveTo(3, -2);
        ctx.lineTo(12, -2 + angle * 10);
        ctx.lineTo(16, 4 + angle * 12);
        ctx.stroke();
    });

    ctx.fillStyle = '#fff';
    ctx.fillRect(-3, -6, 2, 2);
    ctx.fillRect(1, -6, 2, 2);

    ctx.restore();
}

function draw() {
    let altRatio = Math.min(1, maxAltitude / 1000);
    let grad = ctx.createLinearGradient(0, 0, 0, canvas.height);
    
    let topColor = `rgb(${Math.floor(5 * (1 - altRatio))}, ${Math.floor(5 * (1 - altRatio))}, ${Math.floor(16 * (1 - altRatio))})`;
    let bottomColor = `rgb(${Math.floor(40 * (1 - altRatio))}, ${Math.floor(15 * (1 - altRatio))}, ${Math.floor(50 * (1 - altRatio))})`;
    
    grad.addColorStop(0, topColor);
    grad.addColorStop(1, bottomColor);
    ctx.fillStyle = grad;
    ctx.fillRect(0, 0, canvas.width, canvas.height);

    ctx.save();
    ctx.translate(0, -cameraY);

    // 星
    stars.forEach(star => {
        ctx.fillStyle = `rgba(255, 255, 255, ${0.3 + Math.sin(Date.now() * 0.003 + star.alpha) * 0.3})`;
        ctx.fillRect(star.x, star.y, star.size, star.size);
    });

    // 地面
    const groundY = canvas.height - 30;
    ctx.fillStyle = '#1e272e';
    ctx.fillRect(0, groundY, canvas.width, 500);
    ctx.fillStyle = '#2ed573';
    ctx.fillRect(0, groundY, canvas.width, 6);

    // 超大型ホタルの描画
    fireflies.forEach(ff => {
        const glow = Math.sin(ff.pulse) * 8;
        let radialGrad = ctx.createRadialGradient(ff.x, ff.y, 10, ff.x, ff.y, ff.radius + 30 + glow);
        radialGrad.addColorStop(0, 'rgba(241, 196, 15, 0.95)');
        radialGrad.addColorStop(0.4, 'rgba(241, 196, 15, 0.35)');
        radialGrad.addColorStop(1, 'rgba(241, 196, 15, 0)');
        
        ctx.fillStyle = radialGrad;
        ctx.beginPath();
        ctx.arc(ff.x, ff.y, ff.radius + 30 + glow, 0, Math.PI * 2);
        ctx.fill();

        // 核心
        ctx.fillStyle = '#ffffff';
        ctx.beginPath();
        ctx.arc(ff.x, ff.y, ff.radius * 0.5, 0, Math.PI * 2);
        ctx.fill();
    });

    // 蜘蛛の糸
    if (player.ropeState === 'SHOOTING') {
        ctx.strokeStyle = 'rgba(255, 255, 255, 0.9)';
        ctx.lineWidth = 2;
        ctx.beginPath();
        ctx.moveTo(player.x, player.y);
        ctx.lineTo(player.ropeX, player.ropeY);
        ctx.stroke();
    } else if (player.ropeState === 'ATTACHED' && player.targetFirefly) {
        ctx.strokeStyle = 'rgba(255, 255, 255, 0.85)';
        ctx.lineWidth = 2;
        ctx.beginPath();
        ctx.moveTo(player.x, player.y);
        
        let dist = Math.hypot(player.x - player.targetFirefly.x, player.y - player.targetFirefly.y);
        if (dist < player.currentRopeLen - 10) {
            let midX = (player.x + player.targetFirefly.x) / 2;
            let midY = (player.y + player.targetFirefly.y) / 2 + (player.currentRopeLen - dist) * 0.35;
            ctx.quadraticCurveTo(midX, midY, player.targetFirefly.x, player.targetFirefly.y);
        } else {
            ctx.lineTo(player.targetFirefly.x, player.targetFirefly.y);
        }
        ctx.stroke();
    }

    // クモ
    drawSpider(player.x, player.y, player.radius);

    // 矢印
    if (player.ropeState === 'IDLE' && gameState === 'PLAYING') {
        const arrowDist = 38;
        const ax = player.x + Math.cos(player.angle) * arrowDist;
        const ay = player.y + Math.sin(player.angle) * arrowDist;

        ctx.save();
        ctx.translate(ax, ay);
        ctx.rotate(player.angle);

        ctx.fillStyle = '#ff4757';
        ctx.beginPath();
        ctx.moveTo(11, 0);
        ctx.lineTo(-6, -7);
        ctx.lineTo(-2, 0);
        ctx.lineTo(-6, 7);
        ctx.closePath();
        ctx.fill();

        ctx.restore();
    }

    ctx.restore();

    // UI
    ctx.fillStyle = '#fff';
    ctx.font = 'bold 22px monospace';
    ctx.textAlign = 'right';
    ctx.fillText(`高度: ${maxAltitude} m`, canvas.width - 20, 40);

    if (gameState === 'START') {
        ctx.fillStyle = 'rgba(0, 0, 0, 0.6)';
        ctx.fillRect(0, 0, canvas.width, canvas.height);

        ctx.fillStyle = '#fff';
        ctx.textAlign = 'center';
        ctx.font = 'bold 28px sans-serif';
        ctx.fillText('ドット絵グモの夜空登り', canvas.width / 2, canvas.height / 2 - 40);
        ctx.font = '16px sans-serif';
        ctx.fillText('タップしてスタート', canvas.width / 2, canvas.height / 2 + 20);
    } else if (gameState === 'GAMEOVER') {
        ctx.fillStyle = 'rgba(0, 0, 0, 0.7)';
        ctx.fillRect(0, 0, canvas.width, canvas.height);

        ctx.fillStyle = '#ff4757';
        ctx.textAlign = 'center';
        ctx.font = 'bold 32px sans-serif';
        ctx.fillText('GAME OVER', canvas.width / 2, canvas.height / 2 - 50);

        ctx.fillStyle = '#fff';
        ctx.font = '20px sans-serif';
        ctx.fillText(`最高到達度: ${maxAltitude} m`, canvas.width / 2, canvas.height / 2);
        
        ctx.font = '16px sans-serif';
        ctx.fillText('タップしてリトライ', canvas.width / 2, canvas.height / 2 + 60);
    }
}

function gameLoop() {
    update();
    draw();
    requestAnimationFrame(gameLoop);
}

gameLoop();
</script>
</body>
</html>
