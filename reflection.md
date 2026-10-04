# 💭 Reflection: Game Glitch Investigator

## 1. What was broken when you started?

- What did the game look like the first time you ran it?
- List at least two concrete bugs you noticed at the start
  (for example: "the hints were backwards").

When I first ran the game, the interface loaded and allowed me to enter guesses, but I noticed three concrete bugs:

1. **The hints were backwards.** When my guess was higher than the secret number, the game incorrectly told me to go higher instead of lower.
2. **New Game did not fully reset the game.** A new secret number was generated and the attempts reset, but the previous guess remained in the History and input field.
3. **The game information updated one interaction late.** After I submitted a guess, the Higher/Lower feedback appeared immediately, but Attempts, Attempts Left, and History did not update until the next interaction.

**Bug Reproduction Log**

Document at least 3 bugs you found. Add rows as needed.

| Input | Expected Behavior | Actual Behavior | Console Output / Error |
|-------|-------------------|-----------------|------------------------|
| Guess 50 when secret is 31 | Game should say "Go LOWER!" because 50 is greater than 31. | Game says "Go HIGHER!" | No error |
| Click New Game after making a guess | New game should generate a new secret and clear attempts, history, and previous input. | New secret is generated and attempts reset, but the previous guess remains in History and in the input field. | No error |
| Enter a guess and click Submit Guess once | Attempts should increase, attempts left should decrease, and the guess should immediately appear in History. | Feedback appears immediately, but Attempts, Attempts Left, and History remain one interaction behind and update only after another interaction. | No error |

---

## 2. How did you use AI as a teammate?

- Which AI tools did you use on this project (for example: ChatGPT, Gemini, Copilot)?
- Give one example of an AI suggestion that was correct (including what the AI suggested and how you verified the result).
- Give one example of an AI suggestion you did not accept as written (including what the AI suggested, why you rejected or changed it, and how you verified your version). It does not have to be a suggestion that was wrong: over-engineered, out of scope, harder to read, or a poor fit for this codebase all count.

I used ChatGPT and Claude as AI teammates while investigating and fixing the game. One correct AI suggestion was to fix the reversed hint messages in `check_guess()`. When the guess was higher than the secret number, the code said "Go HIGHER!" instead of "Go LOWER!" I made the suggested correction and verified it both manually in the game and with pytest; all three tests passed.

I also tested an AI suggestion for the delayed History/Attempts display. The suggestion was to move the information and debug displays below the Submit Guess processing so they would show the updated session state immediately. Although this fixed the delayed display, it changed the layout of the interface. I also tried a placeholder-based modification, but it caused the debug expander behavior to change. I therefore did not accept these suggestions as written and left this third bug documented rather than adding a larger, out-of-scope change.

---

## 3. Debugging and testing your fixes

- How did you decide whether a bug was really fixed?
- Describe at least one test you ran (manual or using pytest)
  and what it showed you about your code.
- Did AI help you design or understand any tests? How?

I decided a bug was fixed by reproducing the original problem, making a targeted change, and testing the same behavior again. I manually verified that the Higher/Lower hints were correct and that New Game cleared the previous history, input, attempts, and score. I also used pytest to test `check_guess()` with a winning guess, a guess that was too high, and a guess that was too low; all three tests passed. AI helped me understand why the original starter tests failed after refactoring and helped me modify the tests so they checked both the outcome and the corresponding hint message.

---

## 4. What did you learn about Streamlit and state?

- How would you explain Streamlit "reruns" and session state to a friend who has never used Streamlit?

Streamlit reruns the Python script from top to bottom whenever the user interacts with the app, such as by clicking a button. st.session_state preserves values such as the secret number, attempts, score, and history across those reruns. I learned that the order in which the interface is rendered and the session state is updated matters. In this project, the History and Attempts displays were rendered before the submitted guess updated the session state, which is why they appeared one interaction behind.

---

## 5. Looking ahead: your developer habits

- What is one habit or strategy from this project that you want to reuse in future labs or projects?
  - This could be a testing habit, a prompting strategy, or a way you used Git.
- What is one thing you would do differently next time you work with AI on a coding task?
- In one or two sentences, describe how this project changed the way you think about AI generated code.

One habit I want to reuse is reproducing a bug first, making one targeted change, and then testing the same behavior again before deciding that the bug is fixed. I also want to continue using small, meaningful Git commits so that each important change can be tracked separately. Next time I work with AI, I will give it the relevant code and exact observed behavior before asking for a solution, and I will test its suggestions rather than accepting them automatically. This project showed me that AI-generated code and AI suggestions can be useful, but they still need to be understood, tested, and verified by the developer.