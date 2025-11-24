<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8" />
  <title>Matrix | Carlos Lopez</title>
  <style>
    * {
      box-sizing: border-box;
    }

    body {
      margin: 0;
      background: #000;
      color: #0f0;
      overflow: hidden;
      font-family: "Consolas", "Courier New", monospace;
    }

    #matrix {
      display: block;
      width: 100vw;
      height: 100vh;
      background: #000;
    }

    .center-text {
      position: fixed;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
      text-align: center;
      pointer-events: none;
      text-shadow: 0 0 10px #0f0;
    }

    .center-text h1 {
      margin: 0 0 8px 0;
      font-size: 32px;
    }

    .center-text p {
      margin: 0;
      font-size: 16px;
      opacity: 0.8;
    }
  </style>
</head>
<body>
  <canvas id="matrix"></canvas>

  <div class="center-text">
    <h1>Bienvenido a mi GitHub </h1>
    <p>Ingeniería de Gestión · Minería · Frontend</p>
  </div>

  <script>
    const canvas = document.getElementById("matrix");
    const ctx = canvas.getContext("2d");

    function resize() {
      canvas.width = window.innerWidth;
      canvas.height = window.innerHeight;
    }

    window.addEventListener("resize", resize);
    resize();

    const letters = "01";
    const fontSize = 16;
    let columns = Math.floor(canvas.width / fontSize);
    let drops = Array(columns).fill(1);

    function draw() {
      // Fondo semitransparente para dejar estelas
      ctx.fillStyle = "rgba(0, 0, 0, 0.05)";
      ctx.fillRect(0, 0, canvas.width, canvas.height);

      ctx.fillStyle = "#0f0";
      ctx.font = fontSize + "px monospace";

      for (let i = 0; i < drops.length; i++) {
        const text = letters.charAt(Math.floor(Math.random() * letters.length));
        const x = i * fontSize;
        const y = drops[i] * fontSize;

        ctx.fillText(text, x, y);

        if (y > canvas.height && Math.random() > 0.95) {
          drops[i] = 0;
        }

        drops[i]++;
      }

      requestAnimationFrame(draw);
    }

    draw();
  </script>
</body>
</html>
