## 코드
    <!DOCTYPE html>
    <html lang="ko">
    <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1" />
    <title>애니메이션 버튼 3개</title>
    <style>
      body {
        font-family: Arial, sans-serif;
        text-align: center;
        background-color: #111;
        color: white;
        margin: 0;
        padding: 20px;
      }
      button {
        padding: 10px 20px;
        margin: 10px 5px;
        font-size: 16px;
        cursor: pointer;
        border-radius: 5px;
        border: none;
        background-color: #333;
        color: white;
        transition: background-color 0.3s;
      }
      button:hover {
        background-color: #555;
      }
      #canvas-container {
        margin-top: 20px;
        display: flex;
        justify-content: center;
      }
      canvas {
        background-color: #222;
        border-radius: 10px;
      }
    </style>
    </head>
    <body>
    
    <h1>애니메이션 버튼 3개</h1>
    <button id="starBtn">별 애니메이션</button>
    <button id="ballBtn">하늘색 공</button>
    <button id="thirdBtn">버튼3 애니메이션</button>
    
    <div id="canvas-container">
      <canvas id="animCanvas" width="600" height="400"></canvas>
    </div>
    
    <script>
    // 캔버스와 컨텍스트 준비
    const canvas = document.getElementById('animCanvas');
    const ctx = canvas.getContext('2d');
    
    let animationId; // 애니메이션 프레임 ID 저장 (cancelAnimationFrame 위해)
    let currentAnimation = null;
    
    // 1. 별 애니메이션 함수
    function starAnimation() {
      const stars = [];
      const numStars = 100;
    
      // 별 초기 위치와 속도 설정
      for (let i = 0; i < numStars; i++) {
        stars.push({
          x: Math.random() * canvas.width,
          y: Math.random() * canvas.height,
          size: Math.random() * 2 + 1,
          speed: Math.random() * 0.5 + 0.1,
        });
      }
    
      function animate() {
        ctx.clearRect(0, 0, canvas.width, canvas.height);
        ctx.fillStyle = 'white';
    
        stars.forEach(star => {
          // 별 위치를 위쪽으로 이동 (속도 만큼)
          star.y -= star.speed;
          if (star.y < 0) star.y = canvas.height; // 위로 가면 다시 아래로
    
          // 별 그리기 (원 형태)
          ctx.beginPath();
          ctx.arc(star.x, star.y, star.size, 0, Math.PI * 2);
          ctx.fill();
        });
    
        animationId = requestAnimationFrame(animate);
      }
    
      animate();
    }
    
    // 2. 하늘색 공 애니메이션 함수
    function ballAnimation() {
      const balls = [];
      const numBalls = 15;
    
      for (let i = 0; i < numBalls; i++) {
        balls.push({
          x: Math.random() * canvas.width,
          y: Math.random() * canvas.height,
          radius: 20,
          dx: (Math.random() - 0.5) * 2, // x축 속도
          dy: (Math.random() - 0.5) * 2, // y축 속도
          color: 'skyblue',
        });
      }
    
      function animate() {
        ctx.clearRect(0, 0, canvas.width, canvas.height);
    
        balls.forEach(ball => {
          // 공 위치 이동
          ball.x += ball.dx;
          ball.y += ball.dy;
    
          // 벽에 부딪히면 방향 반전
          if (ball.x + ball.radius > canvas.width || ball.x - ball.radius < 0) ball.dx *= -1;
          if (ball.y + ball.radius > canvas.height || ball.y - ball.radius < 0) ball.dy *= -1;
    
          // 공 그리기
          ctx.beginPath();
          ctx.fillStyle = ball.color;
          ctx.shadowColor = 'rgba(135, 206, 250, 0.7)';
          ctx.shadowBlur = 15;
          ctx.arc(ball.x, ball.y, ball.radius, 0, Math.PI * 2);
          ctx.fill();
          ctx.shadowBlur = 0; // 그림자 해제
        });
    
        animationId = requestAnimationFrame(animate);
      }
    
      animate();
    }
    
    // 3. 세 번째 애니메이션 (예: 네모가 왼쪽에서 오른쪽으로 왔다갔다)
    function squareAnimation() {
      let x = 0;
      let dx = 2;
      const size = 50;
    
      function animate() {
        ctx.clearRect(0, 0, canvas.width, canvas.height);
    
        ctx.fillStyle = 'lime';
        ctx.fillRect(x, canvas.height / 2 - size / 2, size, size);
    
        x += dx;
        if (x + size > canvas.width || x < 0) dx *= -1;
    
        animationId = requestAnimationFrame(animate);
      }
    
      animate();
    }
    
    // 버튼 클릭 시 애니메이션 바꾸기 함수
    function changeAnimation(animFunc) {
      if (animationId) {
        cancelAnimationFrame(animationId);
      }
      currentAnimation = animFunc;
      animFunc();
    }
    
    // 버튼 이벤트 연결
    document.getElementById('starBtn').addEventListener('click', () => changeAnimation(starAnimation));
    document.getElementById('ballBtn').addEventListener('click', () => changeAnimation(ballAnimation));
    document.getElementById('thirdBtn').addEventListener('click', () => changeAnimation(squareAnimation));
    
    // 처음에 별 애니메이션 보여주기
    changeAnimation(starAnimation);
    
    </script>
    
    </body>
    </html>


<img width="776" height="621" alt="image" src="https://github.com/user-attachments/assets/a0cc156e-af13-4fe6-a87b-029974fb059c" />

<img width="675" height="610" alt="image" src="https://github.com/user-attachments/assets/c68366c0-4ce3-475d-96f2-c1edccc2e998" />


<img width="731" height="650" alt="image" src="https://github.com/user-attachments/assets/278d3c3f-d184-4fe6-89d2-82e576b6350e" />

