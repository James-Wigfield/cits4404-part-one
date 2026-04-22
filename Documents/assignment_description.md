# CITS4404 Team Project: Building AI Trading Bots

---

## Context and Aims

Automated algorithms, or bots, now perform a substantial percentage of the world's trading. It is difficult to know the exact numbers (and depends how broadly you define algorithmic trading) with some estimates suggesting around 70% of share trading is performed by bots, with digital assets perhaps higher at around 80%. Trading bots can work 24/7, react quickly to changes in the markets, and are not subject to human emotions that some suggest can lead to poor trades. Trading bots can be sold or rented on subscription. There is no doubt that trading bots are big business!

In this assignment we will use adaptive AI techniques to build trading bots. We'll do this for the digital asset Bitcoin — the world's hardest currency — but the same bots could be used for other currencies, for crypto tokens, for stocks, commodities and the like. The bot itself is "agnostic" to what the underlying data represents, although it would be optimised differently for different domains.

In this assignment you will be given the building blocks of a bot that utilises the most widely adopted type of trading signal. We will see how building the bot is a multi-dimensional optimisation problem.

Nature-inspired algorithms (or adaptive algorithms) are designed to seek good solutions to difficult, high-dimensional optimisation problems. They typically use a population of candidate solutions that are adapted according to some heuristics that seek to find improved solutions.

The practical aim of this project is to apply one or more nature-inspired algorithms to develop an effective trading bot. In doing so, we seek to learn more about problem representation and its impact on hypothesis space size and difficulty, as well as nature-inspired algorithms and how they compare with each other and with more traditional approaches.

The structure of the assignment follows a typical research project, albeit in a shorter timeframe — review of relevant literature, implementation and experimentation, and evaluation. For simplicity it is divided into two parts:

- Investigate and compare a number of nature-inspired algorithms, focussing on their distinguishing characteristics that will determine their promise for the task.
- Compare the performance of selected algorithms by developing and testing your trading bot.

Part 1 includes a milestone deliverable. It is expected that work on Part 2 can begin in parallel to Part 1 however. It is up to the team to apportion and manage the tasks.

---

# Part I: Research Paper — Nature-inspired Algorithms

The first part of the project takes the form of a small literature review. It involves researching nature-inspired optimisation algorithms, one or more of which can be selected to implement and experiment with in Part 2. You should read through the specification for Part 2 prior to conducting the review to help you think about which algorithms may be most relevant and ultimately inform your algorithm choice. To accelerate the process a palette of suggested algorithms is provided.

The Mendeley Data repository includes a dataset uploaded by Alexandros Tzanetos that seeks to provide a comprehensive collection of all "nature-Inspired algorithms" (sometimes referred to as metaheuristic algorithms, population-based stochastic algorithms or generically as "evolutionary" algorithms) that have been published to-date as at January 2021. While it is almost impossible to produce a truly comprehensive list, it is an impressive attempt that includes almost 300 algorithms or variants, categorised according to natural phenomena they seek to mimic or use as an explanatory metaphor.

### Getting Started

- Read through the Tzanetos et al.[^1] and the repository's Description.txt[^2].
- Download the dataset and import it into a spreadsheet. Notice that the list is sorted by Category, Subcategory then name. Opening it as a spreadsheet will allow you to sort on other criteria, such as year, that may help you establish the chronology of the algorithms.

Some additional lists of algorithms can be found in Bayzidi et al.[^3] (see Table 1) and Price et al.[^4] (see Table 1).

A constraint on the algorithms you choose to investigate is that they must be **optimisation algorithms** (not for example, neural networks or machine learning algorithms). At least one (but likely all) will also be **"population-based" algorithms**, meaning they maintain a collection of candidate solutions and adapt these in some way to find better solutions.

The goal of Part 1 is to familiarise yourself with a number of algorithms and provide a synopsis on their distinguishing features. **The number of algorithms summarised should correspond to the number of members of your team.** You might ask each member of the team to research one algorithm and discuss it with the group prior to writing the report — if it can be communicated in an understandable way to the group then it is more likely to be understandable in the report.

