
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Pixel Quest</title>
<style>
body {
  margin: 0;
  background: #101827;
  color: white;
  font-family: Arial, sans-serif;
  text-align: center;
}
h1 { color: #35d9ff; }
canvas {
  background: linear-gradient(#172e52, #5294bd);
  width: min(900px, 96vw);
  height: auto;
  border: 3px solid #35d9ff;
}
p { color: #d4e6ff; }
</style>
</head>
<body>
<h1>PIXEL QUEST</h1>
<p>Move: A/D or arrows &nbsp; | &nbsp; Jump: W, ↑ or SPACE</p>
<canvas id="game" width="900" height="500"></canvas>
<p id="status">Collect all coins and reach the golden flag!</p>

<script>
const canvas = document.getElementById("game");
const ctx = canvas.getContext("2d");
const status = document.getElementById("status");

const keys = {};
document.addEventListener("keydown", e => {
  keys[e.key.toLowerCase()] = true;
  if ([" ", "ArrowUp", "ArrowLeft", "ArrowRight"].includes(e.key))
    e.preventDefault();
  if (e.key.toLowerCase() === "r") reset();
});
document.addEventListener("keyup", e => keys[e.key.toLowerCase()] = false);

const platforms = [
  {x:0,y:460,w:900,h:40},
  {x:140,y:380,w:150,h:18},
  {x:350,y:310,w:150,h:18},
  {x:560,y:240,w:150,h:18},
  {x:735,y:170,w:120,h:18}
];

let player, coins, score, won;

function reset() {
  player = {x:40,y:400,w:25,h:34,vx:0,vy:0,ground:false};
  coins = [
    {x:210,y:345,got:false},
    {x:420,y:275,got:false},
    {x:630,y:205,got:false},
    {x:790,y:135,got:false}
  ];
  score = 0;
  won = false;
  status.textContent = "Collect all coins and reach the golden flag!";
}
reset();

function overlap(a,b) {
  return a.x < b.x+b.w && a.x+a.w > b.x &&
         a.y < b.y+b.h && a.y+a.h > b.y;
}

function update() {
  if (won) return;

  player.vx = 0;
  if (keys["a"] || keys["arrowleft"]) player.vx = -4;
  if (keys["d"] || keys["arrowright"]) player.vx = 4;

  if ((keys["w"] || keys["arrowup"] || keys[" "]) && player.ground) {
    player.vy = -11;
    player.ground = false;
  }

  player.vy += 0.48;
  player.x += player.vx;
  player.x = Math.max(0, Math.min(900-player.w, player.x));

  const oldBottom = player.y + player.h;
  player.y += player.vy;
  player.ground = false;

  for (const p of platforms) {
    if (player.vy >= 0 && oldBottom <= p.y &&
        player.y + player.h >= p.y &&
        player.x + player.w > p.x && player.x < p.x+p.w) {
      player.y = p.y-player.h;
      player.vy = 0;
      player.ground = true;
    }
  }

  for (const c of coins) {
    if (!c.got && overlap(player,{x:c.x-10,y:c.y-10,w:20,h:20})) {
      c.got = true;
      score++;
      status.textContent = "Coins: " + score + " / " + coins.length;
    }
  }

  if (player.y > 520) reset();

  if (score === coins.length &&
      overlap(player,{x:845,y:105,w:35,h:65})) {
    won = true;
    status.textContent = "YOU WIN! Press R to play again.";
  }
}

function draw() {
  ctx.clearRect(0,0,900,500);

  // Decorative stars
  ctx.fillStyle = "#ffffff";
  for (let i=0;i<45;i++) {
    const x=(i*197+43)%900, y=(i*83+17)%250;
    ctx.fillRect(x,y,2,2);
  }

  // Platforms
  for (const p of platforms) {
    ctx.fillStyle="#203b36";
    ctx.fillRect(p.x,p.y,p.w,p.h);
    ctx.fillStyle="#39d98a";
    ctx.fillRect(p.x,p.y,p.w,5);
  }

  // Coins
  for (const c of coins) {
    if (c.got) continue;
    ctx.fillStyle="#ffd84a";
    ctx.beginPath();
    ctx.arc(c.x,c.y,10,0,Math.PI*2);
    ctx.fill();
    ctx.fillStyle="#fff2a6";
    ctx.fillRect(c.x-2,c.y-6,4,12);
  }

  // Finish flag
  ctx.fillStyle="#e7efff";
  ctx.fillRect(866,105,5,65);
  ctx.fillStyle="#ff4f81";
  ctx.beginPath();
  ctx.moveTo(871,108);
  ctx.lineTo(899,118);
  ctx.lineTo(871,130);
  ctx.closePath();
  ctx.fill();

  // Player
  ctx.fillStyle="#35d9ff";
  ctx.fillRect(player.x,player.y,player.w,player.h);
  ctx.fillStyle="#ffffff";
  ctx.fillRect(player.x+5,player.y+7,5,5);
  ctx.fillRect(player.x+16,player.y+7,5,5);
  ctx.fillStyle="#10243c";
  ctx.fillRect(player.x+7,player.y+9,2,2);
  ctx.fillRect(player.x+18,player.y+9,2,2);

  ctx.fillStyle="#ffffff";
  ctx.font="18px Arial";
  ctx.fillText("COINS: "+score+"/"+coins.length,20,30);

  if (won) {
    ctx.fillStyle="rgba(0,0,0,0.7)";
    ctx.fillRect(0,0,900,500);
    ctx.fillStyle="#ffd84a";
    ctx.font="bold 48px Arial";
    ctx.fillText("LEVEL COMPLETE!",220,230);
    ctx.font="22px Arial";
    ctx.fillText("Press R to play again",330,275);
  }
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
