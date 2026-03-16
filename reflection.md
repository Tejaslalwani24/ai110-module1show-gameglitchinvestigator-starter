# 💭 Reflection: Game Glitch Investigator

Answer each question in 3 to 5 sentences. Be specific and honest about what actually happened while you worked. This is about your process, not trying to sound perfect.

## 1. What was broken when you started?

- What did the game look like the first time you ran it?
- 
- List at least two concrete bugs you noticed at the start  
  (for example: "the secret number kept changing" or "the hints were backwards").
  1. hints were opposite, go higher should be go lower and go lower should be go higher
  2. History was not updating properly
  3. New game not working properly
  4. attempts should start at 0 but it was starting at 1.

---

## 2. How did you use AI as a teammate?

- Which AI tools did you use on this project (for example: ChatGPT, Gemini, Copilot)?
- Claude code
- Give one example of an AI suggestion that was correct (including what the AI suggested and how you verified the result).
- I suggested the update score method is incorrect i verified it by checking the code
- Give one example of an AI suggestion that was incorrect or misleading (including what the AI suggested and how you verified the result).
- no AI suggestions were misleading in my case

---

## 3. Debugging and testing your fixes

- How did you decide whether a bug was really fixed?
- I checked if the bugs were fixed by running the app on my localhost and seeing if it was really fixed
- Describe at least one test you ran (manual or using pytest)  
  and what it showed you about your code.
  this is the test case:
  def test_too_high_on_even_attempt_deducts_score():
    score = update_score(100, "Too High", attempt_number=2)
    assert score == 95
What it showed:

Before the fix, the original update_score had this logic:


if outcome == "Too High":
    if attempt_number % 2 == 0:
        return current_score + 5   # even attempt → reward a wrong guess!
    return current_score - 5
If you ran this test against the buggy code, it would fail — update_score(100, "Too High", 2) would return 105 instead of 95. A player guessing too high on their 2nd, 4th, or 6th attempt would actually gain points for a wrong answer, making the scoring system incoherent.

The test pinpoints exactly which case breaks: even-numbered attempts with a "Too High" outcome. It's the kind of bug that's hard to spot by just playing the game, because sometimes the score goes up when you're wrong and you might assume it's intentional — the test makes the expected behavior unambiguous.

After the fix (if outcome in ("Too High", "Too Low"): return current_score - 5), the test passes and wrong guesses consistently cost 5 points regardless of attempt number.
  
- Did AI help you design or understand any tests? How?
- AI helped design all the test cases with a simple command on claude code: "generate a pytest case in test/test_game_logic.py that specifically targets the bug you just fixed."

---

## 4. What did you learn about Streamlit and state?

- In your own words, explain why the secret number kept changing in the original app.
- Every time anything happened in the app — a button click, a keystroke, changing the difficulty — Streamlit re-ran the entire app.py script from top to bottom. The original code had:
st.session_state.secret = random.randint(low, high)
without any guard around it, so a fresh random number was generated on every rerun. The secret never stayed the same long enough for a guess to be meaningful.
- How would you explain Streamlit "reruns" and session state to a friend who has never used Streamlit?
- Imagine your app is a piece of paper with instructions. Every time someone clicks a button or types something, Streamlit throws away the paper and rewrites it from scratch. That means any variables you created are gone — Python doesn't "remember" them between clicks.
st.session_state is like a sticky note attached to the page that survives each rewrite. Anything you store there persists across reruns for as long as the browser tab is open. So instead of just writing secret = 42, you write st.session_state.secret = 42 — and next time the script reruns, that value is still there.
- What change did you make that finally gave the game a stable secret number?
- Wrapping the assignment in a "secret" not in st.session_state guard:
if "secret" not in st.session_state:
    st.session_state.secret = random.randint(low, high)

---

## 5. Looking ahead: your developer habits

- What is one habit or strategy from this project that you want to reuse in future labs or projects?
- making test cases
- What is one thing you would do differently next time you work with AI on a coding task?
- I would want it to plot all the bugs for me 
- In one or two sentences, describe how this project changed the way you think about AI generated code.
- This project showed me that while AI-generated code can quickly produce useful solutions and speed up development, it still requires careful review and understanding from the developer. It changed the way I think about AI as a helpful assistant for coding rather than something that can replace a programmer’s judgment.
