# Course lecture summaries — 14.310x

## Week 1 — Lecture 1 — Introduction

- **Instructors:** Esther Duflo, Sara Ellison
- **Slides:** `Week 1/mit14_310x_s23_week01_lec01 (1).pdf`
- **Transcript:** `Week 1/transcript.pdf`
- **Homework:** `Week 1/mit14_310x_s23_homework01.pdf`

**Themes**

- Data are everywhere: World Bank, Census, J-PAL, journals, web/API, surveys.
- Examples: data as **beautiful**, **insightful**, **powerful**, or **misleading**.
- Core warning: **correlation ≠ causation** (even with big data or a good story).

**Beautiful**

- Somali diaspora **Facebook** networks (Kimo Quaintance).
- Tools: **Netvizz**, **Gephi**; nodes, ties, **eigenvector centrality** (like early **PageRank**).

**Insightful — China, Huai River / heating**

- Greenstone et al.; discontinuity at river; separate fits N/S; jump at zero.
- **PM10:** ~**41.6** µg/m³ (95% CI ~11.6–71.6).
- **Life expectancy:** ~**−3.1** yr (95% CI ~−5.0 to −1.3).
- Heat vs pollution: main point is harm from **particulates**, not “turn off heat” as a naive read.

**Powerful — Gujarat, India**

- Auditors **paid by firms** → conflict of interest (like ratings / corporate audit).
- Fix: **pool-paid** auditors + **back-checks**; **random assignment** (treatment vs control).
- Audit histograms vs truth; **legal change** in Gujarat.
- J-PAL scale: many people in programs backed by **RCT** evidence.

**Misleading**

- Trending series: autism vs **glyphosate**, **organic food**, state comparisons.
- **WDI:** schooling vs log GDP — strong **levels**, weak **growth–growth**; reverse causality / omitted variables.
- **Tyler Vigen**-style spurious pairs; fishing in big data.
- **ML:** good for **prediction**, not automatic truth or causality; “**data by the chock-full**” still needs discipline.

**Roadmap**

- **Probability** → **statistics** → **EDA**, econometrics, **ML** → **causality** (framework, experiments, quasi-experiments).
- **R**, design, finding data → **graphs, tables, text**.

**Logistics (Ellison)**

- Assumes basic algebra/calculus; **no** prior probability/stats required.
- **No** single required textbook.

---

## Week 2 — Lecture 2 — Probability

- **Slides:** `Week 2/mit14_310x_s23_week02_lec02 - Probability.pdf`
- **Transcript:** `Week 2/Lec 02 transcript.pdf`

**Basics**

- **S** = sample space; events = sets; **union, intersection, complement**.
- **Mutually exclusive** vs **exhaustive**.
- **Kolmogorov axioms:** nonnegativity, **P(S)=1**, countable additivity (disjoint events).
- Follows: **P(Aᶜ)=1−P(A)**, **P(A∪B)=P(A)+P(B)−P(A∩B)**, monotonicity.

**Counting / finite equally likely**

