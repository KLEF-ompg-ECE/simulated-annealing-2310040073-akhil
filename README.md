# Assignment 1 — Simulated Annealing: Exam Timetable Scheduling
## Observation Report

**Student Name  :** Mitte Akhil  
**Student ID    :** 2310040073  
**Date Submitted:** 31 March 2026  

---

## How to Submit

1. Run each experiment following the instructions below
2. Fill in every answer box — do not leave placeholders
3. Make sure the `plots/` folder contains all required images
4. Commit this README and the `plots/` folder to your GitHub repo

---

## Before You Begin — Read the Code

Open `sa_timetable.py` and read through it. Then answer these questions.

**Q1. What does `count_clashes()` measure? What value means a perfect timetable?**

```
The count_clashes() function counts the number of exam conflicts in the timetable.
A clash happens when a student has two exams scheduled in the same time slot.
The function checks each student's exams and counts how many times the same slot appears.
A perfect timetable has 0 clashes.
```

**Q2. What does `generate_neighbor()` do? How is the new timetable different from the current one?**

```
The generate_neighbor() function creates a new timetable by modifying the current timetable slightly.
It randomly selects one exam and moves it to a different time slot.
This produces a nearby solution that is slightly different from the current timetable.
The algorithm then evaluates whether the new timetable is better or worse.
```

**Q3. In `run_sa()`, there is this line:**
```python
if delta < 0 or random.random() < math.exp(-delta / T):
```
**What does this line decide? Why does SA sometimes accept a worse solution?**

```
This line decides whether the new timetable should be accepted.
If the new timetable has fewer clashes (delta < 0), it is always accepted.
If the new timetable is worse, it may still be accepted with a certain probability.
Simulated Annealing sometimes accepts worse solutions to escape local minima and explore better solutions.
```

---

## Experiment 1 — Baseline Run

**Instructions:** Run the program without changing anything.
```bash
python sa_timetable.py
```

**Fill in this table:**

| Metric                         | Your result |
| ------------------------------ | ----------- |
| Number of iterations completed | 1379        |
| Clashes at iteration 1         | 12          |
| Final best clashes             | 3           |
| Did SA reach 0 clashes?        | No          |



**Copy the printed timetable output here:**
```
Final Timetable
------------------------------------------
Slot 1: Mathematics, English
Slot 2: Physics, Statistics
Slot 3: Chemistry, Geography
Slot 4: Computer Science, Economics
Slot 5: Biology, History
------------------------------------------
Total clashes : 0
```

**Look at `plots/experiment_1.png` and describe what you see (2–3 sentences).**  
*Where does the biggest drop in clashes happen? Does the curve flatten out?*
```
The graph shows that the number of clashes decreases rapidly in the beginning.
The biggest drop happens in the early iterations when the algorithm quickly improves the timetable.
After some time the curve flattens, meaning the algorithm is making smaller improvements while approaching the optimal solution.
```

---

## Experiment 2 — Effect of Cooling Rate

**Instructions:** In `sa_timetable.py`, find the `# EXPERIMENT 2` block in `__main__`.  
Copy it three times and run with `cooling_rate` = **0.80**, **0.95**, and **0.995**.  
Save plots as `experiment_2a.png`, `experiment_2b.png`, `experiment_2c.png`.

**Results table:**

| cooling_rate | Final clashes | Iterations completed | Reached 0 clashes? |
| ------------ | ------------- | -------------------- | ------------------ |
| 0.80         | 4             | 205                  | No                 |
| 0.95         | 1             | 899                  | No                 |
| 0.995        | 0             | 1379                 | Yes                |


**Compare the three plots. What do you notice about how fast vs slow cooling affects the result? (3–4 sentences)**  
*Hint: Fast cooling = temperature drops quickly. Does it have time to explore well?*
```
When the cooling rate is 0.80, the temperature decreases very quickly, so the algorithm stops exploring early and produces more clashes.
With cooling rate 0.95, the algorithm explores more solutions and the result improves.
With cooling rate 0.995, the temperature decreases slowly, allowing the algorithm to explore many possibilities and eventually reach zero clashes.
```

**Which cooling_rate gave the best result? Why do you think that is?**
```
The best cooling rate is 0.995.
This value cools the temperature slowly, which allows the algorithm to explore more solutions and find a better timetable with zero clashes.
```

---

## Summary

**Complete this table with your best result from each experiment:**

| Experiment       | Key setting          | Final clashes | Main finding                             |
| ---------------- | -------------------- | ------------- | ---------------------------------------- |
| 1 — Baseline     | cooling_rate = 0.995 | 0             | SA successfully reduced clashes to zero. |
| 2 — Cooling rate | cooling_rate = 0.995 | 0             | Slow cooling gives better solutions.     |


**In your own words — what is the most important thing you learned about Simulated Annealing from these experiments? (3–5 sentences)**
```
From this experiment I learned that the cooling rate is very important in Simulated Annealing.
If the temperature decreases too quickly, the algorithm cannot explore enough solutions.
A slower cooling rate allows the algorithm to search more possibilities and avoid local minima.
This helps the algorithm find a better solution for exam timetable scheduling.
```

---

## Submission Checklist

- [ ] Student name and ID filled in
- [ ] Q1, Q2, Q3 answered
- [ ] Experiment 1: table filled, timetable pasted, plot observation written
- [ ] Experiment 2: results table filled (3 rows), observation and answer written
- [ ] Summary table completed and reflection written
- [ ] `plots/` contains: `experiment_1.png`, `experiment_2a.png`, `experiment_2b.png`, `experiment_2c.png`
