---
title: "StatSUM"
author: "Geert Müller"
date: "`r Sys.Date()`"
output: pdf_document
---

# Mixed Effects Models

## Linear Mixed-Effects Models
* Can handle non-independence of data
  * Are called *mixed effects* because they contains *fixed* and *random* effects, of which the latter are those that handle the non-independency of data.
    * Have many other names
    
### Fixed Effects
* Fixed intercepts and fixed slopes
* Capture the $\bar{x}$ effects
  * Typically test statistical significance for the fixed effects: "does a new treatment **on average** increase happiness significantly over time, compared to the controls?

(Time * Condition 
1 + Time * Condition)

### Random Effects
* Capture the **variability**: "participants' deviations from the average effects".
Since each participant contributed more than one data point:
* Data will be more similar to each other than data from other individuals
  * If not taken into account, this will result in an inflated **Type 1 Error** for the **fixed effects** (standard error and p-value would be too small).
* Typically we **do not** care about the significance of the random effects.
  
#### Three Types of Random Effects

* Random intercepts
* Random slopes
* Covariances between random effects (**random correlations**)

#### Preview about model syntax
The main package used is **lme4**. This is what the model would look like: 
```{r, eval=FALSE}
m1 <- lmer(Happiness ~ 1 + Time * Condition) + (1 + Time | pp_code), data = mydata)
```
#### Typical sources of non-independence
* Repeated-measures data
  * **>1** data point per subject
    * Grouping factor ("cluster"): *participant*
  * Traditional approaches to deal with such data:
    * Repeated-measures ANOVA
    * Aggregate observations within participants, until there's only 1 observation per participant (linear regression).
* Longitudinal data
  * Also repeated measures
  * Each participant is observed repeatedly over time
    * Grouping factor ("cluster"): *participant*
  * Time itself is a variable of interest
* Nested aka. hierarchical data
  * **Not** repeated measures; but specific data structures
  * Students are **nested** in classes
    * Grouping factor ("cluster"): *class*
- Sources are **not** mutually exclusive

#### Disadvantages of aggregation
**Traditional analysis of non-independent data**
* Repeated-measures ANOVA
  * Nothing wrong with that, but rather restricted
  * Cannot handle continuous predictors well
  * Balanced factorial designs required
  * Doesn't handle missing data well
  * Often necessary to aggregate data
    * Potential problems with aggregation
      * Loses information
      
#### Advantages of Mixed Models
* No aggregation needed
  * No unwanted loss of information
* Information at the trial-level can be taken into account

Sure — here’s the exact same outline, but with lettered subpoints (a, b, c, …) replaced by numeric sub-numbering (1, 2, 3, …). Content is unchanged.  ￼

I. Course start-up and organization
A. How the class is run
1. Interactive format: students should interrupt when something is unclear or the pace is too fast.
2. Course structure for today
2.1. Introductions and how the course works
2.2. First exposure to linear mixed-effects models (LMEMs)
2.3. Step back to a very simple model + basic formulas
2.4. Homework / lab session instructions
B. Logistics
1. Lecture: 10:30–12:15 (MM 03.610).
2. Lab session: 13:30–15:15 (MM 02.110), one time slot.
3. TA: Marta Gomez Vargas.
4. Web lecture recordings available.
C. Brightspace use
1. Materials posted and continuously updated (slides, recordings, homework, example solutions, R scripts, literature/resources).
2. Discussion board threads
2.1. Administrative questions.
2.2. Content-related mixed-model / R questions (students encouraged to answer each other as well).

II. Assessment and ground rules
A. Grades
1. Multiple-choice exam (March 30): 80% (around 50 questions; more info later).
2. Homework assignments (7 total): 20%
2.1. Upload to Pitch2Peer portal.
2.2. Peer-grading: review another student’s homework by a deadline.
2.3. Feedback should be informative (not just “could be better”; point out what and where).
3. Brightspace participation can yield a bonus for active engagement.
B. Minimum requirements and retake rules
1. Each grading component must be at least 5.5.
2. If you fail the multiple-choice exam: second opportunity, maximum grade 10.
3. If you passed the take-home exam, you cannot do the retake.
4. If fewer than 4 of 7 homework assignments are passed: chance to resubmit failed ones; maximum grade 6.
C. Collaboration and plagiarism boundaries
1. Working together is allowed/encouraged, but do not copy/paste each other’s work.
2. Do not copy/paste from previous years or example solutions.
3. Do not share your solutions or the instructor’s example solutions (now or in the future).

