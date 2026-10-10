<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <title>Pixel-Quest</title>
  <style>
    body {
      margin: 0;
      background: #181827;
      color: white;
      font-family: Arial, sans-serif;
      text-align: center;
    }
    h1 { color: #33d8ff; }
    canvas {
      background: linear-gradient(#172e52, #51943d);
      width: min(500px, 90vw);
      height: main;
      border: 3px solid #33d8ff;
    }
    p { color: #d8ff6f; }
  </style>
</head>
<body>
  <h1>Pixel-Quest</h1>
  <p>Use &larr; &rarr; or arrows to move | &uarr; or Space to Jump</p>
  <canvas id="game" width="500" height="500"></canvas>
  <p id="status">Collect all coins and reach the golden flag!</p>

  <script>
    const canvas = document.getElementById("game");
    const ctx = canvas.getContext("2d");
    const status = document.getElementById("status");

    const keys = {};
    document.addEventListener("keydown", e => {
      keys[e.key.toLowerCase()] = true;
      if ([" ", "arrowup", "arrowdown", "arrowleft", "arrowright"].includes(e.key.toLowerCase())) {
        e.preventDefault();
      }
      if (e.key.toLowerCase() === "r") reset();
    });
    document.addEventListener("keyup", e => { keys[e.key.toLowerCase()] = false; });

    const platforms = [
      {x: 0, y: 450, w: 500, h: 40},
      {x: 140, y: 360, w: 130, h: 18},
      {x: 350, y: 310, w: 130, h: 18},
      {x: 260, y: 240, w: 120, h: 18},
      {x: 75, y: 170, w: 120, h: 18}
    ];

    let player, coins, score, won;

    function reset() {
      player = {x: 40, y: 400, w: 25, h: 34, vx: 0, vy: 0, ground: false};
      coins = [
        {x: 210, y: 345, got: false},
        {x: 420, y: 275, got: false},
        {x: 300, y: 205, got: false},
        {x: 130, y: 135, got: false}
      ];
      score = 0;
      won = false;
      status.textContent = "Collect all coins and reach the golden flag!";
    }
    reset();

    function overlap(a, b) {
      return a.x < b.x + b.w && a.x + a.w > b.x &&
             a.y < b.y + b.h && a.y + a.h > b.y;
    }

    function update() {
      if (won) return;

      // Horizontal movement
      if (keys["arrowleft"] || keys["a"]) player.vx = -3;
      else if (keys["arrowright"] || keys["d"]) player.vx = 3;
      else player.vx = 0;

      player.x += player.vx;

      // Canvas boundaries (X)
      if (player.x < 0) player.x = 0;
      if (player.x + player.w > canvas.width) player.x = canvas.width - player.w;

      // Gravity and Jumping
      player.vy += 0.4;
      player.y += player.vy;
      player.ground = false;

      // Platform collisions (Y axis)
      for (let p of platforms) {
        if (overlap(player, p)) {
          if (player.vy > 0 && player.y + player.h - player.vy <= p.y) {
            player.y = p.y - player.h;
            player.vy = 0;
            player.ground = true;
          }
        }
      }

      if ((keys["arrowup"] || keys["w"] || keys[" "]) && player.ground) {
        player.vy = -9;
        player.ground = false;
      }

      // Coin collection
      for (let c of coins) {
        if (!c.got && overlap(player, {x: c.x, y: c.y, w: 15, h: 15})) {
          c.got = true;
          score++;
        }
      }

      // Win condition (reaching top area/flag with all coins)
      if (score === coins.length && player.y < 120 && player.x < 150) {
        won = true;
        status.textContent = "You Win! Press 'R' to restart.";
      }
    }

    function draw() {
      ctx.clearRect(0, 0, canvas.width, canvas.height);

      // Draw platforms
      ctx.fillStyle = "#2e5d32";
      for (let p of platforms) {
        ctx.fillRect(p.x, p.y, p.w, p.h);
        ctx.strokeStyle = "#4caf50";
        ctx.strokeRect(p.x, p.y, p.w, p.h);
      }

      // Draw coins
      ctx.fillStyle = "#ffd700";
      for (let c of coins) {
        if (!c.got) {
          ctx.beginPath();
          ctx.arc(c.x + 7.5, c.y + 7.5, 7, 0, Math.PI * 2);
          ctx.fill();
        }
      }

      // Draw goal flag at the top left
      ctx.fillStyle = "#fff";
      ctx.fillRect(50, 100, 4, 70);
      ctx.fillStyle = "#ff4757";
      ctx.beginPath();
      ctx.moveTo(54, 100);
      ctx.lineTo(84, 115);
      ctx.lineTo(54, 130);
      ctx.fill();

      // Draw player
      ctx.fillStyle = "#ff5252";
      ctx.fillRect(player.x, player.y, player.w, player.h);
    }

    function loop() {
      update();
      draw();
      requestAnimationFrame(loop);
    }

    loop();
  </script>
</body>
</html>
