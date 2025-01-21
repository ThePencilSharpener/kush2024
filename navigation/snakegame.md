<title>Snake Game</title>
<style>
  body {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
    margin: 0;
    background-color: #f0f0f0;
  }
  canvas {
    border: 2px solid #000;
  }
</style>
</head>
<body>
  <canvas id="gameCanvas" width="400" height="400"></canvas>
  <script>
    const canvas = document.getElementById('gameCanvas');
    const ctx = canvas.getContext('2d');
    const gridSize = 20;
    const rows = canvas.height / gridSize;
    const cols = canvas.width / gridSize;
    let snake = [{ x: 5, y: 5 }];
    let food = { x: 10, y: 10 };
    let dx = 1;
    let dy = 0;
    let gameInterval;
    const speed = 100;
    function drawSquare(x, y, color) {
      ctx.fillStyle = color;
      ctx.fillRect(x * gridSize, y * gridSize, gridSize, gridSize);
    }
    function drawSnake() {
      snake.forEach(segment => drawSquare(segment.x, segment.y, 'green'));
    }
    function drawFood() {
      drawSquare(food.x, food.y, 'red');
    }
    function moveSnake() {
      const head = { x: snake[0].x + dx, y: snake[0].y + dy };
      // Check for collisions
      if (
        head.x < 0 || head.x >= cols || 
        head.y < 0 || head.y >= rows || 
        snake.some(segment => segment.x === head.x && segment.y === head.y)
      ) {
        clearInterval(gameInterval);
        alert('Game Over!');
        return;
      }
      snake.unshift(head);
      // Check if the snake eats the food
      if (head.x === food.x && head.y === food.y) {
        placeFood();
      } else {
        snake.pop();
      }
    }
    function placeFood() {
      food = {
        x: Math.floor(Math.random() * cols),
        y: Math.floor(Math.random() * rows)
      };
      while (snake.some(segment => segment.x === food.x && segment.y === food.y)) {
        food = {
          x: Math.floor(Math.random() * cols),
          y: Math.floor(Math.random() * rows)
        };
      }
    }
    function update() {
      ctx.clearRect(0, 0, canvas.width, canvas.height);
      drawFood();
      moveSnake();
      drawSnake();
    }
    function changeDirection(event) {
      const { key } = event;
      if (key === 'ArrowUp' && dy === 0) {
        dx = 0;
        dy = -1;
      } else if (key === 'ArrowDown' && dy === 0) {
        dx = 0;
        dy = 1;
      } else if (key === 'ArrowLeft' && dx === 0) {
        dx = -1;
        dy = 0;
      } else if (key === 'ArrowRight' && dx === 0) {
        dx = 1;
        dy = 0;
      }
    }
    document.addEventListener('keydown', changeDirection);
    function startGame() {
      placeFood();
      gameInterval = setInterval(update, speed);
    }
    startGame();
  </script>
</body>
</html>