III. Course goals and prerequisites
A. Learning objectives (what you should be able to do after the course)
1. Apply linear mixed-effects modeling to research questions.
2. Recognize, evaluate, and interpret parameter estimates.
3. Judge appropriateness of mixed models in published literature.
4. Describe theoretical underpinnings (but course emphasizes application over heavy math).
5. Use these methods in later research and report results in scientific articles.
B. Practical skills focus
1. Use LMEMs in R.
2. Decide when they are appropriate/inappropriate.
3. Prepare data, troubleshoot/diagnose models, interpret/report (text + figures).
C. Prerequisites
1. Familiarity with R/RStudio.
2. Basic + somewhat advanced stats: linear and logistic regression (lm(), glm(), brms::brm()).

IV. Why mixed-effects models? (motivation and big picture)
A. Why this course / why LMEMs
1. Relatively recent methods, now widely used across many fields.
2. Core idea: “like regression, but for non-independent data.”
3. Works for Gaussian and also other outcome types later (binary, counts, ordinal, etc.).
4. Often fewer restrictions than some traditional approaches (e.g., repeated-measures ANOVA).
5. Enables more flexible study designs and often more appropriate analyses.
B. Reality check about learning and the field
1. Basic idea is simple, but correct use requires time and practice.
2. Mixed models remain an active research area.
3. R is highly up-to-date for mixed modeling: new developments get incorporated quickly.
4. Downsides: textbooks become outdated fast; experts sometimes disagree; some parts can be complicated.
C. Main goal for today
1. First grasp of what mixed models are and what they are for.
2. Overview of components: intercepts/slopes; fixed/random effects.
3. Then “step back” to the simplest possible model and build up over weeks.

V. First exposure via a realistic example (happiness treatment over time)
A. Study setup
1. Research question: a new treatment claims to improve happiness across several weeks.
2. Data: 6 participants measured at baseline (time 0) and weeks 1–4.
3. Conditions: 3 treatment, 3 control (sham).
4. Key question: does treatment improve happiness over time relative to control? (Condition × Time interaction).
B. The central problem: non-independence
1. Repeated observations within a person are more similar to each other than observations across people.
2. Individuals differ in intercepts (starting levels) and slopes (change over time).
C. Why not plain regression?
1. A regression like lm(Happiness ~ Time * Condition) assumes independent data points.
2. Violating independence inflates Type I error for fixed effects because standard errors and p-values become too small.
3. Mixed models address this by explicitly modeling the non-independence.

VI. What “mixed” means: fixed effects + random effects
A. Fixed effects (what you already know from regression)
1. Fixed intercept: overall average baseline (depending on coding/centering).
2. Fixed slopes: average effects of predictors.
3. Example fixed-effects structure for the happiness study
3.1. Main effect of Time.
3.2. Main effect of Condition.
3.3. Interaction Time × Condition (the main research focus).
3.4. In R formula terms: 1 + Time * Condition (where * expands to main effects + interaction).
B. Random effects (what handles non-independence)
1. Purpose: account for clustering (e.g., multiple rows per participant).
2. Prevents incorrect inference on fixed effects by correcting SEs/p-values.
3. Three random-effect components introduced
3.1. Random intercepts (participants differ in baseline levels).
3.2. Random slopes (participants differ in effects like Time).
3.3. Covariance between random effects (a “random correlation,” e.g., intercept–slope association).
4. Typical interpretation
4.1. Fixed effects = “average” pattern across participants (usually what you test).
4.2. Random effects = variability around that average (often not the main inferential target).

VII. Preview of model syntax in R (lme4 / lmer)
A. Core function and package
1. Main package: lme4.
2. Main fitting function: lmer().
B. Example model from the happiness study
1. m1 <- lmer(Happiness ~ 1 + Time * Condition + (1 + Time | pp_code), data = mydata)
C. How to read this formula
1. DV: Happiness.
2. Fixed-effects part: 1 + Time * Condition
2.1. Intercept is included by default (unless specified otherwise, e.g., 0 + …).
3. Random-effects term: (1 + Time | pp_code)
3.1. Grouping factor after “|”: pp_code (participant), the source of non-independence.
3.2. “1” on the left: random intercept per participant.
3.3. “Time” on the left: random slope of Time per participant.
3.4. Default: includes covariance between random intercept and random slope (unless you specify otherwise).

VIII. What kinds of data call for mixed models? (“Grouped” / “clustered” data)
A. Definition and common sources of non-independence
1. Non-independent (clustered/grouped) observations: DV rows are not independent.
2. Typical sources
2.1. Repeated-measures data.
2.2. Longitudinal data.
2.3. Nested / hierarchical data.
2.4. Other sources (e.g., non-independence induced by stimuli; mentioned as later topic).
B. Repeated measures
1. Each participant contributes more than one observation (from 2 to many).
2. Traditional approaches
2.1. Repeated-measures ANOVA.
2.2. Aggregation to one score per person (then regression), which can throw away information.
C. Longitudinal data
1. A special case of repeated measures where time is central.
2. Example: symptom development over years as a function of early attachment, changing relationship quality, etc.
3. Also called growth-curve modeling.
D. Nested/hierarchical data (not necessarily repeated measures)
1. Example: students nested in classes (shared teacher influences).
2. Multiple nesting levels can occur (classes in schools in districts, etc.).
3. Another example: patients nested within therapists.
E. Combinations are possible
1. E.g., longitudinal data with students nested in classes/schools, plus repeated-measures tasks each year.