- **P(A)=n(A)/n(S)** when outcomes are equally likely.
- Multiplication rule; **with vs without replacement** (e.g. license plates).
- **Supplementary video (permutations & combinations):** [All of Combinatorics in 30 Minutes](https://www.youtube.com/watch?v=VJkvPTY6kZw) — extra walkthrough alongside the lecture.

**Permutations — order matters**

- A **permutation** is an **ordered** lineup: **A,B,C** ≠ **B,A,C** (same three people, different arrangement).
- **All N distinct objects, use every one:** **N** choices for the first spot, **N−1** for the second, … → **N!** total orderings (**N! = N×(N−1)×⋯×1**).
- **Pick n of N distinct objects without replacement, order matters:** **N** choices for the first draw, **N−1** for the second, …, **N−n+1** for the n-th →  
**N×(N−1)×⋯×(N−n+1) = N!/(N−n)!** (“**N** permute **n**”).
- **Read it as slots:** *slot 1* has **N** options; *slot 2* has **N−1**; …; *slot n* has **N−n+1** — multiply.
- **Lecture tie-in:** Massachusetts **vehicle license plate** (the metal tag on a car); **“no repeat” rule:**
  - **What you’re counting:** different **license plates** the state could issue — each plate is a string of **6 characters** printed on that tag.
  - **Each license plate** has **6 positions** in a row. Each position is **one** character from **26 letters + 10 digits = 36** possibilities.
  - **Special rule in this example:** on a given **license plate**, the **same** letter or digit **cannot appear twice** (no duplicate character on that one plate).
  - Count: **36** choices for 1st position on the plate, **35** for 2nd, **34** for 3rd, …, **31** for 6th → **36×35×34×33×32×31** possible **license plates**.
  - Same count as **permutations of 6 symbols chosen from 36** = **36!/(36−6)! = 36!/30!** (left-to-right order on the **license plate** matters: `ABC123` ≠ `CBA321`).

**Combinations — order does not matter**

- A **combination** is a **subset** of **n** objects chosen from **N**: only **which** items are in the group counts, not the **order** you listed them in.
- **Link to permutations:** count ordered picks **N!/(N−n)!**, then divide by **n!** because each **unordered** group appears in **n!** different orders →  
**N choose n** = **N!/((N−n)!n!)** (read “**N** choose **n**”).
- Special case **n = 2:** **N choose 2** = **N(N−1)/2** (each pair counted once).
- **Lecture tie-in — handshakes (pairs of people):**
  - **Goal:** A **number** — **how many handshakes** in total when **every** pair of people in a group shakes hands **exactly once** (e.g. all candidates on stage). Not a probability; just counting distinct **person–person** pairs.
  - **What that means:** each **unordered** pair **{A, B}** is **one** handshake.
  - **Step 1 — line up two people in order (temporary):** pick who is “**first**” in the pair → **N** choices; pick who is “**second**” → **N−1** choices (someone else). That gives **N×(N−1)** **ordered** pairs (e.g. **Trump** then **Cruz** vs **Cruz** then **Trump**).
  - **Step 2 — handshakes don’t have order:** those two orderings are the **same single handshake**, so every handshake was counted **twice**. **Divide by 2.**
  - **Count:** **N×(N−1)/2** handshakes — same as **N choose 2**.
  - **Lecture numbers:** **9** candidates → **9** choices for first slot, **8** for second → **9×8 = 72** ordered pairs → **72/2 = 36** handshakes.
- **Lecture tie-in — Area Four pizza (pairs of toppings):**
  - **Goal:** A **probability** — you randomly pick **2** toppings (see setup). You want **P**(your pizza ends up **mixed**) = **P**(**exactly one** vegetarian **and** **exactly one** non-vegetarian). Not “two veg” or “two meat.”
  - **Plan:** (1) Count **all** equally likely **two-topping** outcomes → denominator **55**. (2) Count outcomes that are **mixed** → numerator **30**. (3) **P = 30/55**.
  - **Setup:** **6** vegetarian and **5** non-vegetarian names (**11** toppings total). Each name is on a slip; you **draw 2 different slips** for one pizza — the pizza only cares **which two** toppings you got, **not** which slip you drew **first** vs **second**.
  - **Sample space — step 1 (ordered draws):** first slip **11** choices, second slip **10** choices (no repeat) → **11×10 = 110** **ordered** pairs `(first draw, second draw)`.
  - **Sample space — step 2 (unordered pair):** `(pepper, mushroom)` and `(mushroom, pepper)` are the **same pizza**, so every **unordered** pair was counted **twice** → **110/2 = 55** different **two-topping** outcomes — same as **11 choose 2** = **11×10/2**.
  - **Event (one veg, one non) — step 1 (ordered):** **veg** then **non** → **6×5 = 30**; **non** then **veg** → **5×6 = 30** → **60** ordered mixed pairs.
  - **Event — step 2:** each **mixed** unordered pair **{veg, non}** still appears in **two** orders → **60/2 = 30** favorable outcomes (same as **6×5** if you think “pick **which** veg × **which** non” once).
  - **Probability:** **P = 30/55**. (Lecture: this story later motivates the **hypergeometric** distribution.)
- **Lecture tie-in — faculty offices (Esther & Sara adjacent):**
  - **Goal:** A **probability** — **40** distinct people are assigned at random to **40** offices in a **fixed row** (one person per office). You want **P(Esther and Sara end up in neighboring offices)**.
  - **Sample space — what one outcome is:** A complete **assignment** “**who** sits in **office 1**, **office 2**, …, **office 40**.” Offices are **labeled**; **people** are **distinct**. Every assignment is **equally likely** if all **40!** orderings of people into the row are equally likely (**40** choices for office **1**, **39** for office **2**, … → **40!** outcomes — same **permutation** logic as the license plate slots, but here you use **all 40** symbols).
  - **Denominator:** **n(S) = 40!**.
  - **Event — the “block” idea:** Whenever Esther and Sara are **next to each other**, you can picture them as **one glued unit** (a **block**) that occupies **two side-by-side** offices. The block can read **Esther–Sara** or **Sara–Esther** along the row → **2** internal orders (**2** ways to orient the pair inside the block).
  - **Numerator — count favorable assignments:** Treat **{block}** + **the other 38 people** as **39 objects** to lay out in order along the row. Each ordering of these **39** objects pins down **exactly one** full seating of all **40** people (the block always fills **two consecutive** spots as one chunk). There are **39!** ways to order the **39** objects, and **×2** for **ES** vs **SE** inside the block → **n(A) = 2×39!**.
  - **Same kind of outcome as the denominator:** **n(A)** and **n(S)** both count **complete** assignments — **every** person in **some** office — so the ratio **n(A)/n(S)** is a real probability for “random full seating.” A count that only fixes Esther and Sara (e.g. **39×2** for **which adjacent pair** × **ES/SE**) is **not** enough: it leaves the **other 38** people unspecified.
  - **Why every ordering of the others matters:** For **each** valid placement/order of Esther and Sara, there are **38!** ways to put the **remaining 38** faculty in the **remaining 38** offices. Each of those is a **different** outcome (different people in different rooms), so they all belong in **n(A)**. Equivalently: **39×2×38! = 2×39!** (because **39×38! = 39!**).
  - **Probability:** **P(A) = (2×39!)/40!**. Since **40! = 40×39!**, this simplifies to **2/40 = 1/20**. (If you **condition** on Esther’s office: **end** offices give Sara only **1** adjacent slot → **1/39**; **interior** offices give **2** slots → **2/39**; weighting by Esther’s position still averages to **2/40** — same answer as the **block** count.)

**Other counting examples (shorter)**

- **Dice:** ordered outcomes (permutation-style product **6×6** for two dice).

**Independence**

- **P(A∩B)=P(A)P(B)** — learning **B** doesn’t change odds of **A**.
- If **A,B** independent → **A** and **Bᶜ** independent.
- **Lecture tie-in — Steph Curry (binomial preview):**
  - **Goal:** **P(exactly 3 makes** and **3 misses in 6 attempts)** — **3** successes in **6** **independent** tries (**Bernoulli trials**).
  - **Setup (lecture numbers):** **P(make) = p = 0.44**; **P(miss) = q = 1 − p = 0.56**. Independence means probabilities **multiply** along a sequence of outcomes.
  - **Step 1 — one specific sequence:** e.g. **Make-Make-Make-Miss-Miss-Miss** (**MMMXXX**). **P(that sequence) = p³q³ = 0.44³ × 0.56³ ≈ 0.01496** (≈ **0.015** rounded).
  - **Step 2 — how many sequences:** Any ordering with **exactly 3** makes in **6** ordered slots uses **three** factors **p** and **three** factors **q**, so each such sequence has the **same** probability **p³q³**. Count orderings: **(6 choose 3)** = **6!/(3!(6−3)!)** = **(6×5×4)/(3×2×1)** = **20** (e.g. **MXMXMX**, **XXXMMM**, …).
  - **Step 3 — total:** **P(exactly 3 makes)** = **20 × 0.015 = 0.30** — about **30%** for a **3-for-6** line under these assumptions.
  - **General form (binomial PMF):** **P(exactly k successes in n trials)** = **(n choose k) p^k (1−p)^(n−k)** when trials are **independent** with the same **p**.
- **Related (complement):** **P(at least one make in n tries) = 1 − P(all misses) = 1 − q^n** — same “multiply independent probabilities” idea.

**Conditional probability & partitions**

- **P(A|B)=P(A∩B)/P(B)**.
- **Law of total probability:** e.g. **P(W)=Σᵢ P(W|Aᵢ)P(Aᵢ)** (nomination → general election).

**Bayes / base rates**

- **P(A|B)=P(B|A)P(A)/P(B)**; expand **P(B)** over disease / not-disease (partition).
- Want **P(disease | +)**, not **P(+ | disease)**.
- Rare disease: many healthy people → lots of **false positives** even at low **P(+|healthy)**.
- A **+** is weak evidence unless **prior** is high or test is very accurate.
- **Lecture (Zika-style):** **P(Z)≈0.001**, **P(+|Z)≈0.99**, **P(+|Zᶜ)≈0.05** → **P(Z|+)≈0.019** (~2%).
- Interpretation: belief moves up from **0.1%**, but **P(+)** is still mostly healthy people testing positive.

**Confusion-matrix intuition (~1000 people, easier counts)**

- Same test as above: **P(+|Z)≈0.99**, **P(+|Zᶜ)≈0.05**. For the table only, assume **P(Z)=10%** (not the lecture’s **0.1%**) so each cell is a **round integer** you can picture. The **logic** is the same; rarer disease just shrinks the sick row and makes **P(Z|+)** even smaller.
- **Rows** = truth (**actually sick** vs **actually not**). **Columns** = test (**positive** vs **negative**).
- **100** sick, **900** not sick → multiply by hit/miss rates: sick row **99** vs **1**; not-sick row **45** vs **855**.


|                       | **Test: positive**  | **Test: negative**  |
| --------------------- | ------------------- | ------------------- |
| **Actually sick**     | 99 (true positive)  | 1 (false negative)  |
| **Actually not sick** | 45 (false positive) | 855 (true negative) |


- **P(sick | test +)** = sick & positive **÷** all positive = **99 / (99+45) = 99/144 ≈ 69%** (up from **10%** prior, but **not** **99%** — many **+** are still healthy).
- Compare to lecture: with **P(Z)=0.1%**, the positive column is almost all **false positives**, so **P(Z|+)≈2%**.

