# Cleaner Hospitals vs. Better Rehab: What Actually Gets Patients Home?
### A data-driven look at what separates top-performing long-term care hospitals from the rest

---

When a seriously ill patient enters a long-term care hospital (LTCH), 
the goal is simple: get them well enough to go home. But across hundreds 
of U.S. hospitals treating the same types of patients, outcomes vary 
dramatically. Some hospitals consistently send patients home. Others do not.

What makes the difference?

Is it cleaner wards with fewer infections? Lower costs? Better 
physiotherapy? Using data from 290 U.S. long-term care hospitals, 
this analysis set out to find the answer.

---

## The Questions

- **Q1:** What clinical factors separate high-performing hospitals from low-performing ones?
- **Q2:** Can a hospital's discharge performance be predicted from its quality metrics alone?
- **Q3:** Which factors matter most for that prediction?
- **Q4:** If a struggling hospital invests in improvement — what actually changes its outcome?

---

## What the Data Shows

### Q1: The Surprising Gap Between Infections and Outcomes

The 290 hospitals in this dataset are rated by the Centers for Medicare 
& Medicaid Services (CMS) into three groups based on how many of their 
patients are successfully discharged home:

| Performance | Hospitals | Share |
|---|---|---|
| 🟢 Better than National Rate | 28 | 9.7% |
| 🔵 Average | 222 | 76.6% |
| 🔴 Worse than National Rate | 40 | 13.8% |

When comparing the clinical profiles of these three groups, 
a clear and surprising pattern emerges:

| Metric | 🟢 Better | 🔵 Average | 🔴 Worse |
|---|---|---|---|
| Cost Efficiency (MSPB) | **0.93** | 0.99 | 1.04 |
| Mobility Improvement Score | **8.78** | 6.93 | 5.70 |
| Readmission Rate (RSRR) | **21.3%** | 22.5% | 23.3% |
| Infection Rate (CAUTI SIR) | 0.54 | 0.70 | **0.82** |

The top-performing hospitals are more cost-efficient and achieve 
stronger mobility improvements. But infection rates? 
**The differences are small and inconsistent across groups.**

> 💡 *The hospitals that send the most patients home are not necessarily 
> the ones with the lowest infection rates — they are the ones that get 
> patients moving again.*

---

### Q2: Can Performance Be Predicted?

Yes — with meaningful accuracy. A predictive model trained exclusively 
on quality metrics (infection rates, readmission rates, cost efficiency, 
and mobility scores) was able to classify hospital performance 
significantly better than random chance.

Importantly, when the model was tested with and without rehabilitation 
and cost metrics, performance dropped sharply without them — confirming 
that these dimensions carry the most predictive signal.

---

### Q3: Which Factors Matter Most?

When the model ranks which metrics are most useful for predicting 
whether a hospital performs Better, Average, or Worse, the results 
are consistent with what the data showed in Q1:

| Rank | Factor | Importance |
|---|---|---|
| 🥇 1 | Cost Efficiency (MSPB Score) | Highest |
| 🥈 2 | Mobility Improvement Score | High |
| 🥉 3 | Readmission Rate | Moderate |
| 4 | Infection Rates (CAUTI, MRSA, CLABSI) | Low |

**Infection control ranks at the bottom.** Despite being one of the 
most visible and widely reported hospital quality metrics, it contributes 
the least to predicting whether patients go home.

---

### Q4: What Actually Changes a Hospital's Outcome?

To answer this directly, a struggling hospital (*"Midwest General LTCH"*) 
was simulated — currently rated *Worse than the National Rate* — 
and two improvement strategies were tested step by step:

#### Strategy 1: Invest in Rehabilitation (Mobility Score)

| Mobility Score | Performance Prediction |
|---|---|
| 4.0 *(starting point)* | 🔴 Worse |
| 4.5 | 🔵 Average ← **first flip** |
| 7.5 | 🟢 Better ← **second flip** |
| 10.0 | 🟢 Better (57% confidence) |

A **minimal improvement** of just 0.5 points in the mobility score 
was enough to shift the prediction from *Worse* to *Average*. 
Reaching *Better* required a score of 7.5 — still below the 
Better-class average of 8.78.

#### Strategy 2: Invest in Infection Control (Infection Rates)

| Infection Rate (CAUTI SIR) | Performance Prediction |
|---|---|
| 2.0 *(starting point)* | 🔴 Worse |
| 1.5 | 🔴 Worse |
| 1.0 *(national average)* | 🔴 Worse |
| 0.4 *(best in class)* | 🔴 Worse |

**No improvement was observed — at any level.**
Reducing infection rates from worst to best in class 
produced zero prediction flips. 
The hospital remained *Worse* throughout.

> 💡 *A tiny improvement in rehabilitation flipped the outcome twice. 
> A full reduction of infection rates to best-in-class levels 
> changed nothing.*

---

## What This Analysis Cannot Tell Us

Every data analysis has boundaries — and being transparent about them 
is just as important as the findings themselves.

**The hospitals in this dataset are not all equal in size**
Larger hospitals treat more patients, which naturally affects their 
infection counts, costs, and readmission numbers. While rate-based 
metrics partially account for this, size differences may still 
influence the results in ways that are difficult to fully separate.

**The factors measured are not independent of each other**
Infection rates, readmission rates, and costs do not exist in isolation. 
A patient who develops an infection during their stay is more likely to 
be readmitted — which in turn increases costs. The model treats each 
factor as if it were independent, which means the indirect effect of 
infection control may be larger than the model suggests.

**The simulation changes one thing at a time — the real world does not**
In practice, a hospital that invests in rehabilitation does not just 
improve its mobility score — it likely also reduces readmissions and 
lowers costs as patients recover faster. The true benefit of investing 
in rehabilitation is probably even greater than the simulation shows.

**The dataset is relatively small**
With only 290 hospitals — of which just 28 are classified as *Better* 
and 40 as *Worse* — the model is learning from a limited number of 
examples. Results could shift with a larger or more recent dataset.

**Cost efficiency may partly reflect outcomes rather than cause them**
The MSPB Score measures total Medicare spending including costs incurred 
in the 30 days *after* a patient leaves the hospital. A hospital that 
successfully discharges patients home will automatically tend to have 
lower post-discharge costs. Lower costs may therefore be a *consequence* 
of good discharge performance — not just a cause of it.

---

## The Bottom Line

Three separate analyses — comparing class profiles, ranking predictors, 
and simulating improvements — all point to the same conclusion:

> **Getting patients home from a long-term care hospital is driven by 
> rehabilitation and cost efficiency. Infection control, despite its 
> prominence in hospital quality reporting, plays a surprisingly small role.**

For hospital leaders and policymakers, the implication is direct:

- **Prioritise early mobilisation and physiotherapy programmes**
- **Monitor cost efficiency as a system-level quality signal**
- **Recognise that infection metrics alone are not a reliable proxy 
  for overall discharge performance**

This does not mean infection control is unimportant — reducing infections 
matters for patient safety and wellbeing. But if the goal is to get more 
patients home, the data points clearly elsewhere.

---

*Data source: Centers for Medicare & Medicaid Services (CMS), 
LTCH Quality Reporting Program. 290 hospitals included in analysis.
Full technical methodology available on [GitHub](https://github.com/Alexlab2525/Data-Science-Udacity).*