In the second part of the project you will select one or more of these algorithms to test and compare. It may be worth considering, in this context, whether you wish to explore "variants on a theme" in one Category, or explore more than one Category.

---

## Deliverable 1: Synopses

For each algorithm you should provide a **1–1½ page synopsis**.

As you work through the selected paper (and any supporting literature) you should seek to address the following questions, and reflect this in your own document.

> These are the kinds of questions you would be asking yourself as a Reviewer in deciding whether you would recommend the paper be included for presentation and publication. They are also questions you should ask yourself if submitting your own research as a dissertation or for publication.

**1. What problem with existing algorithms is the new algorithm attempting to solve?**
The algorithm may be directly presented in relation to previous algorithms, or it may be presented as a better solution for a problem in some application domain. In the latter case you may find it helpful to your exposition to give some brief context of the problem or application domain. The main focus, however, should be on the implications for the algorithm.

**2. Why, or in what respect, have previous attempts failed?**
The work will have been done because of a perceived deficiency in previous approaches, or lack of solution to a problem. Your job is to understand and convey the motivation for the work.

**3. What is the new idea presented in this paper?**
How does this paper seek to improve on previous work? What is its novelty?

**4. How is the new approach demonstrated?**
This is the "method" of the paper. Is it demonstrated, for example, by an implementation and experiments, or perhaps by a mathematical proof, or human feedback/surveys from use cases? Does it build on previous work? Is enough information (or references, links) provided that you are confident the results could be replicated?

**5. What are the results or outcomes and how are they validated?**
How are the results validated? Was the approach compared/benchmarked against previous results? Were the comparisons against other "evolutionary" approaches or more "traditional" approaches? Did the results show substantive differences? Were they improvements, or perhaps improvements on some metrics and not others?

**6. What is your assessment of the conclusions?**
Did the authors claim positive results? (Note that negative results can also be useful results.) Do you think they were justified in any claims from the content of the paper? (This may have some bearing on whether you are likely to choose this algorithm for your own experiments.)

### Conclusions (Part 1 Comparative Section)

Having provided a synopsis of each paper individually, provide a brief account (**not more than 1–2 pages**) comparing the selected algorithms. What algorithms did you choose to review and why? Are they variants on a theme, or quite different in nature? Is there a relevant chronology or taxonomy? (A diagram may prove useful in some cases.)

---

# Part II: Experiment — Design and Optimisation of an AI Trading Bot

## 1. Introduction to Technical Analysis

Technical analysis (TA) (sometimes called quantitative analysis) refers to trading strategies that focus on numerical measures, in particular price and volume history, to try to predict future prices — or at least the direction of the market. This contrasts with fundamentals trading that might focus more on broader factors (such as geopolitics and macro factors) and inputs and outputs (such as employment and earnings reports), that are perceived to have an impact on price.

Many (human) traders of stocks, currencies and commodities trade primarily on technical analysis, and are known as *chartists* (or sometimes *quants*). They are also often momentum traders who rely on trends in the data. Fundamentals traders, who often consider themselves to be value traders, on the other hand, sometimes pejoratively liken TA to horoscopes!

The key aspects of technical analysis needed for this assignment follow. You may find it useful to follow the examples at the (free) information website CoinGecko, where you can play around with the technical indicators discussed.

### OHLCV Data

A candlestick chart for BTC/USDT shows one candle per time period (e.g. one day). Each candle encodes:

```
         High ──┐
                │  (thin line = intra-period range)
  Open ─── ┌───┤
           │   │  (thick body = open-to-close range)
  Close ── └───┤
                │
         Low  ──┘

  [volume histogram shown below]
```

This standard representation is known as **OHLCV** data: **O**pen, **H**igh, **L**ow, **C**lose, **V**olume. The same format applies to hourly, daily, weekly candles etc. Reference: CoinGecko → TradingView tab.

### TA Indicators

TA seeks to identify trends, patterns or distinctive features in the historical data that may indicate future price movement. The data generated to represent these patterns are called *(technical) indicators*.

One of the simplest and most widely known indicators is the **simple moving average (SMA)** — a lagging indicator that averages data over a window of elapsed time.

