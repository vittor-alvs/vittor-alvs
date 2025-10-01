@HTML

<!DOCTYPE html>
<html lang="pt-br">
<head>
  <meta charset="UTF-8" />
  <title>🚀 Desvie do Asteroide! (Controle com Mouse)</title>
  <style>
    body {
      margin: 0;
      background-color: black;
      color: white;
      font-family: sans-serif;
      text-align: center;
    }
    canvas {
      background: #111;
      display: block;
      margin: 0 auto;
      border: 2px solid #444;
    }
  </style>
</head>
<body>
  <h1>🚀 Desvie do Asteroide! (Controle com Mouse)</h1>
  <p>Mova o mouse para mover a nave</p>
  <canvas id="gameCanvas" width="400" height="600"></canvas>

  <script>
    const canvas = document.getElementById("gameCanvas");
    const ctx = canvas.getContext("2d");

    const nave = { x: 180, y: 550, width: 40, height: 40 };
    const asteroide = { x: Math.random() * 360, y: -60, size: 40, speed: 3 };
    let gameOver = false;
    let score = 0;

    // Atualiza posição X da nave para acompanhar o mouse dentro do canvas
    canvas.addEventListener("mousemove", (e) => {
      const rect = canvas.getBoundingClientRect();
      let mouseX = e.clientX - rect.left;
      // Limitar para não sair da tela
      if (mouseX < nave.width / 2) mouseX = nave.width / 2;
      if (mouseX > canvas.width - nave.width / 2) mouseX = canvas.width - nave.width / 2;
      nave.x = mouseX - nave.width / 2;
    });

    function desenharNave() {
      ctx.fillStyle = "lime";
      ctx.beginPath();
      ctx.moveTo(nave.x + nave.width / 2, nave.y);
      ctx.lineTo(nave.x, nave.y + nave.height);
      ctx.lineTo(nave.x + nave.width, nave.y + nave.height);
      ctx.closePath();
      ctx.fill();
    }

    function desenharAsteroide() {
      ctx.fillStyle = "red";
      ctx.beginPath();
      ctx.arc(
        asteroide.x + asteroide.size / 2,
        asteroide.y + asteroide.size / 2,
        asteroide.size / 2,
        0,
        Math.PI * 2
      );
      ctx.fill();
    }

    function desenharScore() {
      ctx.fillStyle = "white";
      ctx.font = "16px Arial";
      ctx.fillText("Pontos: " + score, 10, 20);
    }

    function colisao(rect, circle) {
      const distX = Math.abs(circle.x + circle.size / 2 - (rect.x + rect.width / 2));
      const distY = Math.abs(circle.y + circle.size / 2 - (rect.y + rect.height / 2));

      if (distX > (rect.width / 2 + circle.size / 2)) return false;
      if (distY > (rect.height / 2 + circle.size / 2)) return false;

      return true;
    }

    function atualizar() {
      if (gameOver) return;

      ctx.clearRect(0, 0, canvas.width, canvas.height);

      desenharNave();
      desenharAsteroide();
      desenharScore();

      asteroide.y += asteroide.speed;

      if (asteroide.y > canvas.height) {
        asteroide.y = -60;
        asteroide.x = Math.random() * (canvas.width - asteroide.size);
        score++;
        asteroide.speed += 0.3;
      }

      if (colisao(nave, asteroide)) {
        gameOver = true;
        ctx.fillStyle = "white";
        ctx.font = "30px Arial";
        ctx.fillText("💥 Game Over!", 100, 300);
        ctx.fillText("Pontuação: " + score, 120, 350);
      }

      requestAnimationFrame(atualizar);
    }

    atualizar();
  </script>
</body>
</html>

@CSS

.Tudoooo{


    background-color: green;

}

@JAVASCRIPT

function parEImpar(numero){

  if(numero % 2 === 0 ){

    return 'Este número é par'

  } else {

   return 'Este número é impar'

  }

}

console.log(parEImpar(7))
