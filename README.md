<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Our Universe </title>
  <style>
    body {
      background-color: #000;
      margin: 0;
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
    }
    canvas {
      border: 1px solid #fff;
      cursor: pointer;
    }
    .modal {
      display: none;
      position: fixed;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
      background-color: rgba(255, 255, 255, 0.9);
      padding: 20px;
      border-radius: 5px;
      text-align: center;
    }
    .close {
      position: absolute;
      top: 10px;
      right: 10px;
      cursor: pointer;
    }
  </style>
</head>
<body>
  <canvas id="starCanvas" width="800" height="600"></canvas>
  <div class="modal" id="starModal">
    <span class="close" onclick="closeModal()">&times;</span>
    <h2 id="starName"></h2>
    <p id="starDescription"></p>
    <p id="starQuote"></p>
  </div>
  <script> const canvas = document.getElementById('starCanvas');
    const ctx = canvas.getContext('2d');
    const stars = [];
    const numSmallStars = 141;
    const numBigStars = 2;
    const totalStars = numSmallStars + numBigStars;
    const quotes = [ 
"My love for you is a fire, warming even the coldest night",
"It's a melody that serenades my heart, filling it with joy",
"Your love is a gentle touch, soothing my soul like a summer breeze",
 "It's a compass, guiding me through life's twists and turns",
  "Your love is a masterpiece, painting my world with vibrant colors",
   "It's the laughter, that brightens my darkest days", 
   " My love for you is a sanctuary, a safe haven in my solitude",
    " It's the strength, that supports me through life's storms", 
    " Your love is the poetry, that dances in my heart",
     " It's the answer to questions,I never knew I had", 
     " My love for you is a promise, a commitment to forever", 
     "It's the map, that charts the course of our journey together", 
     " It's the destination, of all my desires", 
     " Your love is the essence, of my existence", 
     "It's the meaning, of my life, pure and everlasting", 
     "Your love is like a beacon, guiding me home through life's uncertainties",
      "It's the sweetest lullaby, that cradles my soul to sleep", 
"My love for you is a sunrise, bringing warmth and hope to each day", 
"It's the starlight, that shines in my darkest hours", 
"It's the unspoken words, that connect our hearts",
"Your love is the missing piece, that completes the puzzle of my life",
"It's the strength of a mountain, unwavering and constant", 
"My love for you is a journey, filled with adventures and surprises", 
 "It's the laughter, that echoes in the chambers of my heart", 
"Your love is the calm, in the midst of life's chaos", 
"It's the melody, that plays in the background of my thoughts",
 "It's the reason, I believe in the magic of love",
"Your love is the sunrise, after the darkest night",
"It's the canvas, upon which our story is painted",
"It's the dream,I never want to wake up from", 
"My love for you is the strength,that keeps me going, day by day", 
"It's the faith, that everything will be alright", 
"It's the bond, that ties our hearts together", 
"Your love is the light, at the end of my tunnel", 
"It's the inspiration, behind my every endeavor", 
"Your love is a sanctuary, where I find peace", 
"It's the calm, in the midst of life's storms", 
"It's the courage, to face whatever comes our way",
"My love for you is a garden, where our memories bloom", 
"It's the dance of two souls, perfectly in sync",
"Your love is the compass, that guides me through the maze of life", 
"It's the story, I want to tell for the rest of my days", 
"It's the hope, that fills my heart with each sunrise", 
"My love for you is the reason, I believe in forever", 
"It's the trust, that grows stronger with each passing moment",
"It's the treasure, I will cherish for all eternity", 
"Your love is the poetry, that flows from my heart", 
"It's the whispers of affection, in the stillness of the night", 
"It's the promise, I intend to keep, no matter what",
"My love for you is like a rare gem, precious and priceless", 
"It's the laughter, that brings light to our shared moments",
"It's the dream, that has come true in the form of you",
"Your love is the melody, that plays in the background of my life",
"It's the strength, that carries me through the challenges we face",
"It's the home, where my heart finds solace", 
"My love for you is like a symphony, harmonious and beautiful", 
"It's the kindness, that makes my world a better place", 
"It's the compass, that keeps us on the right path", 
"Your love is the sunrise, that marks the beginning of each day",
"It's the star, that guides me when I'm lost", 
"My love for you is the reason, I believe in destiny", 
"It's the comfort, I find in your embrace",
"It's the joy, that fills my heart with each smile you share", 
"Your love is the anchor, that keeps me grounded", 
"It's the light, that dispels the darkness of doubt", 
"It's the serendipity, that brought us together"," My love for you is the promise, that I'll always be by your side", 
"It's the adventure of a lifetime, that we're on together", 
"It's the magic, that makes every day feel like a fairy tale",
"Your love is the tapestry, woven from our shared experiences", 
"It's the laughter, that echoes in our shared moments",
"It's the compass, that points us towards happiness", 
"My love for you is the sunrise, that brightens my world",
" It's the moonlight, that fills our nights with romance", 
"It's the dream, I never want to wake up from", 
"Your love is the strength, that carries us through life's challenges", 
 "It's the promise, that we'll weather every storm together", 
"It's the sanctuary, where our hearts find peace",
"My love for you is the laughter, that fills our days with joy",
"It's the courage, to face the unknown hand in hand",
"It's the hope, that we'll create a beautiful future together",
"Your love is the melody, that plays in the background of our love story",
"It's the bond, that grows stronger with each passing day",
"It's the anchor, that keeps us steady in the sea of life",
"My love for you is the sunrise, that marks the start of every adventure", 
"It's the starlight, that guides us through the night",
"It's the dream, I'm grateful for every day", 
"Your love is the compass, that always points us in the right direction", 
" It's the strength, that helps us overcome any obstacle", 
"It's the home, where my heart truly belongs", 
" My love for you is a masterpiece of emotions, painted with care", 
"It's the laughter, that fills our hearts.",
"It's the sunrise, that greets us with hope each day",
"Your love is the moonlight, that casts a gentle glow on our nights",
"It's the dream, that weaves the tapestry of our shared future",
" My love for you is the foundation, upon which our relationship is built",
"It's the trust, that deepens with every passing moment",
"It's the laughter, that creates music in our hearts",
"Your love is the lighthouse, guiding me through life's storms",
"It's the comfort, I find in your presence",
"It's the joy, that fills our shared adventures",
"My love for you is the warmth, in the coldest of times",
"It's the bond, that ties our souls together",
"It's the melody, that never fades from our love song",
"Your love is the sunrise, that signals a new beginning",
"It's the star, that shines brightly in our shared universe",
"It's the dream, that continues to unfold with you by my side",
"My love for you is the courage, to face life's challenges head-on",
"It's the hope, that blossoms in the garden of our hearts",
"It's the sanctuary, where our souls find peace",
"Your love is the compass, that guides us to each other",
"It's the strength, that carries us through the ebb and flow of life",
"It's the shelter, in the storms of uncertainty",
"My love for you is the canvas, upon which our memories are painted",
"It's the symphony, that plays when our hearts beat as one",
"It's the promise, that binds us in an unbreakable bond",
"Your love is the sunrise, that heralds a new chapter",
"It's the moon, that lights our path on the darkest nights",
"It's the dream, that continues to inspire us",
"My love for you is the melody, in the soundtrack of our lives",
"It's the laughter, that echoes through our shared moments",
"It's the compass, that leads us to our shared destiny",
"It's the anchor, that keeps us grounded in love",
"Your love is the sunrise, that paints the sky with hope",
"It's the stars, that twinkle in your eyes",
"It's the dream, that becomes reality when we're together",
"My love for you is the strength, that carries us through any storm",
"It's the promise, that we'll be there for each other, always",
"It's the sanctuary, where we find solace in each other's arms",
"It's the laughter, that brings light to our days",
"Your love is the courage, to face whatever comes our way",
"It's the hope, that paints a brighter future for us",
"It's the compass, that never loses its way in our love story",
"My love for you is the sunrise, that marks the dawn of our love",
"It's the moonlight, that creates a romantic ambiance",
"It's the dream, that unites our hearts and souls",
"Your love is the melody, that plays in the background of our life",
"It's the bond, that grows stronger with each passing day",
"It's the anchor, that keeps us steady in the face of challenges",
"My love for you is the sunrise, that promises a new beginning",
"It's the starlight, that guides us through the night",
"It's the dream, that I cherish with all my heart",
" Your love is the key, that unlocks the door to my happiness",
];

    const modal = document.getElementById('starModal');
    const starNameElement = document.getElementById('starName');
    const starDescriptionElement = document.getElementById('starDescription');
    const starQuoteElement = document.getElementById('starQuote');
    
    function drawStar(x, y, size, brightness) {
      ctx.beginPath();
      ctx.arc(x, y, size, 0, 2 * Math.PI);
      const gradient = ctx.createRadialGradient(x, y, 0, x, y, size);
      gradient.addColorStop(0, `rgba(255, 255, 255, ${brightness})`);
      gradient.addColorStop(1, 'transparent');
      ctx.fillStyle = gradient;
      ctx.fill();
    }
    
    function getRandomCoordinate(max) {
      return Math.floor(Math.random() * max);
    }
    
    function getRandomQuote() {
      return quotes[Math.floor(Math.random() * quotes.length)];
    }
    
    function findClickedStar(event) {
      const rect = canvas.getBoundingClientRect();
      const mouseX = event.clientX - rect.left;
      const mouseY = event.clientY - rect.top;
    
      for (const star of stars) {
        const distance = Math.sqrt((star.x - mouseX) ** 2 + (star.y - mouseY) ** 2);
        if (distance < star.size) {
          displayStarInfo(star.name, star.description, star.quote);
          break;
        }
      }
    }
    
    function displayStarInfo(name, description, quote) {
      starNameElement.textContent = name;
      starDescriptionElement.textContent = description;
      starQuoteElement.textContent = quote;
      modal.style.display = 'block';
    }
    
    function closeModal() {
      modal.style.display = 'none';
    }
    
    function updateStarsPosition() {
      for (const star of stars) {
        star.x += (Math.random() - 0.5) * 0.5; // Move the star horizontally within a small range
        star.y += (Math.random() - 0.5) * 0.5; // Move the star vertically within a small range
    
        // Ensure stars stay within the canvas boundaries
        if (star.x < 0) star.x = canvas.width;
        if (star.x > canvas.width) star.x = 0;
        if (star.y < 0) star.y = canvas.height;
        if (star.y > canvas.height) star.y = 0;
      }
    }
    
    function getStarOrdinalNumber(number) {
  const lastDigit = number % 10;
  const lastTwoDigits = number % 100;

  if (lastTwoDigits >= 11 && lastTwoDigits <= 13) {
    return `${number}th`;
  } else if (lastDigit === 1) {
    return `${number}st`;
  } else if (lastDigit === 2) {
    return `${number}nd`;
  } else if (lastDigit === 3) {
    return `${number}rd`;
  } else {
    return `${number}th`;
  }
}

