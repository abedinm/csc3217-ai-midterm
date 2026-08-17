# CSC 3217 — Final Term Materials

Post-midterm material for AI & Expert System. The midterm covered Lectures 1-6
(intro, agents, uninformed search, informed search, adversarial search).
Everything here is what comes after.

## Confirmed topics (in both the official course outline and the moderator's own lecture list)

1. Local Search — hill climbing, simulated annealing, local beam (AIMA 4.1)
2. Genetic Algorithms — TWO weeks, one of them entirely worked problems (AIMA 4.1.4)
3. Constraint Satisfaction Problems — TWO weeks: backtracking, then MRV /
   forward checking / arc consistency (AIMA 6)
4. Probability, Bayes' theorem, Bayesian Networks (AIMA 13-14)
5. Artificial Neural Networks — perceptron rule, backpropagation (AIMA 18.7)

## Sources disagree on these three — confirm with the teacher

- Hidden Markov Models (AIMA 15) — on the moderator's lecture list only
- Learning from Examples / supervised learning / linear models (AIMA 18) — same
- Expert Systems — on the semester outline only, in the last teaching week

## Folders

- `lectures-2025-26/` — Spring 2025-26 decks (most recent): local search, GA,
  probabilistic reasoning, CSP (3 files)
- `lectures/` — earlier-semester decks: local search + GA, GA, CSP (49 slides,
  includes the Australia arc-consistency trace), statistical reasoning (46 slides)
- `practice/` — worked problem sets: GA example, CSP problems, Bayes' rule,
  Bayesian network + solution, practise problems 1-3
- `notes/` — 73-page complete final-term note compilation (Spring 2025-26),
  and the official AIUB OBE course plan with the Midterm/Final week dividers
- `lab-code/` — final-term lab Python: GA 8-queens (including a real final
  question file and the instructor's own starter), backtracking, Naive Bayes,
  neural network

## Worth knowing

The lab is 30 of the 100 final-term marks. `GA_8 QueenFinalQuestion.txt` is a
real final-term lab question — the fitness, selection and crossover functions
are given and you implement `mutation()`. Practise that.

Exam problems the department actually reuses:
- GA: maximise f(x) = x^2/2 - 3x for x in [0,31], 5-bit binary encoding
- GA: 8-queens, fitness = non-attacking pairs, max 28 = n(n-1)/2
- CSP: Australia map colouring with arc consistency (SA's domain empties)
- Bayes: meningitis/stiff-neck; two bags of balls; flu vs measles with rash
  probabilities 0.08 / 0.95; three applicants in ratio 1:2:4

Final term is 60% of the course grade (midterm was 40%).

## Provenance

Lecture decks and practice files come from student-uploaded GitHub mirrors of
AIUB course material, not from AIUB directly. Content is consistent across
independent sources but is not officially published. Verify against your own
section's outline on VUES.
