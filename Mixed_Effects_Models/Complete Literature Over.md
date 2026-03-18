# File: README.md
# Description: This is the master study guide for the Mixed Effects Models course. It provides a detailed, step-by-step statistical framework based on the 7 "Typical Research Steps" from the 2026 curriculum. Updated with vivid imagery, hypothetical studies, and conceptual evolution.

# 🎓 Mixed Effects Models (MEM): The Master Framework
> **Conceptual Summary:** MEM is the senior sibling of standard regression. While standard regression assumes all data points are independent (like 100 different people), MEM handles "clumpy" data (like 10 people measured 10 times). By splitting effects into **Fixed** (average pattern) and **Random** (individual deviation), we generalise our results from a specific sample to the entire population without inflating our error rates.

---

## 🏗️ The Statistical Roadmap: "The 7 Steps"

```mermaid
graph LR
    S1["1. Prepsteps<br/>Centring & Coding"]
    S2["2. Visualisation<br/>Wave & Windows"]
    S3["3. Specification<br/>Fixed vs. Random"]
    S4["4. Model Fitting<br/>lmer vs. brm"]
    S5["5. Diagnostics<br/>Residuals"]
    S6["6. Inference<br/>p-values & CIs"]
    S7["7. Refinement<br/>Post-hocs"]

    S1 --> S2 --> S3 --> S4 --> S5 --> S6 --> S7

    classDef purple fill:#f3e5f5,stroke:#7b1fa2,stroke-width:2px,rx:5,ry:5,color:#4a148c;
    class S1,S2,S3,S4,S5,S6,S7 purple
```

---

## 📅 The Conceptual Evolution (Week-by-Week)

### 🟢 Week 1: The Foundation (Non-independence)
*   **The Problem:** Standard $t$-tests and regressions assume every observation is independent. If you have 6 participants each measured 4 times (the **"Happiness Treatment"** study), you don't have $N=24$; you have 6 individuals. 
*   **The Danger:** Treating $N=24$ as independent is "cheating." It makes your standard errors too small and your $p$-values too significant (Inflated **Type 1 Error**).
*   **The Add:** MEM solves this by allowing each participant to have their own "baseline" (Random Intercept).

### 🟢 Week 2: The Workflow (The "Prepsteps")
*   **The Problem:** Raw data is often uninterpretable. If "Trial" ranges from 1 to 5 (the **"Cherry Pit Spitting"** study), the intercept represents "Trial 0," which doesn't exist.
*   **The Add:** **Centring** trial so that 0 represents the middle of the experiment. Learning to use **Sum-to-zero coding** so that main effects are tested against the grand mean, not just a baseline group.

### 🟢 Week 3 & 4: Inferential Precision
*   **The Problem:** Standard $p$-values are often biased in small samples. The "Wald Test" (standard in many packages) is notoriously unreliable for MEM.
*   **The Add:** Introduction of **Kenward-Roger (KR)** corrections—a "shield" that adjusts degrees of freedom to protect against false positives. We also learn to compare models using **Likelihood Ratio Tests (LRT)**.

### 🟢 Week 5: Interactions & Follow-ups
*   **The Problem:** An interaction like `Gender * Trial` is just the start. If significant, how do we know *where* the difference is?
*   **The Add:** Using `emmeans` for pairwise comparisons (The **"Politeness Data"** study). We also learn to run **Follow-up** models (e.g., testing the trial effect for females and males separately) to untangle the interaction.

### 🟢 Week 6: The "Maximal" Reality
*   **The Problem:** We are told to "keep it maximal" (Barr et al., 2013), but real data often crashes (`Singularity` warnings).
*   **The Add:** Dealing with the **"AAT" (Approach-Avoidance)** data. Learning **Principled Pruning**: removing random correlations first (`||` syntax), and only then simplifying slopes that the data cannot support.

### 🟢 Week 7: Complex Architectures
*   **The Problem:** Sometimes subjects aren't the only thing that's random. In the **"School23"** or **"Honeymoon"** studies, we have students nested in schools, or participants responding to specific stimuli (Items).
*   **The Add:** **Crossed Random Effects.** Modelling both "Who" (Participants) and "What" (Items/Stimuli) simultaneously to truly generalise to the population.

---

## 🖼️ Visual Imagery & Plot Mnemonics

### 🌊 1. The Wave (Density Plot)
*   **Description:** A smooth, flowing curve showing the distribution of your data.
*   **Look for:** Is the wave skewed? Does it have a "long tail" (typical for reaction times)?
```text
      _
     / \
   _/   \__
__/        \__
```

### 🪟 2. The Windows (Lattice/Individual Plots)
*   **Description:** Small, separate panels for every single participant.
*   **Look for:** "The Outlier." Does one window look completely different from the others (e.g., a flat line while others go up)?
```text
[ . ] [ . ] [ . ]
[ / ] [ \ ] [ . ]
```

### 📏 3. The Diagonal (Q-Q Plot)
*   **Description:** Dots lining up on a straight, 45-degree path.
*   **Look for:** "The Deviation." If the dots snake away from the line at the ends, your data isn't normally distributed.
```text
      / .
     / .
   ./
 ./
```

### ☁️ 4. The Cloud (Residual Plot)
*   **Description:** A patternless cluster of points scattered like a thin cloud.
*   **Look for:** "The Funnel." If the cloud gets wider or narrower at one end, you have heteroscedasticity (a violation of assumptions).
```text
 .  .   .  .
   .  .   .
 .   .  .  .
```

---

## 📄 Formulating Fixed vs. Random: The Rules

| Effect Type | Rule for Selection | Study Example |
| :--- | :--- | :--- |
| **Fixed ($\beta$)** | Levels represent **all possible values** or are **directly manipulated**. | **Gender** (M/F), **Treatment** (Drug/Sham). |
| **Random ($u$)** | Levels are a **random subset** of a larger population. | **Participants** (pid), **Stimuli** (item_id). |
| **Random Slope** | Add if the predictor varies **within** the grouping factor. | **Trial** varies within Participant. |

---

## 📄 Sums of Squares (SS): Type 1, 2, and 3
*Source: Week 5, Slide 65; Week 4 Example Script*

*   **Type 1 (Sequential):** Order matters. Adding `Gender` then `Trial` gives different results than `Trial` then `Gender`. Rarely used in MEM.
*   **Type 2 (Hierarchical):** Tests main effects *before* interactions. Good for balanced designs.
*   **Type 3 (Simultaneous):** **The Course Default.** Tests each effect against all others simultaneously. 
    *   *Context:* Essential for unbalanced real-world data. 
    *   *Warning:* Only accurate if you use **Sum-to-zero coding** (`contr.sum`)!

---

## 🔗 How to use this guide with LLMs
To test your understanding, paste this guide into an LLM and ask:
1.  *"Using the 'Cherry Pit' example, explain why centring trial is a critical prepstep."*
2.  *"I have a singularity warning in my AAT model. Based on 'Principled Pruning', what should my first three steps be?"*
3.  *"Explain the difference between Type 2 and Type 3 SS using the 'Happiness' study as a context."*
