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

- [ ] Describe the game's purpose.
   Games purpose was to guess the number
- [ ] Detail which bugs you found.
1. hints were opposite, go higher should be go lower and go lower should be go higher
2. History was not updating properly
3. New game not working properly
4. attempts should start at 0 but it was starting at 1.
- [ ] Explain what fixes you applied.
claude code fixed all the bugs

## 📸 Demo

- [ ] [Insert a screenshot of your fixed, winning game here]
   ![Screenshot of winning game](https://github.com/Tejaslalwani24/ai110-module1show-gameglitchinvestigator-starter/blob/main/Screenshot%202026-03-15%20225919.png)
- [ ] Test Cases passed screenshot
![Screenshot of test cases passed](https://github.com/Tejaslalwani24/ai110-module1show-gameglitchinvestigator-starter/blob/main/Screenshot%202026-03-15%20223752.png)  

## 🚀 Stretch Features

- [ ] [If you choose to complete Challenge 4, insert a screenshot of your Enhanced Game UI here]