Key observations about SMAs:
- A **shorter window** tracks the price signal more closely but is more erratic (higher frequency response).
- A **longer window** smooths out more small deviations (lower frequency response), but introduces more lag.
- The window size $N$ is a tuning parameter that trades off responsiveness against smoothing.

**Figure 2 (from spec):** Two moving average indicators plotted against BTC price. The green line has a greater delay and more smoothing (lower frequency); the orange line reacts more quickly (higher frequency). Blue crosses mark where buy/sell triggers occur — where the two lines cross.

```
  Price ─────────────────── (noisy)
  Slow MA (green) ────────── (smooth, lags behind)
  Fast MA (orange) ──────── (less smooth, reacts faster)

  Buy  ▲  when fast crosses ABOVE slow  (golden cross)
  Sell ▼  when fast crosses BELOW slow  (death cross)
```

**Trading insight:** The strategy catches uptrends and skips downtrends, but is less effective during sideways ("choppy") markets, especially with transaction costs. The strategy is *parameterised by window sizes* — rather than guessing, we use optimisation.

---

## 2. The Bot Building Blocks

Our bots will be constructed from filter units that implement various **weighted moving averages (WMAs)**, along with simple arithmetic and comparison units.

### 2.1 Weighted Moving Averages

Consider a time series of data points $P = p_0, p_1, p_2, \ldots$ representing (e.g.) daily closing prices.

#### Simple Moving Average (SMA)

The simple moving average at any point $p_n$ is the average of the $N$ data points preceding (and including) $p_n$:

$$\text{SMA}_n = \frac{1}{N} \sum_{k=0}^{N-1} p_{n-k} \tag{1}$$

This is a weighted sum of all data points in a moving "window" of size $N$, with all points given equal weight of 1, normalised by $N$. (Equivalently, a window of $N$ weights each of magnitude $\frac{1}{N}$.)

SMAs are **lagging indicators** — the RHS of the data is aligned with the RHS of the window, so changes appear after they happen. The size of lag increases with window size.

**Convolution implementation:** Rather than evaluating Eq. (1) per point, the SMA can be computed using convolution. Define a "boxcar" filter kernel:

$$K = \frac{1}{N} \cdot \begin{cases} 1 & \text{if } 0 \leq k < N \\ 0 & k \geq N \end{cases} \tag{2}$$

Then:
$$\text{SMA} = P * K \tag{3}$$

$K$ is a **low-pass filter** (kernel): it averages out higher-frequency changes in $P$ while revealing lower-frequency trends.

**Edge padding:** $P$ is undefined prior to $n=0$, so the signal must be padded up to width $N$. The approach used here is to "flip" the first part of the sequence over (rotate 180°), so if the series is rising from $p_0$, it will also be rising into $p_0$.

```python
def pad(P, N):
    padding = -np.flip(P[1:N])
    return np.append(padding, P)

def sma_filter(N):
    return np.ones(N) / N

def wma(P, N, kernel):
    return np.convolve(pad(P, N), kernel, 'valid')
```

To generate an $N$-day SMA: `wma(P, N, sma_filter(N))`

**Filter shape (SMA):** Flat rectangular pulse — all $N$ weights are equal at $\frac{1}{N}$, then drop to zero abruptly.

---

#### Linear-Weighted Moving Average (LMA)

The SMA gives equal weighting to all points in the window then suddenly drops off. The LMA gives higher weighting to more recent points, with weights reducing linearly to zero over the window width. Uses a "triangular" filter:

$$K = \frac{2}{N+1} \cdot \begin{cases} 1 - k\frac{1}{N} & \text{if } 0 \leq k < N \\ 0 & k \geq N \end{cases} \tag{4}$$

The term $\frac{2}{N+1}$ normalises the filter so that weights sum to 1. **Equation (3) does not change** — only the filter kernel swaps out. Implementation requires writing `lma_filter(N)` according to Eq. (4).

**Filter shape (LMA):** Triangular — slopes linearly from maximum at $k=0$ down to near-zero at $k=N-1$.

---

