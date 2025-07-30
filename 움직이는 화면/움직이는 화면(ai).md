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



### 1. 기본 HTML + CSS + JavaScript 애니메이션

- HTML: 화면 구조 만들기 (캔버스 또는 div 요소)
- CSS: 간단한 애니메이션 (keyframes, transitions)
- JavaScript: 움직임 제어, 이벤트 처리

        설명
        CSS 애니메이션은 간단한 움직임에 좋음 (예: 버튼 색상 변화, 간단한 위치 이동)
        
        JavaScript로는 더 복잡한 움직임과 제어 가능
        
        예를 들어 setInterval, requestAnimationFrame을 써서 프레임마다 화면을 업데이트 가능


### 2. Canvas API (HTML5 Canvas) 

- HTML <canvas> 태그
- JavaScript Canvas API

        설명
        <canvas>는 픽셀 단위로 그래픽을 그릴 수 있는 공간
        
        도형, 이미지, 텍스트를 그릴 수 있고 직접 픽셀을 조작 가능
        
        애니메이션을 하려면 requestAnimationFrame을 써서 매 프레임마다 그림을 다시 그림
        
        게임, 인터랙티브한 그래픽에 많이 쓰임


### 3. 라이브러리 활용하기 (예: p5.js, Three.js)

        p5.js
        
        - 2D 그래픽과 애니메이션을 쉽게 만드는 라이브러리
        - Processing 언어에서 영감을 받아 JS로 만든 것
        - 간단한 코드로 그리기, 움직임 제어 가능

        Three.js
        
        - 3D 그래픽과 애니메이션 라이브러리
        - WebGL을 쉽게 쓸 수 있도록 도와줌
        - 3D 모델, 조명, 카메라 효과 등을 만들 수 있음

### 추천 시작 방법

1단계: 기본 HTML/CSS/JS로 간단한 움직임 만들어 보기

- 버튼 누르면 박스가 움직이거나 색이 변하는 것부터 시작

2단계: Canvas API 사용해서 간단한 그림 그리기 + 움직이기

- 원이나 사각형이 움직이게 만들어 보기
- requestAnimationFrame 공부하기

3단계: p5.js 써보기

- p5.js 공식 사이트에서 튜토리얼 참고
- 예제 보고 따라해보기

### 참고 영상 및 자료

기본 애니메이션

- CSS 애니메이션 기초 강좌 - 생활코딩
- JavaScript 애니메이션 기초 - 생활코딩

Canvas API

- Canvas Tutorial for Beginners (by Traversy Media)
- MDN Canvas API 문서

p5.js

- p5.js Crash Course by The Net Ninja
- p5.js 공식 튜토리얼