IX. Advantages of mixed models over traditional approaches (and why aggregation can be problematic)
A. Limitations of repeated-measures ANOVA (as presented here)
1. Continuous predictors handled poorly (often forced categorization).
2. Balanced factorial designs often required.
3. Missing data handled poorly (participant-wise deletion).
4. No general “ANOVA” family for different DV types (binary/proportions/counts).
5. Often pushes researchers to aggregate trial-level data → loss of information.
B. Why aggregation can lose information (Stroop-style examples)
1. Unequal accuracy across participants: aggregating RTs of correct trials can ignore important differences (and can give equal weight despite very different error rates).
2. Different within-person variability can be hidden when only means are used.
3. Learning/fatigue over trials: continuous trial index is ideal, but ANOVA often forces block categorization.
C. Mixed model advantages
1. No need to aggregate (though you can if you want).
2. Can use trial-level information
2.1. Participants with more observations can contribute more information (“more weight”).
2.2. Less noisy participants can effectively contribute more precise information.
3. Supports continuous and categorical predictors.
4. Can model more relevant processes when appropriate.
5. Handles (to a point) unbalanced designs, missing data (row-wise removal rather than dropping an entire participant), and avoids the sphericity assumption; some approaches can address heteroscedasticity.
6. Can handle multiple nesting and crossed/partially crossed random effects (e.g., participant and item).
7. Sometimes better power without inflating Type I error.

X. The cost: increased complexity
A. Estimation and practical challenges
1. No simple closed-form “formula-based” solution like in t-tests/ANOVA/regression.
2. Uses numeric iterative estimation (can take time).
3. Convergence or singularity warnings can occur → requires careful checking and sometimes model adjustments.
4. Mathematical details can be hard.
B. Field maturity and disagreement
1. Methods are relatively new and still developing.
2. Experts may disagree; different “schools of thought.”
3. “Best practices” not always fully settled; lab SOPs exist as guidance (mentioned in slides).

XI. Step back to basics: regression recap + simplest mixed model (intercept-only)
A. Linear regression recap
1. Predict one dependent variable using one or more predictors.
2. Linear relationship represented as a straight line.
3. Key components
3.1. b0 (intercept): expected Y when X = 0.
3.2. b1 (slope/coefficient): direction and strength of relation.
3.3. εi (error): observed minus predicted.
B. Intercept-only mixed model example (cherry pit spitting contest)
1. Data structure
1.1. 5 participants.
1.2. 5 trials each (5 cherries), distance in meters → 25 observations.
1.3. “Multilevel” framing
1.3.1. Level 1 = trial-level observations.
1.3.2. Level 2 = participant-level (trials nested in participants).
2. Notation introduced
2.1. Yij: observation i (trial) from participant j.
2.2. b0j: participant-specific intercept (participant mean; interpretation depends on coding/centering).
2.3. εij: trial-level deviation from that participant mean, assumed Normal with mean 0 and variance σ².
3. Second-level (participant-level) formula idea
3.1. b0: overall intercept (often grand mean; depends on coding/centering) = fixed intercept.
3.2. uj: participant deviation from the grand mean = random intercept.
3.3. uj assumed Normal with mean 0 and variance estimated from the data.
4. “Put together” conceptual decomposition
4.1. Fixed effect: b0 (overall average).
4.2. Random effect: uj (how participant j differs from overall average).
4.3. Residual: εij (trial-to-trial deviation around participant j’s mean).
5. Note about notation
5.1. Different authors write this differently, but the idea is the same.

XII. Tools and next steps
A. Installing/using software
1. Install lme4 (and optionally a very recent version via the provided repository approach).
2. Other packages mentioned as also used later: lattice, car, boot, pbkrtest, ggplot2, psych, afex, brms.
B. General lmer template
1. MyModel <- lmer(DV ~ 1 + IV1 + IV2 + (1 + IV1 | GroupingFactor), data = MyData)
2. New element vs lm(): the ( … | … ) term specifies random effects
2.1. Right side of “|” = grouping factor.
2.2. Left side of “|” = random intercept and/or random slopes.
2.3. Random-effects structure can vary in complexity (more next week).
C. Preview topic for next class
1. Quantifying non-independence: ICC (intra-class / intra-cluster correlation) — sometimes useful, often not; covered next week.