#### Exponential Moving Average (EMA)

The EMA takes the LMA idea further — using exponential rather than linear decay. This gives even greater priority to more recent data points and tails off more gently to zero. Approximated over a fixed-length window:

$$K = \alpha \cdot \begin{cases} (1-\alpha)^k & \text{if } 0 \leq k < N \\ 0 & k \geq N \end{cases} \tag{5}$$

The EMA has **two tuning parameters**: window size $N$, and smoothing factor $\alpha$ which determines the rate of exponential decay. Example: $\alpha = 0.3$.

**Filter shape (EMA):** Exponential decay — high weight at $k=0$, dropping off steeply then tapering toward zero.

---

#### Filter Comparison Summary

```
Filter  | Weighting profile     | Responsiveness  | Smoothing
--------|----------------------|-----------------|----------
SMA     | Flat (equal weights) | Slowest         | Most
LMA     | Linear decay         | Medium          | Medium
EMA     | Exponential decay    | Fastest         | Least
```

> LMA responds more quickly than SMA to changes in signal $p$; EMA responds more quickly than LMA. Conversely, SMA provides the most smoothing of short-term fluctuations.

Each filter's response can be tuned by window length $N$. The EMA has additional parameter $\alpha$. Timeframe (hours, days, weeks, months, years) is also an additional parameter that can be optimised.

**General filter:** One could even use a fully general filter where the weight given to each of the $N$ impulses in the window is a separate free parameter. This would subsume SMA, LMA and EMA as special cases, but at the cost of many more parameters — a classic trade-off between the expressiveness of the hypothesis space and its size/dimension.

---

### 2.2 Crossover Points as Buy and Sell Signals

The vast majority of WMA-based trading strategies use some variation of the **crossover** between a short-term (high-frequency) signal and a longer-term (low-frequency) signal. The idea is that when the short-term signal crosses the long-term signal, it suggests the breaking of a longer-term trend.

| Crossover event | Traditional name | Signal |
|---|---|---|
| Short-term crosses **below** long-term | **Death cross** | **Sell** |
| Short-term crosses **above** long-term | **Golden cross** | **Buy** |

**Two common approaches for choosing the two signals:**

1. Two moving averages of the **same type** but different durations (different $N$), with smaller $N$ being the more responsive.
2. Different WMA types: typically **EMA** for the responsive signal, **SMA** for the smoothed trend signal.

#### Compound Filters

WMAs provide building blocks for designing buy/sell signal functions. Additional "units" can be composed:

- **Subtraction block:** computes the difference between two WMA signals. The difference crosses zero from positive to negative when the short-term average crosses below the long-term average.
- **Sign-change detection filter:** recognises a change in sign of the difference signal by convolving with:

$$K = \frac{1}{2} \cdot \begin{cases} 1 & \text{if } k = 0 \\ -1 & \text{if } k = 1 \\ 0 & k > 1 \end{cases} \tag{6}$$

---

### 2.3 Building a Bot

**Figure 6 (from spec) — Simple trading bot architecture:**

```
                  ┌─────────┐
              ┌──▶│  SMA10  │──┐
              │   └─────────┘  │
P ────────────┤                ├──▶ (−) ──▶ sign ──▶ [change detector] ──▶ >0.5 ──▶ Buy
              │   ┌─────────┐  │                       (Eq. 6 filter)    ──▶ <-0.5──▶ Sell
              └──▶│  SMA20  │──┘
                  └─────────┘
```

The bot: subtracts the 20-day SMA from the 10-day SMA → takes `sign` of result (values: 1, −1, or 0) → convolves with Eq. (6) filter to detect sign changes → outputs Buy (>0.5) or Sell (<−0.5).

**Figure 7 (from spec):** The simple bot operating on the test signal, showing buy (▲ green) and sell (▼ red) signals plotted against price $P$, the 10-day SMA, 20-day SMA, and the difference signal SMA10−SMA40.

#### MACD (More Elaborate Example)

**MACD(12, 26, 9)** — a very widely used trading signal:

