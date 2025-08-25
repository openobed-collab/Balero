<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Balero — Super Flexible String</title>
  <style>
    html, body {
      margin: 0;
      padding: 0;
      height: 100%;
      background: #0f172a;
      color: #e2e8f0;
      font-family: system-ui, sans-serif;
      overflow: hidden;
    }
    #ui {
      position: fixed;
      top: 12px;
      left: 12px;
      background: rgba(2, 6, 23, 0.6);
      border: 1px solid rgba(226,232,240,0.2);
      border-radius: 14px;
      padding: 10px 12px;
      backdrop-filter: blur(6px);
      user-select: none;
    }
    #ui .row { display: flex; gap: 8px; align-items: center; flex-wrap: wrap;}
    #ui .pill {
      padding: 6px 10px;
      background: rgba(30,41,59,0.8);
      border: 1px solid rgba(226,232,240,0.08);
      border-radius: 999px;
      font-size: 14px;
      line-height: 1;
    }
    #ui .score { font-weight: 700; }
    #footer {
      position: fixed;
      bottom: 12px;
      left: 50%;
      transform: translateX(-50%);
      font-size: 14px;
      opacity: 0.8;
      text-align: center;
      user-select: none;
      background: rgba(2, 6, 23, 0.6);
      border: 1px solid rgba(226,232,240,0.15);
      padding: 8px 12px;
      border-radius: 10px;
      backdrop-filter: blur(6px);
    }
    canvas { display: block; }
    .btn {
      padding: 6px 10px;
      background: #111827;
      color: #e5e7eb;
      border: 1px solid rgba(229,231,235,0.15);
      border-radius: 10px;
    }
    .btn:hover { filter: brightness(1.1); }
  </style>
</head>
<body>
  <canvas id="game"></canvas>

  <div id="ui">
    <div class="row" style="gap:12px; margin-bottom:8px;">
      <span class="pill score" id="scorePill">Score: 0</span>
      <span class="pill" id="streakPill">Streak: 0</span>
      <button id="resetBtn" class="btn">Reset</button>
    </div>
  </div>

  <div id="footer">
    Move your mouse — the stick follows you.<br/>
    Swing the ball and land the hole on the tip of the stick to score!
  </div>

  <script>
    (() => {
      const canvas = document.getElementById('game');
      const ctx = canvas.getContext('2d');

      let W = 0, H = 0;
      function size() {
        W = canvas.width = window.innerWidth;
        H = canvas.height = window.innerHeight;
      }
      window.addEventListener('resize', size);
      size();

      // Game state
      let pivot = { x: W * 0.5, y: H * 0.35 };
      let prev = { x: pivot.x, y: pivot.y + 160 };
      let ball = { x: pivot.x, y: pivot.y + 160 };
      let vx = 0, vy = 0;
      let L = 160;
      let G = 1600;
      let D = 0.985;

      const stickLen = 120;
      const ballR = 24;
      const holeR = 10;
      const scoreThreshold = holeR + 6;
      const tipR = 6;

      let score = 0;
      let streak = 0;
      let canScore = true;

      function resetBall() {
        ball.x = pivot.x;
        ball.y = pivot.y + L;
        prev.x = ball.x;
        prev.y = ball.y;
        vx = 0; vy = 0;
        canScore = true;
      }

      function updateScoreLabels() {
        document.getElementById('scorePill').textContent = 'Score: ' + score;
        document.getElementById('streakPill').textContent = 'Streak: ' + streak;
      }

      function setPivot(x, y) {
        pivot.x = x; pivot.y = y;
      }

      window.addEventListener('pointermove', (e) => {
        setPivot(e.clientX, e.clientY);
      }, { passive: true });

      document.getElementById('resetBtn').addEventListener('click', () => {
        score = 0;
        streak = 0;
        updateScoreLabels();
        resetBall();
      });

      let last = performance.now();
      function frame(now) {
        const dt = Math.min(0.033, (now - last) / 1000);
        last = now;
        update(dt);
        draw();
        requestAnimationFrame(frame);
      }
      requestAnimationFrame(frame);

      function update(dt) {
        const x = ball.x, y = ball.y;
        vx = (ball.x - prev.x) / dt;
        vy = (ball.y - prev.y) / dt;

        vy += G * dt;
        vx *= D;
        vy *= D;

        let nx = ball.x + vx * dt;
        let ny = ball.y + vy * dt;

        // --- SUPER FLEXIBLE STRING ---
        let dx = nx - pivot.x;
        let dy = ny - pivot.y;
        let dist = Math.hypot(dx, dy);

        const slack = 120;       // huge slack so ball can come very close to pivot
        const stiffness = 0.05;  // very soft spring

        if (dist > L) {
          const stretch = dist - L;
          nx -= (dx / dist) * stretch * stiffness;
          ny -= (dy / dist) * stretch * stiffness;
        } else if (dist < L - slack) {
          const stretch = (L - slack) - dist;
          nx += (dx / dist) * stretch * stiffness;
          ny += (dy / dist) * stretch * stiffness;
        }

        prev.x = x;
        prev.y = y;
        ball.x = nx;
        ball.y = ny;

        vx = (ball.x - prev.x) / dt;
        vy = (ball.y - prev.y) / dt;

        const pdist = Math.hypot(ball.x - pivot.x, ball.y - pivot.y);
        if (pdist < scoreThreshold) {
          if (canScore) {
            score++;
            streak++;
            canScore = false;
            updateScoreLabels();
            vy -= Math.max(80, 220 - L * 0.5);
          }
        } else {
          canScore = true;
        }
      }

      function draw() {
        ctx.fillStyle = '#0f172a';
        ctx.fillRect(0, 0, W, H);

        ctx.lineWidth = 2;
        ctx.strokeStyle = '#94a3b8';
        ctx.beginPath();
        ctx.moveTo(pivot.x, pivot.y);
        ctx.lineTo(ball.x, ball.y);
        ctx.stroke();

        const stickBottomX = pivot.x;
        const stickBottomY = pivot.y + stickLen;
        ctx.lineWidth = 8;
        ctx.lineCap = 'round';
        ctx.strokeStyle = '#f5deb3';
        ctx.beginPath();
        ctx.moveTo(pivot.x, pivot.y);
        ctx.lineTo(stickBottomX, stickBottomY);
        ctx.stroke();

        ctx.fillStyle = '#d1d5db';
        ctx.beginPath();
        ctx.arc(pivot.x, pivot.y, tipR, 0, Math.PI * 2);
        ctx.fill();

        ctx.fillStyle = '#eab308';
        ctx.beginPath();
        ctx.arc(ball.x, ball.y, ballR, 0, Math.PI * 2);
        ctx.fill();

        ctx.fillStyle = '#0f172a';
        ctx.beginPath();
        ctx.arc(ball.x, ball.y, holeR, 0, Math.PI * 2);
        ctx.fill();
      }

      resetBall();
    })();
  </script>
</body>
</html>
