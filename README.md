# 🎮 Game Glitch Investigator: The Impossible Guesser

## 🚨 The Situation

You asked an AI to build a simple "Number Guessing Game" using Streamlit.
It wrote the code, ran away, and now the game is unplayable. 

- You can't win.
- The hints lie to you.
- The secret number seems to have commitment issues.

## 🛠️ Setup

1. Install dependencies: `pip install -r requirements.txt`
2. Run the broken app: `python -m streamlit run app.py`

## 🕵️‍♂️ Your Mission

1. **Play the game.** Open the "Developer Debug Info" tab in the app to see the secret number. Try to win.
2. **Find the State Bug.** Why does the secret number change every time you click "Submit"? Ask ChatGPT: *"How do I keep a variable from resetting in Streamlit when I click a button?"*
3. **Fix the Logic.** The hints ("Higher/Lower") are wrong. Fix them.
4. **Refactor & Test.** - Move the logic into `logic_utils.py`.
   - Run `pytest` in your terminal.
   - Keep fixing until all tests pass!

## 📝 Document Your Experience

- [x] **Game purpose:** The game asks the player to guess a randomly generated secret number within a limited number of attempts. It provides Higher/Lower hints after each guess.

- [x] **Bugs found:** I found three reproducible bugs: the Higher/Lower hints were reversed, New Game did not completely clear the previous game state, and the displayed Attempts/History information updated one interaction late.

- [x] **Fixes applied:** I corrected the reversed Higher/Lower messages and fixed New Game so it resets the attempts, history, input, score, status, and secret number. I documented the delayed display bug but did not fix it as part of the required project.

## 📸 Demo Walkthrough


1. Start the Streamlit app and select a difficulty level. The sidebar displays the number range and allowed attempts.
2. Enter a number and click **Submit Guess**.
3. The game compares the guess with the secret number and displays the appropriate **Go HIGHER!** or **Go LOWER!** hint.
4. Continue guessing until the secret number is found or the allowed attempts are exhausted.
5. Click **New Game** to generate a new secret number and reset the attempts, history, input, score, and game status.

**Screenshot** *(optional)*: <!-- Insert a screenshot of your fixed, winning game here -->

## 🧪 Test Results

```
python -m pytest
========================= 3 passed in 0.04s =========================
```

## 🚀 Stretch Features

- [ ] [If you choose to complete Challenge 4, describe the Enhanced UI changes here — a screenshot is optional]