```
Step 1:  MACD line   = EMA(12) − EMA(26)         [difference of two EMAs]
Step 2:  Signal line = EMA(9) of MACD line        [EMA of the difference]
Step 3:  Trigger     = crossover of MACD line and Signal line
         (or: zero crossing of MACD line itself)
```

- Crossover → **bullish (buy)** or **bearish (sell)** signal
- The MACD(12,26,9) parameters (12, 26, 9) are themselves candidates for optimisation

All of these bots can be implemented with the WMA convolution tools described above.

---

## 3. The Experiments

### Generalisation and Design

There is no particular reason to believe that SMAs with specific window sizes (e.g. the conventional 12, 26, 9 for MACD) will perform best — these are most commonly people's best "guesstimates". We can generalise by combining different filter types, allowing optimisation to choose how much of each to incorporate.

**Example — Generalised HIGH-frequency component:**

$$\text{HIGH} = \frac{w_1 \cdot \text{SMA}(d_1) + w_2 \cdot \text{LMA}(d_2) + w_3 \cdot \text{EMA}(d_3, \alpha_3)}{\sum_i w_i} \tag{7}$$

where $d_i$ are the durations, $\alpha$ is the EMA decay, and $w_i$ are weights that balance how much attention to give each filter type. By letting $w_i$ "float" freely, the optimisation algorithm chooses how much attention to give each kind of filter based on historical data.

**Optimisation dimensionality:**

| Bot configuration | Parameter vector | Dimensions |
|---|---|---|
| HIGH component only | $[w_1, w_2, w_3, d_1, d_2, d_3, \alpha_3]$ | 7 |
| HIGH + LOW component | Same × 2 | 14 |
| Full MACD (HIGH + LOW + smoothing of difference) | Same × 3 | 21 |

**Further generalisations (optional, increases dimensions):**

- Let each individual WMA weight float freely (subsumes SMA, LMA, EMA as special cases of a general WMA profile)
- Use optimisation to adapt the **bot's topology** itself — which components to use and how they are connected (introduces discontinuities in the evaluation landscape — adding a component may cause a large "jump" in quality)

The sky is the limit — constrained only by imagination and computational cost.

---

### Choosing Algorithms

Once the bot design (hypothesis space) is chosen, we need to select algorithm(s) and an evaluation function.

- **Primary:** Use one or more algorithms from those researched in Part 1.
- **Comparison value:** Trying more than one algorithm allows informed comparison that may elucidate important differences.
- **Extensions:** Additional nature-inspired algorithms may be added if experimentation suggests the original algorithms are lacking.
- All algorithms should be **population-based**.
- **Optional extended comparison:** Include one single-state algorithm from lectures (e.g. direct methods, stochastic/single global optimisation). Compare on a **fixed number of evaluations** (not generations) for a fair comparison.

---

### Evaluation of Bots (Back-Testing)

Bots are evaluated on historical data. Evaluation must be repeatable. Given a period of price data $P_E = p_0, \ldots, p_m$:

| Rule | Detail |
|---|---|
| Starting capital | $1000 USD (zero bitcoin) |
| Buy signal (holding cash) | Trade **all** cash (minus fees) for bitcoin at current price |
| Sell signal (holding bitcoin) | Trade **all** bitcoin for cash (minus fees) at current price |
| Transaction fee | **3% per transaction** |
| End of sequence | Sell any remaining bitcoin at final price |
| **Fitness** | **Cash held at end of evaluation period** |

This approach is known as **back-testing**. Note: success on past data does not guarantee success on future data.

**Multiple evaluation sequences:** You may use a set of sequences $P_E$; fitness = average or total score over the whole set. Any two parameterisations must be compared on **the same set** (deterministic evaluation, not probabilistic batch averaging).

**Timescale:** Up to you (minutes, hours, days). Components of your bot may use different timescales; the timescale itself may be a parameter to optimise over.

---

### Data

**Primary dataset:** Bitcoin Historical Dataset from the Kaggle repository.

| Granularity | Date range | Approx. size |
|---|---|---|
| Daily | 2014–2022 | 2,652 data points |
| Hourly | varies | larger |
| Per-minute (yearly sets) | varies | ~600,000 data points per year |

