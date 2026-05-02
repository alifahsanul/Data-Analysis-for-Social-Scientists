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
- **What each rate is:** **P(+|Z)≈0.99** = **true positive** rate (sensitivity): infected → test **+**. **P(+|Zᶜ)≈0.05** = **false positive** rate: **not** infected but test **+** anyway — so **0.05** is **not** a false-negative rate. **False negative** rate is **P(−|Z)** ≈ **1 − 0.99 = 0.01** (infected but test **−**).
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

---

## Week 2 — Lecture 3 — Random Variables, Distributions, and Joint Distributions

- **Slides:** `Week 2/Lecture 03 Random Variables, Distributions, and Joint Distributions.pdf`
- **Transcript:** `Week 2/Lecture 03 Transcript - Random Variables, Distributions, and Joint Distributions.pdf`
- **OCW mirror (same content):** [Lecture 3 resource page](https://ocw.mit.edu/courses/14-310x-data-analysis-for-social-scientists-spring-2023/resources/mit14_310x_s23_week02_lec03_pdf/) — direct PDF: `mit14_310x_s23_week02_lec03.pdf`

**Housekeeping / near-term schedule (lecture)**

- Same week: **Tuesday** (Esther) — examples, data sources / gathering (e.g. web scraping), **histograms** and **kernel density** plots (ways to **estimate** distributions from data).
- **Wednesday** — independence of random variables, conditional distributions, maybe more.
- **Friday recitation** — mostly **R** tutorial; possible **probability hints** for the problem set depending on what it covers.

**Random variables**

- A **random variable** is a **real-valued function** whose **domain is the sample space** (e.g. sum of two dice, Curry’s makes in six attempts, count of veg toppings on a random pizza); formally **X : S → ℝ**.
- Contrast (slide graphic): **P** assigns probabilities to **events** (subsets of **S**) and takes values in **[0, 1]**; **X** assigns a **number** to each outcome. **Probability on S** **induces the distribution** of **X**.

**Discrete vs continuous**

- **Discrete:** finite or **countably infinite** support (examples so far are discrete).
- **Continuous:** can take any value in an interval (bounded or not); course will **use continuous a lot**, partly because many discrete situations are **well approximated** by continuous models, and because **math for functions of RVs** is often **simpler** in the continuous setup.

**Discrete — probability mass function (PMF, also called PF)**

- Start from a story → assign **P(X = x)** for each possible **x** → tabulate or plot; that function is the **PMF** (**P**robability **M**ass **F**unction; often just called **PF** in these notes).
- **Graph convention:** vertical segments under each mass point; each point is a **point mass**.

**Hypergeometric — Area Four pizza (veg count)**

- **Story:** You pick **n** distinct toppings **without replacement** from the **Area Four** “extra toppings” list. **X** = how many of your **n** picks are **vegetarian**.
- **Counts from the menu (lecture):** **N = 11** toppings total — **K = 6** vegetarian, **N − K = 5** non-vegetarian (meat/fish). **Veg (6):** e.g. caramelized onions, pickled banana peppers, mushrooms, green olives, arugula, 2 farm eggs. **Non-veg (5):** e.g. sopressata, sausage, bacon, chicken, marinated white anchovies.
- **Model:** **X ~ H(N, K, n)** with **N = 11**, **K = 6**. Support: **x = 0, 1, …, min(K, n)** (you cannot draw more veg toppings than exist or than **n**).
- **PF (same as Lecture 2 counting):** choose **x** veg from **6**, and **n − x** non-veg from **5**, divided by all ways to choose **n** from **11**:
  - $P(X = x) = \dfrac{\binom{6}{x}\binom{5}{n-x}}{\binom{11}{n}}$ when **0 ≤ x ≤ min(6, n)** and **n − x ≤ 5**; **0** otherwise. **0! = 1** so **x = 0** is fine.
- **Why probabilities depend on n:** the denominator **C(11, n)** and the non-veg factor **C(5, n−x)** both change when you change **n** (e.g. **n = 2** in Lecture 2’s “mixed pizza” problem vs **n = 3** below).

**PMF for n = 3** (slide numbers — replaces the plotted PF)


| **x** (veg count) | **P(X = x)** | **≈ decimal** |
| ----------------- | ------------ | ------------- |
| 0                 | 6/99         | ≈ 0.061       |
| 1                 | 36/99        | ≈ 0.364       |
| 2                 | 45/99        | ≈ 0.455       |
| 3                 | 12/99        | ≈ 0.121       |


- **Check:** **6 + 36 + 45 + 12 = 99** → probabilities sum to **99/99 = 1**. Same PMF as **10/165, 60/165, 75/165, 20/165** (numerators **C(6,x)C(5,3−x)** for **x = 0,…,3**).
- Notation on slides may use **x** for the veg count and **n** for draws; a fully pedantic PF sets **f_X(x) = 0** off the support.

**Binomial — Curry threes**

- **X** = number of makes in **n** **independent** trials with same **p** = **P(make):** **X ~ B(n, p)**.
- **Lecture instance:** **n = 6**, **p** consistent with Lecture 2 (~**0.44**); rounded PF: **P(0)≈.03**, **P(1)≈.15**, **P(2)≈.29**, **P(3)≈.30**, **P(4)≈.18**, **P(5)≈.06**, **P(6)≈.01**.
- **p = 0.5** → symmetric PF; shape **foreshadows** the **normal** distribution (visual in slides).

**PF properties (discrete)**

- $f_X(x) = P(X = x)$.
- $0 \le f_X(x_i) \le 1$; $\sum_i f_X(x_i) = 1$; for an event $A$, $P(X \in A) = \sum_{x_i \in A} f_X(x_i)$.

**Continuous — probability density function (PDF)**

- Usually given a **density** **f_X** (not built step-by-step from a verbal lattice like many discrete examples).
- **X** is **continuous** if there exists **f_X ≥ 0** such that for any (nice) set $A$, $P(X \in A) = \int_A f_X(x)dx$.
- **Properties:** $f_X(x) \ge 0$; $\int_{-\infty}^{\infty} f_X(x)dx = 1$; $P(a \le X \le b) = \int_a^b f_X(x)dx$.
- **Not** like discrete mass: **P(X = x) = 0** for every **x**; **f_X(x)** is **not** “probability at x” and **can exceed 1** — only **areas** under the curve are probabilities.
- **PMF vs PDF (quick diff):** **PMF** = exact-point probabilities for **discrete** outcomes, $P(X=x)$; **PDF** = density for **continuous** outcomes, where probabilities come from **integrals over intervals** (area under curve), not from a point value.

**Terminology**

- “**Distribution** of **X**” is used loosely for either a **PF** or a **PDF**; notation and vocabulary **vary by source** — stay consistent within one problem.

**Uniform**

- **X ~ U[a, b]** on **[a, b]**: **f_X(x) = 1/(b−a)** on **[a, b]**, **0** otherwise.
- Probability over **[c, d] ⊂ [a, b]** = **(d−c)/(b−a)** (length ratio; same as integrating the flat density).

**Cumulative distribution function (CDF)**

- **F_X(x) = P(X ≤ x)** — same idea for **discrete or continuous**.
- **Properties:** **0 ≤ F_X(x) ≤ 1**; **non-decreasing**; limits **0** as **x → −∞**, **1** as **x → +∞**; **right-continuous**.
- **Discrete:** **F** has **jumps** at mass points; **continuous:** **F** is continuous (typically).

**Linking PF/PDF and CDF**

- Same information, different form; each determines the other.
- **Continuous case:** $F_X(x) = \int_{-\infty}^{x} f_X(t)dt$; where **F_X** is differentiable, $F_X'(x) = f_X(x)$ (slides: “**except possibly finitely many points**” caveats for corner cases).

**Joint distributions**

- Motivation: study **relationships** — e.g. rainfall & yield; express vs regular line lengths; **veg and non-veg counts** on a pizza; FX rate & exporter’s stock price.
- **Continuous (X, Y):** joint **PDF** $f_{X,Y}(x,y)$ with $P((X,Y) \in A) = \iint_A f_{X,Y}(x,y)dxdy$; integrates to **1** over the plane; **a point or a curve** has probability **0**.
- **Discrete analogue:** **f_{X,Y}(x,y) = P(X=x, Y=y)** (joint PF); slides focus definitions on continuous but idea parallels.

**Worked joint example — headache meds**

- One tablet **naproxen** (duration **X**) and one **acetaminophen** (**Y**), **independent**-looking joint density on **x, y ≥ 0**: **f_{X,Y}(x,y) = λ² e^{−λ(x+y)}**.
- **Both active within 3 hours:** **P(X ≤ 3, Y ≤ 3) = (1 − e^{−3λ})²** (product structure from integrating over the rectangle).
- **Sequential dosing:** take acetaminophen only **after** naproxen wears off → interest in **P(X + Y ≤ 3)** (integral over a **triangle**, not the rectangle; setup left as “details at home” on slides).
- **New variable** **Z = X + Y** (total relief when taken in sequence): **F_Z(z) = P(Z ≤ z) = 1 − (1 + zλ)e^{−zλ}** for **z > 0**; **f_Z(z) = F_Z′(z) = λ² z e^{−zλ}** for **z > 0** (**Gamma**-type shape, **shape 2**, rate **λ**).

---

## Week 2 — Lecture 4 — Gathering and Collecting Data

- **Slides:** `Week 2/Lecture 04 - Gathering and Collecting Data.pdf`
- **Transcript:** `Week 2/Lecture 04 Transcript - Gathering and Collecting Data.pdf`

**Main frame**

- Three practical routes: **existing data libraries**, **extracting from the internet** (API/scraping), and **collecting your own data**.
- Practical advice: start from the **question**, then search for the best feasible data source (free, purchasable, restricted-access, or self-collected).

**Existing data sources (examples from lecture)**

- Public/data repositories: **Data.gov**, **IPUMS** (US + international), **ICPSR**, **Harvard Dataverse**, **Amazon public datasets**.
- International survey sources: **DHS**, **World Bank LSMS**, **RAND** panels.
- Research replication archives: **J-PAL/IPA** and **AEA** journal data posting requirements.
- Data quality reminder: even trusted datasets need scrutiny (question wording, recall error, measurement validity).

**Cross-sections, panels, and quality checks**

- **Repeated cross-section:** resample comparable units over time (not the same individuals/households).
- **Panel data:** track the **same unit** over time (household/farm/village/state, etc.).
- **Back-checks** are quality control re-visits on a subset of questions; they are different from follow-up waves.

**Internet data: API vs scraping**

- Prefer a platform **API** when available (structured access, terms/limits).
- If no API or insufficient API, scrape webpage structure (e.g., parse classes/fields into a table).
- Tools highlighted: Python (**requests**, **BeautifulSoup**), and in R (**rvest**, `readHTMLTable` for simple tables).
- Constraints are common: rate limits, anti-bot barriers, changing page structure, and engineering overhead.

**Collecting your own data**

- Feasible options: online surveys, app-based passive collection (with consent), field questionnaires, dedicated survey teams.
- Recommended workflow: funding/resources → data management/security plan → IRB/COUHES approval → instrument design/pilot → implementation.
- Lecture emphasis: modern digital collection (tablets/phones) generally outperforms paper on cost + data quality workflows.

**Ethics and human subjects**

- Human-subject research is governed by IRB frameworks (Belmont principles: **respect for persons, beneficence, justice**).
- Distinction stressed in lecture: firms can often run product experiments under user agreements; **research intended for generalizable knowledge/publication** triggers stricter human-subject requirements.

**Transition to next lecture content**

- Lecture closes by starting **EDA for distributions**: histograms, kernel density estimates, bandwidth trade-off (variance vs bias), and plotting/diagnostics in R.

---

## Week 3 — Lecture 05 — Summarizing and Describing Data

- **Slides:** `Week 3/Lecture 05 Summarizing and Describing Data.pdf`
- **Transcript:** `Week 3/Lecture 05 Transcript Summarizing and Describing Data.pdf`

**EDA workflow (lecture focus)**

- Start by plotting raw distributions before modeling assumptions.
- Main tools: **histograms**, **kernel density estimates**, and **CDF plots**.
- In R/`ggplot2`, default settings are a useful baseline, then adjust deliberately.

**Histograms and kernel density**

- Histograms are bin-based approximations; shape can change with bin width.
- Kernel density is a smooth, non-parametric estimate using weighted local information.
- Choice of kernel (e.g., Epanechnikov vs Gaussian) usually matters less than **bandwidth**.
- Bandwidth trade-off: too small -> noisy/high variance; too large -> oversmoothed/high bias.
- Practical guidance: start with R default bandwidth (`nrd0`), then check sensitivity.

**Comparing distributions: PDF vs CDF**

- PDF/kernel is better for seeing shape: mode, skewness, tail thickness.
- CDF is better for probability comparisons because vertical distances are easier to compare than areas.
- Visual first-order stochastic dominance: if one CDF is always below another, it tends to have larger values across thresholds (example: US vs Bihar female heights).

**Bivariate and joint distributions**

- Separate 1D plots can hide structure when variables are related (e.g., shot location on a basketball court).
- Use joint displays (2D histogram/heatmap/3D surface) to reveal clustering patterns (e.g., bunching near 3-point line and near basket).

**Data-quality caution from top-income example**

- Administrative microdata can be **top-coded** (privacy protection), creating artificial mass points in upper tails.
- For top-income shares over time, lecture highlights using tax tabulations plus a Pareto-tail approximation (Piketty-Saez style) to recover top-share statistics.

---

## Week 3 — Lecture 06 — Joint, Marginal, and Conditional Distributions

- **Slides:** `Week 3/Lecture 06 Joint, Marginal, and Conditional Distributions.pdf`
- **Transcript:** `Week 3/Lecture 06 Transcript Joint, Marginal, and Conditional Distributions.pdf`
- **OCW mirror (same content):** [Week 3 — Lecture 6](https://ocw.mit.edu/courses/14-310x-data-analysis-for-social-scientists-spring-2023/pages/week-3/) — slides resource: [Lecture 6 PDF](https://ocw.mit.edu/courses/14-310x-data-analysis-for-social-scientists-spring-2023/resources/mit14_310x_s23_week03_lec06_pdf/); transcript: `1pBw6Y3O7_Y19n4fJ76a8Wniwg8eiOcqa_transcript.pdf` on that page

**Framing**

- Builds on the joint-PDF material from earlier weeks; works a **continuous** joint example (DeGroot & Schervish–style) with **3D pictures** of the surface over the support, then **marginals**, **independence**, and **conditionals** (discrete tennis PF + same continuous example).
- **Marginals alone do not determine the joint:** a joint distribution encodes (i) how **X** behaves, (ii) how **Y** behaves, and (iii) how they **relate** — you need (iii) to go from marginals back to a joint law.

**Continuous joint PDF — support, constant c, region probability**

- **Model:** $f_{X,Y}(x,y) = c\,x^2 y$ when **x² ≤ y ≤ 1**, and **0** otherwise (so **x ∈ [−1, 1]** from the inequalities).
- **Support:** region in the **(x, y)**-plane between **y = x²** and **y = 1** (draw this first; integrate only where density is positive).
- **Normalize:** $\iint_{\text{support}} c\,x^2 y\,dy\,dx = 1$ → inner integral over **y** from **x²** to **1**, outer **x** from **−1** to **1** gives **(4/21)c = 1**, so **c = 21/4**.
- **P(X > Y):** intersect **{x > y}** with the support → integrate over the **sliver** where **y** runs from **x²** to **x** and **x** from **0** to **1** → **P = 3/20** (lecture’s limits).

**Marginal distributions**

- **Discrete:** $f_X(x) = \sum_y f_{X,Y}(x,y)$ — fix **x**, add all **y** (same idea as “add along a row” in a table).
- **Continuous:** $f_X(x) = \int f_{X,Y}(x,y)\,dy$ (integrate out **y** over the **y**-slice of the support for that **x**); analogously $f_Y(y) = \int f_{X,Y}(x,y)\,dx$.
- **From the lecture’s continuous example:** for **x ∈ [−1, 1]**, $f_X(x) = \int_{x^2}^{1} \frac{21}{4} x^2 y\,dy = \frac{21}{8} x^2 (1 - x^4)$ (slides use an **indicator** on **x** for pedantry). For **y ∈ [0, 1]**, $f_Y(y) = \int_{-\sqrt{y}}^{\sqrt{y}} \frac{21}{4} x^2 y\,dx = \frac{7}{2} y^{5/2}$.
- **Tennis (discrete joint PF):** **X** and **Y** = unforced errors per game for the two players; correlation in play quality concentrates mass near **x ≈ y** (few joint mass on “one very high, one very low”). After summing out the other variable, the **marginal** laws for **X** and **Y** **coincide** in the toy table (e.g. **P(X = 0) = 3/8**, **P(X = 1) = 5/16**, … — illustrative numbers from the lecture, not “real” match data).

**Independence of random variables**

- **Definition (events-style):** **P(X ∈ A, Y ∈ B) = P(X ∈ A)P(Y ∈ B)** for **all** (nice) **A, B** — hard to check directly.
- **Usable equivalents:** joint **CDF** factors as product of marginals; with densities, **joint PDF = f_X(x) f_Y(y)** **iff** independent.
- **Continuous shortcut:** if a joint PDF exists, independence **iff** the density **factors** as **g(x) h(y)** with **g, h ≥ 0** (functions of **x** and **y** alone) — **but** the **support** must allow factorization too: if the region where **f > 0** forces **y** to depend on **x** (e.g. **x² ≤ y ≤ 1**), variables are **not** independent even when **c x²y** looks multiplicative on the formulas alone.
- **Headache-pill example (earlier lecture):** **f_{X,Y}(x,y) = λ² e^{−λ(x+y)}** on **x, y ≥ 0** **does** factor → **X** and **Y** independent (same marginal shape for each drug’s duration).
- **Tennis table:** some **(x, y)** regions have **zero** joint probability while the **product of marginals** is **positive** → violates independence.
- **Discrete tables:** independence **iff** **every row** is proportional to every other row **iff** **every column** is proportional to every other column.

**Conditional distributions**

- **Discrete:** $P(Y=y \mid X=x) = f_{X,Y}(x,y) / f_X(x)$ (when **f_X(x) > 0**). A **slice** of the joint table at fixed **x** is **not** yet a PMF — **renormalize** so probabilities sum to **1** (lecture: condition on **Y = 2**, use **P(Y = 2) = 5/32** from the **marginal of Y** to scale the slice).
- **Continuous:** $f_{Y \mid X}(y \mid x) = f_{X,Y}(x,y) / f_X(x)$ for **x** with **f_X(x) > 0**; expression can involve both **x** and **y**, but **plug in** a fixed **x** to get a **density in y** only (lecture: **x = 1/2** → **y** from **1/4** to **1**, gives **f_{Y \mid X}(y \mid 1/2) ∝ y**, normalized to **(32/15) y** on that interval).
- **Link to independence:** **f_{Y \mid X} = f_Y** (conditional equals marginal) **iff** **X** and **Y** are independent — conditioning carries **no** information about the other variable.

**Bridge to next topic**

- **Statistics** are **functions of random variables** (e.g. sample mean); next lectures develop **distributions of transforms** **h(X)** or **h(X₁,…,X_n)**. Preview: if **Y = |2X + 3|**, track how scaling **stretches** the PDF and **|·|** **folds** mass from negative **x** to positive support (area still **1**).

---

## Week 4 — Lecture 07 — Functions of Random Variables

- **Slides:** `Week 4/Lecture 07 Slides - Functions of Random Variables.pdf`
- **Transcript:** `Week 4/Lecture 07 Transcript - Functions of Random Variables.pdf`

**Framing and method**

- Goal: given a known distribution for **X**, derive the distribution of **Y = h(X)**.
- Method emphasized in lecture: (1) find **CDF** via $F_Y(y)=P(h(X)\le y)$ by integrating over the correct region; (2) differentiate to get **PDF** when **Y** is continuous.
- Which derivation tricks are available depends on context: discrete vs continuous, one variable vs vector, invertible vs non-invertible transformation.

**Warm-up example: $Y=X^2$ with $X \sim U[-1,1]$**

- Support mapping: **X in [-1,1]** implies **Y in [0,1]**.
- CDF steps: $F_Y(y)=P(X^2\le y)=P(-\sqrt y\le X\le \sqrt y)=\int_{-\sqrt y}^{\sqrt y} \frac12 dx=\sqrt y$, for $0\le y\le1$.
- Piecewise CDF: $F_Y(y)=0$ for $y<0$, $F_Y(y)=\sqrt y$ for $0\le y\le1$, $F_Y(y)=1$ for $y>1$.
- PDF: $f_Y(y)=\frac{1}{2\sqrt y}$ on $(0,1)$, and $0$ otherwise.
- Intuition: squaring “folds” negative and positive **X** onto the same positive **Y**, creating high density near 0.

**Important example 1: linear transformation**

- If **Y = aX + b** with $a\neq0$, CDF algebra splits by sign of $a$ (inequality direction flips when $a<0$).
- Final density formula (both cases compactly):  
  $f_Y(y)=\frac{1}{|a|}f_X\left(\frac{y-b}{a}\right)$.
- Interpretation: translation by $b$ shifts the distribution; scaling by $a$ stretches/compresses by $|a|$.
 
Examples (concrete — Curry shot feet → meters):

- Real-world setup: suppose we model Steph Curry's shot distance $X$ measured in feet. As a simple parametric example, let

  $X \sim N(23, 5^2)$  (mean 23 ft, SD 5 ft)

  (these numbers are illustrative — think of 23 ft as a typical 3-point/long-two distance and 5 ft as a plausible spread).

- Convert to meters with the linear transform $Y = aX + b$ where $a = 0.3048$ (1 ft = 0.3048 m) and $b = 0$. Then

  $Y = 0.3048\,X \Rightarrow Y \sim N(23\times 0.3048,\ (5\times 0.3048)^2) = N(7.0104,\ 1.524^2)$

  So Curry's shot distance is about 7.01 meters on average with SD $\approx 1.524$ m.

- PDF relationship (numeric): the general formula $f_Y(y) = \frac{1}{|a|} f_X\!\left(\frac{y-b}{a}\right)$ becomes here

  $f_Y(y) = \frac{1}{0.3048} f_X\!\left(\frac{y}{0.3048}\right) \approx 3.28084\, f_X(3.28084\, y).$

  Intuition: converting feet → meters compresses distances ($a<1$), which reduces the SD and stretches the density vertically by $1/a$ so areas remain probabilities.

**Important example 2: probability integral transform**

- If **X** is continuous and $Y=F_X(X)$, then $Y\in[0,1]$ and $F_Y(y)=y$ on $[0,1]$.
- Therefore $Y\sim U[0,1]$: transforming a continuous RV by its own CDF yields uniform draws.
- Reverse direction: if $U\sim U[0,1]$, then $F^{-1}(U)$ has CDF $F$ (under standard regularity conditions).
- Practical use in simulation: many RNGs provide uniform pseudo-random numbers, then inverse-CDF transforms generate draws from target distributions (exponential, beta, etc.).

**Important example 3: convolution (sum of independent RVs)**

- In probability, convolution refers to the distribution of a sum of independent RVs.
- For independent continuous **X, Y** and $Z=X+Y$, joint density is $f_{X,Y}(x,y)=f_X(x)f_Y(y)$.
- CDF route: $F_Z(z)=P(X+Y\le z)=\int_{-\infty}^{\infty}\int_{-\infty}^{z-y} f_X(x)f_Y(y)\,dx\,dy$.
- Differentiate to get convolution formula:  
  $f_Z(z)=\int_{-\infty}^{\infty} f_X(z-y)f_Y(y)\,dy$.
- Generalizes naturally to sums of $N$ independent RVs and linear combinations.

**Important example 4: order statistics**

- Setup: $X_1,\dots,X_n$ i.i.d. continuous; define max $Y_n=\max\{X_1,\dots,X_n\}$ (the $n$-th order statistic).
- CDF of max: $F_{Y_n}(y)=P(X_1\le y,\dots,X_n\le y)=[F_X(y)]^n$.
- PDF of max: $f_{Y_n}(y)=n[F_X(y)]^{n-1}f_X(y)$.
- For min $Y_1=\min\{X_1,\dots,X_n\}$: $f_{Y_1}(y)=n[1-F_X(y)]^{n-1}f_X(y)$.
- Example with $X_i\sim U[0,1]$, $n=5$: max has $f(y)=5y^4$, min has $f(y)=5(1-y)^4$, both on $[0,1]$.
- As $n$ grows: min mass concentrates near 0 and max mass near 1 (in the limit, point-mass behavior at edges).