function drawStars() {
  ctx.clearRect(0, 0, canvas.width, canvas.height);

  // Draw big stars
  for (let i = 0; i < numBigStars; i++) {
    const x = getRandomCoordinate(canvas.width);
    const y = getRandomCoordinate(canvas.height);
    const size = 10;
    stars.push({ x, y, size, name: `Star ${i + 1}/${totalStars}`, brightness: 1, description: `In Patrick Universe Gallery: The ${getStarOrdinalNumber(i + 1)} Star among ${totalStars}.`, quote: getRandomQuote() });
    drawStar(x, y, size, 1);
  }

  // Draw small stars
  for (let i = 0; i < numSmallStars; i++) {
    const x = getRandomCoordinate(canvas.width);
    const y = getRandomCoordinate(canvas.height);
    const size = Math.random() * 2 + 1; // Random size between 1 and 3
    stars.push({ x, y, size, name: `Star ${getStarOrdinalNumber(numBigStars + i + 1)}/${totalStars}`, brightness: 1, description: `In Patrick universe Gallery: The ${getStarOrdinalNumber(numBigStars + i + 1)} Star among ${totalStars}.`, quote: getRandomQuote() });
    drawStar(x, y, size, 1);
  }
}
    
    function animate() {
      updateStarsPosition();
      ctx.clearRect(0, 0, canvas.width, canvas.height);
      for (const star of stars) {
        drawStar(star.x, star.y, star.size, star.brightness);
      }
      requestAnimationFrame(animate);
    }
    
    drawStars();
    canvas.addEventListener('click', findClickedStar);
    animate();
    </script>
</body>
</html>