**Train/test split (mandatory):**
- **Optimise** your agent on data **prior to 2020**
- **Reserve** data **from 2020 onwards** for final testing of your optimised bot (treat as if it is the start of 2020)
- This allows you to evaluate performance on unseen data, simulating forward testing

Alternative real-time data source: Kraken exchange (most exchanges offer free data without sign-up; the `ccxt` library can assist). You may supplement the Kaggle dataset if desired.

---

### "Rules of Engagement"

The primary purpose is **not** to produce the best possible trading bot. Rather, the learning objectives are:

- Understand the "pluggable" components as a language for designing bots
- Use nature-inspired algorithms to generate instances (hypotheses, models) within that language
- Use the algorithms along with an evaluation function, over real-world data, to adaptively improve those models
- Understand and have practical experience with the **trade-off between degrees of freedom** (richness of models, hence existence of better solutions) and the **size of the search space** (consequent difficulty of finding them), and find the right balance through experimentation
- Be able to use an experimental design to assess (through fair comparisons) the algorithms

**Ground rules (strictly enforced):**

| Rule | Detail |
|---|---|
| Bot code | **Must be written by the team** — no code from other sources for the bot or its evaluation |
| Optimisation code | **No general optimisation libraries** or code from other sources |
| Algorithm code from papers | May be adapted, provided the source is **acknowledged** in both written and verbal deliverables |

---

## 4. Deliverables

Part 2 has **three deliverables**: video presentation, report, and code repository.

### Presentation (Video)

**Maximum length: 25 minutes**

Required sections:

| Section | Content |
|---|---|
| **Algorithms investigated** | Short overview of algorithms examined in Part 1 plus any additional ones tested. Categorise them if relevant; point out distinguishing features. Visual aids (table, graph) useful. |
| **Bot design and parameterisation** | Considerations that went into choosing bot configuration and hypothesis space. Discuss iteration across configurations, degrees of freedom, evaluation cost, practicality. What did you try and learn? |
| **Algorithm selection** | Why you chose the algorithms you tested. High-level explanation of how they work (diagrams and/or pseudocode, not actual code). Implementation issues may be discussed. What did you learn from experiments? |
| **Experiments and evaluation** | Your evaluation/testing regime. Discuss trade-offs (e.g. more data = theoretically better results but more expensive). |
| **Results** | Presentation of results. **Visual representations preferred** (images, tables, animations, simulations). |
| **Conclusions** | Conclusions from your work. Remember: this is an open-ended real-world problem; the goal is what you learnt, not whether you "solved" it. |

### Report (Written)

The report should **complement** the video — include extra details that would distract from the video's flow:

- References and links
- Additional results that didn't make the cut in the video
- Diagrams or pseudocode
- **Must not include code** (but may refer to submitted code)

**What to omit from the report:**
- Do not repeat information from the project specification (take it "as read")
- Do not repeat the Part 1 deliverable (refer back to it instead)
- Assume the reader is familiar with algorithmic trading, TA, and the unit's lecture notes
- Include enough introduction for the document to flow, but not a full standalone-paper-style introduction

**Constraints:**
- Maximum **3000 words** (excluding diagrams and references)
- Text beyond the word count will not be marked
- Word count must be included on the title page
- Title page must also include: team number, names and student numbers of all team members
- Submit as **PDF**

### Code

- Submit as a **`.ipynb` (Jupyter Notebook)** file
- Must include all implementation for the project
- Code should allow **reproduction of results**
- Brief instructions for running the code may be included in a **README**
- Code is not marked per se, but results must be repeatable if required

---

## 5. Practicalities

### Working as a Team

- **Maximum 4 members** per team (group number will be assigned)
- How well the team works together can be as much a factor in success as the technical aspects
- **Planning:** Meet early; plan tasks, time allocations, and initial responsibilities (revisit as difficulty becomes clearer)
- **Communications:** Decide upfront how the team will communicate both in-person (meeting frequency) and electronically; regular communication keeps everyone on the same page and lets emerging difficulties be addressed early

### Submissions

