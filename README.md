<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Flashcard Maker</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background: #f5f7fb;
      margin: 0;
      padding: 20px;
    }
    h1 {
      text-align: center;
    }
    .container {
      max-width: 800px;
      margin: auto;
    }
    .input-section, .flashcard-section {
      background: white;
      padding: 20px;
      border-radius: 10px;
      box-shadow: 0 4px 10px rgba(0,0,0,0.1);
      margin-bottom: 20px;
    }
    textarea {
      width: 100%;
      min-height: 100px;
      margin-bottom: 10px;
      padding: 10px;
      font-size: 14px;
    }
    button {
      padding: 10px 16px;
      font-size: 14px;
      border: none;
      border-radius: 6px;
      cursor: pointer;
      background: #4f46e5;
      color: white;
    }
    button:hover {
      background: #4338ca;
    }
    .flashcard {
      background: #eef2ff;
      border-radius: 10px;
      padding: 30px;
      text-align: center;
      font-size: 18px;
      cursor: pointer;
      min-height: 120px;
      display: flex;
      align-items: center;
      justify-content: center;
    }
    .controls {
      display: flex;
      justify-content: space-between;
      margin-top: 10px;
    }
  </style>
</head>
<body>
  <div class="container">
    <h1>Flashcard Maker</h1>

    <div class="input-section">
      <h3>Enter Questions & Answers</h3>
      <p>Format: <strong>Question | Answer</strong> (one per line)</p>
      <textarea id="qaInput" placeholder="What is photosynthesis? | The process plants use to make food"></textarea>
      <button onclick="createFlashcards()">Create Flashcards</button>
    </div>

    <div class="flashcard-section" id="flashcardSection" style="display:none;">
      <div class="flashcard" id="flashcard" onclick="flipCard()"></div>
      <div class="controls">
        <button onclick="prevCard()">Previous</button>
        <button onclick="nextCard()">Next</button>
      </div>
    </div>
  </div>

  <script>
    let flashcards = [];
    let currentIndex = 0;
    let showingAnswer = false;

    function createFlashcards() {
      const input = document.getElementById('qaInput').value.trim();
      const lines = input.split('\n');
      flashcards = [];

      for (let line of lines) {
        const parts = line.split('|');
        if (parts.length === 2) {
          flashcards.push({
            question: parts[0].trim(),
            answer: parts[1].trim()
          });
        }
      }

      if (flashcards.length === 0) {
        alert('Please enter at least one valid question and answer.');
        return;
      }

      currentIndex = 0;
      showingAnswer = false;
      document.getElementById('flashcardSection').style.display = 'block';
      showCard();
    }

    function showCard() {
      const card = flashcards[currentIndex];
      document.getElementById('flashcard').textContent = showingAnswer ? card.answer : card.question;
    }

    function flipCard() {
      showingAnswer = !showingAnswer;
      showCard();
    }

    function nextCard() {
      currentIndex = (currentIndex + 1) % flashcards.length;
      showingAnswer = false;
      showCard();
    }

    function prevCard() {
      currentIndex = (currentIndex - 1 + flashcards.length) % flashcards.length;
      showingAnswer = false;
      showCard();
    }
  </script>
</body>
</html>
