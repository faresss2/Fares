<!DOCTYPE html><html lang="ar" dir="rtl">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>عيد مبارك</title>  <link href="https://fonts.googleapis.com/css2?family=Cairo:wght@400;700&display=swap" rel="stylesheet">  <style>
    body {
      margin: 0;
      height: 100vh;
      display: flex;
      justify-content: center;
      align-items: center;
      background: linear-gradient(to bottom, #0d47a1, #1976d2);
      color: white;
      font-family: 'Cairo', sans-serif;
      overflow: hidden;
    }

    .content {
      text-align: center;
      z-index: 2;
    }

    h1 {
      font-size: 2.8em;
      animation: glow 2s infinite alternate;
    }

    input {
      padding: 10px;
      border-radius: 20px;
      border: none;
      text-align: center;
      margin-top: 15px;
      font-family: 'Cairo';
    }

    button {
      margin-top: 10px;
      padding: 8px 15px;
      border: none;
      border-radius: 20px;
      background: white;
      color: #1976d2;
      cursor: pointer;
      font-family: 'Cairo';
    }

    .name {
      position: absolute;
      bottom: 10px;
      font-size: 0.9em;
      opacity: 0.8;
    }

    .moon {
      position: absolute;
      top: 60px;
      left: 60px;
      width: 80px;
      height: 80px;
      background: #fff;
      border-radius: 50%;
      box-shadow: -15px 0 0 0 #1976d2;
      animation: floatMoon 4s infinite ease-in-out;
    }

    @keyframes floatMoon {
      50% { transform: translateY(-15px); }
    }

    .star {
      position: absolute;
      width: 3px;
      height: 3px;
      background: white;
      border-radius: 50%;
      animation: twinkle 2s infinite;
    }

    @keyframes twinkle {
      50% { opacity: 1; }
      0%,100% { opacity: 0.2; }
    }

    .mosque {
      position: absolute;
      bottom: 0;
      width: 100%;
      height: 200px;
      background: rgba(255,255,255,0.1);
      clip-path: polygon(0% 100%, 0% 70%, 20% 70%, 25% 50%, 30% 70%, 45% 70%, 50% 40%, 55% 70%, 70% 70%, 75% 50%, 80% 70%, 100% 70%, 100% 100%);
    }

    @keyframes glow {
      from { text-shadow: 0 0 10px #fff; }
      to { text-shadow: 0 0 25px gold; }
    }

    canvas {
      position: absolute;
      inset: 0;
      pointer-events: none;
    }

  </style></head>
<body><canvas id="fireworks"></canvas>

  <div class="moon"></div>  <script>
    // نجوم
    for (let i = 0; i < 80; i++) {
      let s = document.createElement('div');
      s.className = 'star';
      s.style.top = Math.random()*innerHeight+'px';
      s.style.left = Math.random()*innerWidth+'px';
      s.style.animationDelay = Math.random()*2+'s';
      document.body.appendChild(s);
    }
  </script>  <div class="mosque"></div>  <div class="content" id="main">
    <h1 id="title">اكتب اسمك 🎉</h1>
    <input type="text" id="username" placeholder="اسمك هنا">
    <br>
    <button onclick="startEid()">ابدأ</button>
  </div>  <div class="name">فارس بن سعيد</div><audio id="takbeer" src="https://cdn.pixabay.com/audio/2022/03/15/audio_5f5b4f1f4b.mp3"></audio>

  <script>
    const canvas = document.getElementById('fireworks');
    const ctx = canvas.getContext('2d');
    canvas.width = innerWidth;
    canvas.height = innerHeight;

    let particles = [];

    function createFirework(x, y) {
      for (let i = 0; i < 40; i++) {
        particles.push({
          x, y,
          angle: Math.random() * Math.PI * 2,
          speed: Math.random() * 5 + 2,
          life: 60
        });
      }
    }

    function animate() {
      ctx.clearRect(0,0,canvas.width,canvas.height);
      particles.forEach((p,i)=>{
        p.x += Math.cos(p.angle)*p.speed;
        p.y += Math.sin(p.angle)*p.speed;
        p.life--;
        ctx.fillRect(p.x,p.y,2,2);
        if(p.life<=0) particles.splice(i,1);
      });
      requestAnimationFrame(animate);
    }

    animate();

    function startEid() {
      let name = document.getElementById('username').value;
      if(!name) name = '🌙';

      document.getElementById('main').innerHTML = `
        <h1>كل عام وانت بخير يا ${name} 🎉</h1>
        <p>اضغط للاحتفال 🎆</p>
      `;

      document.body.onclick = () => {
        document.getElementById('takbeer').play();
        createFirework(Math.random()*canvas.width, Math.random()*canvas.height/2);
      };
    }
  </script></body>
</html>