- Report: **PDF file**
- Video: **MP4 format** (unless otherwise arranged) OR a link to a streaming service (YouTube) or shared Google Drive folder with permissions set to "Anyone with the link can view" — link can be included in the report
- Referencing: **IEEE style**
- All materials from other sources must be referenced
- Group work declaration: submitting constitutes a declaration that the work is entirely the team's own except as referenced
- Only **one group member** needs to make the submission

### Deadlines

| Deliverable | Deadline |
|---|---|
| **Deliverable 1** (Part 1 synopses) | Friday 24th April, 11:59pm AWST |
| **Deliverable 2** (Part 2: presentation, report, code) | Sunday 24th May, 11:59pm AWST |

**Late submission penalty:**

| Timing | Penalty |
|---|---|
| Within 48 hours (Days 1–2) | **Waiver** — marked as late but no penalty applied |
| Day 3 (after 48 hours) | 15% deduction (accrued) |
| Days 4–7 | Additional 5% per day |
| After Day 7 | Assignment **not accepted** |

The penalty is 5% of the total mark allocated per day for the first 7 days (including weekends and public holidays).

---

## References

[^1]: A. Tzanetos, I. Fister and G. Dounias, "A comprehensive database of Nature-Inspired Algorithms", *Data in Brief*, vol. 31, 2020, https://doi.org/10.1016/j.dib.2020.105792

[^2]: A. Tzanetos, "Nature-Inspired Algorithm", Mendeley Data, V2, January 14, 2021, doi: 10.17632/xfnzd2c8v7.2

[^3]: Hadi Bayzidi, Siamak Talatahari, Meysam Saraee, Charles-Philippe Lamarche, "Social Network Search for Solving Engineering Optimization Problems", *Computational Intelligence and Neuroscience*, Wiley, September 2021.

[^4]: K. V. Price, N. H. Awad, M. Z. Ali and P. N. Suganthan, "The 2019 100-Digit Challenge on Real-Parameter, Single Objective Optimization: Analysis of Results", available on GitHub.

---

## Quick Reference Summary

### All Equations

| # | Equation | Description |
|---|---|---|
| (1) | $\text{SMA}_n = \frac{1}{N}\sum_{k=0}^{N-1} p_{n-k}$ | Simple Moving Average |
| (2) | $K = \frac{1}{N} \cdot \begin{cases}1 & 0 \leq k < N \\ 0 & k \geq N\end{cases}$ | SMA (boxcar) filter kernel |
| (3) | $\text{SMA} = P * K$ | SMA via convolution |
| (4) | $K = \frac{2}{N+1} \cdot \begin{cases}1 - k\frac{1}{N} & 0 \leq k < N \\ 0 & k \geq N\end{cases}$ | LMA (triangular) filter kernel |
| (5) | $K = \alpha \cdot \begin{cases}(1-\alpha)^k & 0 \leq k < N \\ 0 & k \geq N\end{cases}$ | EMA (exponential decay) filter kernel |
| (6) | $K = \frac{1}{2} \cdot \begin{cases}1 & k=0 \\ -1 & k=1 \\ 0 & k>1\end{cases}$ | Sign-change detection filter |
| (7) | $\text{HIGH} = \frac{w_1 \text{SMA}(d_1) + w_2 \text{LMA}(d_2) + w_3 \text{EMA}(d_3,\alpha_3)}{\sum_i w_i}$ | Generalised composite high-frequency component |

### Optimisation Parameter Vectors

| Scope | Parameters | Dimensions |
|---|---|---|
| One composite component | $[w_1, w_2, w_3, d_1, d_2, d_3, \alpha_3]$ | 7 |
| Two components (HIGH + LOW) | Above × 2 | 14 |
| Three components (MACD-style) | Above × 3 | 21 |

### Bot Evaluation Rules (Summary)

- Start: $1000 USD, 0 BTC
- Buy signal: trade all cash → BTC (−3% fee)
- Sell signal: trade all BTC → cash (−3% fee)
- End: liquidate remaining BTC at final price
- Fitness = final cash value
- Train on data **before 2020**; test on data **from 2020 onwards**