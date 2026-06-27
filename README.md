# Memory Game & Mini Games

A collection of simple browser-based games built with pure HTML, CSS, and JavaScript. The project currently includes:

- Memory Game: a responsive and accessible card-matching game
- Whack-a-Mole: a fast-paced arcade-style clicking game

## Games Included

### Memory Game
- File: `memory-game.html`
- Features:
  - 4x4 and 6x6 grid options
  - Smooth card flip animations
  - Timer and moves counter
  - Star rating system
  - Local storage for best scores
  - Keyboard controls for accessibility
  - Responsive design for all devices

### Whack-a-Mole
- File: `whack-a-mole.html`
- Features:
  - Randomly appearing moles
  - Score tracking
  - 30-second countdown timer
  - Best score persistence using local storage
  - Restart button and responsive layout

## How to Play

### Memory Game
1. Open `memory-game.html` in a web browser
2. Click or use keyboard (Tab + Enter/Space) to flip cards
3. Find matching pairs to win
4. Try to complete the game with as few moves as possible
5. Switch between 4x4 and 6x6 grids using the buttons

### Whack-a-Mole
1. Open `whack-a-mole.html` in a web browser
2. Click the Start Game button
3. Whack the mole as it appears in the holes
4. Try to score as many points as possible before time runs out

## Technical Details

- Pure HTML, CSS, and JavaScript implementation
- No external libraries or dependencies
- Fully responsive design using CSS Grid and flexible layouts
- Accessible with ARIA attributes and keyboard controls where applicable
- Local storage for persistent high scores and best game results

## Development

1. Clone the repository
2. Open either HTML file in a web browser
3. Or serve using a local HTTP server:
   ```bash
   python3 -m http.server 8000
   ```
4. Visit `http://localhost:8000/memory-game.html` or `http://localhost:8000/whack-a-mole.html`