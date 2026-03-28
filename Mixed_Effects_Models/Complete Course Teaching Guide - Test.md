# Mixed Effect Models Master Study Guide

Status:
- Updated March 28, 2026

## Table Of Contents

- [1. The Big Picture](#1-the-big-picture)
- [2. Anatomy Of Mixed-Model Formulas](#2-anatomy-of-mixed-model-formulas)
  - [Formula Ladder](#formula-ladder)
  - [The Master Teaching Equation](#the-master-teaching-equation)
  - [R Syntax Rosetta Stone](#r-syntax-rosetta-stone)
  - [Formula Decryption Worked Examples](#formula-decryption-worked-examples)
- [3. Statistical Workflow Step By Step](#3-statistical-workflow-step-by-step)
  - [Study-Design To Model Recipe](#study-design-to-model-recipe)
- [4. Core Concepts From The Syllabus](#4-core-concepts-from-the-syllabus)
  - [4.1 Why Mixed Models](#41-why-mixed-models)
  - [4.2 Minimum Ingredients Of A Mixed-Effects Model](#42-minimum-ingredients-of-a-mixed-effects-model)
  - [4.3 Fixed Versus Random Effects](#43-fixed-versus-random-effects)
  - [4.4 Random Intercepts](#44-random-intercepts)
    - [Formula Decryption](#formula-decryption)
  - [4.5 Random Slopes](#45-random-slopes)
    - [Formula Decryption](#formula-decryption-1)
  - [4.6 Interaction Logic](#46-interaction-logic)
  - [4.7 Crossed Versus Nested Structures](#47-crossed-versus-nested-structures)
  - [4.8 Output Interpretation](#48-output-interpretation)
  - [4.9 Type 2 Versus Type 3 Tests](#49-type-2-versus-type-3-tests)
  - [4.10 Maximal Models](#410-maximal-models)
    - [Design-To-Model Decryption](#design-to-model-decryption)
  - [4.11 Syntax Decoding](#411-syntax-decoding)
    - [Full Formula Decryption](#full-formula-decryption)
  - [4.12 Contrast Coding](#412-contrast-coding)
  - [4.13 Post-Hocs And Follow-Up Models](#413-post-hocs-and-follow-up-models)
  - [4.14 Convergence Versus Singularity](#414-convergence-versus-singularity)
  - [4.15 Diagnostics](#415-diagnostics)
  - [4.16 Longitudinal Models](#416-longitudinal-models)
  - [4.17 Design-Driven Versus Data-Driven Analysis](#417-design-driven-versus-data-driven-analysis)
- [5. GLMMs And Non-Gaussian Outcomes](#5-glmms-and-non-gaussian-outcomes)
  - [5.1 Why GLMMs Are Needed](#51-why-glmms-are-needed)
  - [5.2 Binary Responses](#52-binary-responses)
  - [5.3 Aggregated Binary Responses And Proportions](#53-aggregated-binary-responses-and-proportions)
  - [5.4 Ordinal Outcomes](#54-ordinal-outcomes)
  - [5.5 What Changes For Diagnostics And P Values In GLMMs](#55-what-changes-for-diagnostics-and-p-values-in-glmms)
- [6. Exam Traps And Fast Distinctions](#6-exam-traps-and-fast-distinctions)
  - [6.1 Fast Exam Checklist](#61-fast-exam-checklist)
  - [6.2 High-Yield Distinctions](#62-high-yield-distinctions)
- [7. Quick Reference Tables](#7-quick-reference-tables)
  - [7.1 Formula-To-English Table](#71-formula-to-english-table)
  - [7.2 Syntax-To-Meaning Table](#72-syntax-to-meaning-table)
  - [7.3 Output-Reading Table](#73-output-reading-table)
  - [7.4 Method-Selection Table](#74-method-selection-table)
  - [7.5 Warning-Handling Table](#75-warning-handling-table)
  - [7.6 DV-Type Routing Table](#76-dv-type-routing-table)
- [Glossary](#glossary)

## 1. The Big Picture

### Why This Matters

If you do not understand why mixed models exist, the later syntax will look arbitrary.
This course is built around one central idea:
- behavioural-science data are often clustered
- clustered data violate independence
- mixed models let us analyse that structure without throwing away trial-level information

<details>
<summary>Source</summary>
<ul>
<li>Syllabus, Objectives</li>
<li>Example exam questions, opening instructions</li>
<li>Lecture slides, Week 2, slide 6</li>
<li>Syllabus, Course description</li>
</ul>
</details>

### The Core Problem

In ordinary regression thinking, each row is treated as if it were fully independent.
In this course, that assumption often fails because:

- the same participant contributes multiple observations
- the same item or stimulus is reused
- the data are nested in classes, schools, clinics, or other groups
- the data are collected across time within person

When those observations are treated as independent anyway, the model can become too confident.
That is why the course keeps returning to:
- non-independence
- clustered errors
- inflated Type 1 errors

### The Big-Picture Formula

At the most general level, the course wants you to think like this:

```text
Outcome = average structure + group-specific variation + residual noise
```

The simple version of that idea in mixed-model notation is:

$$
Y_{ij} = \beta_{0} + \beta_{1} X_{ij} + u_{0j} + e_{ij}
$$

This is not yet the only formula you need, but it captures the central leap:
- there is an average pattern in the population
- there is also variation across people, items, or other groups
- and there is still trial-level noise left over



### How Mixed Models Extend Older Approaches

Mixed models should be understood as the bridge between:
- the formula logic of regression
- the design logic of repeated-measures or grouped data

Ordinary regression already gives you:
- an outcome
- predictors
- an intercept
- slopes

Mixed models add:
- random intercepts
- random slopes
- grouping structure

So the course is not saying "forget regression."
It is saying:
- keep regression logic
- stop pretending clustered observations are independent

### What The Course Wants You To Be Able To Do

By the end of the course, you should be able to:
- recognize when a mixed model is appropriate
- read and write the model formula
- decide which random effects are justified
- choose or interpret the testing workflow
- read the output
- judge whether a paper uses the model appropriately
- move to GLMM logic when the dependent variable is not Gaussian

### What To Remember

- Mixed models exist because behavioural data are often not independent.
- They keep trial-level or grouped data instead of collapsing everything prematurely.
- They extend regression rather than replacing it.
- The whole course is about learning how to connect data structure, model structure, and interpretation.



## 2. Anatomy Of Mixed-Model Formulas: The Basics

### Why This Matters

If you can decode the formula, you can usually decode the model.
This section is the translation layer between:

- the conceptual statistics
- the model equation
- the R syntax
- the output

<details>
<summary>Source</summary>
<ul>
<li>Bodo tutorial 1, pp. 1-3</li>
<li>Bodo tutorial 2, pp. 2-3</li>
<li>Lecture slides, Week 2, slides 26-28</li>
<li>Lecture slides, Week 3, slide 45</li>
</ul>
</details>

### Formula Ladder

The course really teaches a ladder of formulas:

```text
pitch ~ sex
```

This is the simplest regression idea:
- one outcome
- one predictor

```text
pitch ~ politeness + sex + e
```

Now you have:
- one outcome
- two fixed effects
- an error term

```text
distance ~ 1 + (1 | pid)
```

Now the model becomes mixed:
- fixed intercept
- random intercept varying across participant

```text
Reaction ~ 1 + Days + (1 + Days | f_Subject)
```

Now you have:
- fixed intercept
- fixed slope for `Days`
- random intercept by subject
- random slope for `Days` by subject
- estimated correlation between those random coefficients; this is automatically estimated by R because the random intercept and random slope are inside the same `( ... | f_Subject )` term

### The Master Teaching Equation

For most of the course, this is the most useful conceptual equation:

$$
Y_{ij} = \beta_{0} + \beta_{1} X_{ij} + u_{0j} + u_{1j} X_{ij} + e_{ij}
$$

<details>
<summary>Source</summary>
<ul>
<li>Bodo tutorial 1, pp. 1-3</li>
<li>Bodo tutorial 2, pp. 2-3 and 15-16</li>
<li>Lecture slides, Week 2, slides 26-28</li>
<li>Lecture slides, Week 3, slide 45</li>
</ul>
</details>

### What Each Symbol Means

| Symbol | Meaning |
| --- | --- |
| $Y_{ij}$ | outcome for observation `i` inside unit `j` |
| $\beta_{0}$ | fixed intercept, the average baseline |
| $\beta_{1}$ | fixed slope, the average effect of predictor $X$ |
| $X_{ij}$ | predictor value for observation `i` in unit `j` |
| $u_{0j}$ | random intercept deviation for unit `j` |
| $u_{1j}$ | random slope deviation for unit `j` |
| $e_{ij}$ | residual error for that specific observation |

Key subscript rule used throughout the guide:
- $i$ = lower-level observation within a unit, such as one trial or one row of data for that unit
- $j$ = higher-level unit or cluster, such as one participant, item, class, clinic, or judge
- $t$ = time index in the longitudinal chapter
- symbol with only $j$ = unit-level quantity
- symbol with $ij$ = observation-level quantity inside unit $j$

### Plain-English Meaning

This equation says:
- there is an overall average starting point ($\beta_{0}$)
- there is an overall average effect of the predictor ($\beta_{1} X_{ij}$)
- each unit can start a bit higher or lower than average ($u_{0j}$)
- each unit can respond a bit more strongly or weakly to the predictor ($u_{1j} X_{ij}$)
- even after all that, some observation-level noise remains ($e_{ij}$)

So mixed models are not mysterious.
They are just models that split variation into:
- average structure ($\beta$ terms)
- group-specific structure (`u` terms)
- leftover noise ($e_{ij}$)

### R Syntax Rosetta Stone

| Syntax | Plain-English Meaning |
| --- | --- |
| `~` | is predicted by |
| `1` | intercept |
| `+` | add another term |
| `*` | main effects plus interaction |
| `:` | interaction only |
| `|` | what varies on the left, who varies on the right |
| `||` | same random coefficients, but without estimating their correlation |
| `(1 | group)` | varying baseline across the grouping factor |
| `(1 + X | group)` | varying baseline and varying effect of `X` |
| `(0 + X | group)` | slope of `X` without an intercept in that random term |

### How The Statistical Formula Maps To R

Conceptual equation:

$$
Y_{ij} = \beta_{0} + \beta_{1} X_{ij} + u_{0j} + e_{ij}
$$

R syntax:

```r
lmer(Y ~ 1 + X + (1 | group), data = d)
```

Conceptual equation with random slope:

$$
Y_{ij} = \beta_{0} + \beta_{1} X_{ij} + u_{0j} + u_{1j} X_{ij} + e_{ij}
$$

R syntax:

```r
lmer(Y ~ 1 + X + (1 + X | group), data = d)
```

<details>
<summary>Source</summary>
<ul>
<li>Bodo tutorial 1, pp. 1-3</li>
<li>Bodo tutorial 2, pp. 2-3 and 15-16</li>
<li>Lecture slides, Week 2, slides 26-28</li>
<li>Lecture slides, Week 3, slide 45</li>
</ul>
</details>

### Formula Decryption Worked Examples

For:

```r
lmer(distance ~ 1 + (1 | pid), data = dfcp)
```

decrypt it like this:
- dependent variable: `distance`
- fixed intercept: the `1` after `~`
- fixed slopes: none, because no predictor appears after the intercept
- random intercept: the `1` inside `(1 | pid)`
- random slopes: none
- grouping factor: `pid`
- residual: not written in the R formula, but still estimated by the Gaussian mixed model
- `data = dfcp`: tells R where the variables come from; it is not a model term

So the sentence version is:
- predict `distance`
- estimate one average baseline
- let each participant have a different baseline
- keep residual observation-level noise

For:

```r
lmer(Reaction ~ 1 + Days + (1 + Days | f_Subject), data = sleepstudy2)
```

decrypt it like this:
- dependent variable: `Reaction`
- fixed intercept: the `1` after `~`
- fixed slope: `Days` in the fixed part
- random intercept: the `1` inside `(1 + Days | f_Subject)`
- random slope: `Days` inside `(1 + Days | f_Subject)`
- grouping factor: `f_Subject`
- random correlation term: implied because the random intercept and random slope are estimated together inside the same `|` term
- action status for the correlation term: automatically estimated by R; no extra action is needed unless you intentionally remove it with `||` or split the random terms apart
- residual: not written in the R formula, but still estimated by the Gaussian mixed model
- `data = sleepstudy2`: tells R where the variables come from; it is not a model term

So the sentence version is:
- predict `Reaction`
- estimate one average intercept
- estimate one average effect of `Days`
- let each subject have a different baseline
- let each subject have a different `Days` effect
- estimate the correlation between those subject-specific intercepts and slopes
- keep residual observation-level noise

### Hidden Terms That Are Still Estimated

Some model components are real even when they are not written as separate visible terms in the R formula:
- residual variance: automatically estimated in Gaussian LMMs; no extra action is needed
- intercept-slope correlation: automatically estimated when intercept and slope appear together inside the same `( ... | group )` term
- no intercept-slope correlation: if you use `||` or split the random terms, R does not estimate that correlation
- in GLMMs, there is no ordinary Gaussian residual term written in the same way as $e_{ij}$; outcome variability is handled through the model family and link

### How To Read These Formulas In Output

The course expects you to connect syntax to output structure:

- the fixed part of the formula appears in the `Fixed effects` section
- the random part appears in the `Random effects` section
- the grouping factor appears in the `Groups` column
- the residual is reported separately from the random effects

So, for:

```r
lmer(distance ~ 1 + (1 | pid), data = dfcp)
```

you should expect:
- one fixed intercept
- one participant-level random-intercept variance
- one residual variance

For:

```r
lmer(Reaction ~ 1 + Days + (1 + Days | f_Subject), data = sleepstudy2)
```

you should expect:
- fixed intercept
- fixed `Days` slope
- subject random-intercept variance
- subject random-slope variance for `Days`
- correlation between random intercept and random slope
  this is automatically estimated because both random coefficients are inside the same `(1 + Days | f_Subject)` term
- residual variance

### Common Formula Traps

- `1` does not mean "no fixed effect"; it means intercept.
- `(1 | group)` is not the same as adding `group` as a fixed predictor.
- `X * Z` expands to `X + Z + X:Z`.
- `||` does not remove the slope; it removes the estimated random correlation.
- The right side of `|` is the grouping factor, not another predictor of interest.

### What To Memorize

- `~` means "predicted by."
- `1` means intercept.
- left of `|` = random coefficients.
- right of `|` = grouping factor.
- `(1 | group)` = varying baseline.
- `(1 + X | group)` = varying baseline and varying effect of `X`.
- `X * Z` means main effects plus interaction.

## 3. Statistical Workflow Step By Step

<details>
<summary>Open Statistical Workflow</summary>
### Why This Matters

Your current summaries extract concepts, but a study guide also has to teach you what to do in order.
That is what this workflow section fixes.

### The Workflow At A Glance

1. define the statistical question
2. identify the dependent-variable type
3. identify the dependence structure
4. identify grouping factors
5. choose fixed effects
6. choose random intercepts
7. choose random slopes
8. choose coding and inference method
9. fit the model
10. read the output
11. diagnose the model
12. handle warnings if needed
13. do follow-up tests if needed
14. report the result

### Step 1. Start With The Research Question

Ask:
- what do I want to explain or predict?
- what is my dependent variable?
- what effect or interaction do I actually care about?

If you cannot answer that first, the rest of the model will be vague.

### Step 2. Identify The Dependent-Variable Type

This is the first branching point.

If the DV is approximately continuous and Gaussian:
- stay on the LMM path

If the DV is binary, aggregated binary, ordinal, or another non-Gaussian type:
- move to the GLMM path

Core rule:

```text
continuous Gaussian DV -> lmer-style logic
non-Gaussian DV -> glmer / clmm / other generalized logic
```

Week 8 makes this explicit because the model family and link function become part of the modeling decision.

### Step 3. Identify Non-Independence

Ask:
- are there repeated observations per participant?
- are the same items reused?
- are people nested in classes, schools, clinics, herds, or time points?

If yes, ordinary independent-observation modeling is not enough.
This is the point where you justify using a mixed model at all.

### Step 4. Identify The Grouping Factors

Ask:
- who or what is contributing repeated observations?
- over which unit do I expect baseline differences?

Typical grouping factors in the course:
- participant
- item or stimulus
- class
- school
- herd
- judge

The grouping factor becomes the right-hand side of the random-effects term:

```r
(1 | participant)
(1 | item)
(1 | school/class)
```

### Step 5. Choose The Fixed Effects

These are the predictors whose average effects you want to estimate or test.

Examples:
- treatment or condition
- time
- gender
- attitude
- interactions among these

Start by writing the fixed part of the model in plain regression style:

```text
DV ~ 1 + A + B + A:B
```

Only after that do you ask how the random structure should be added.

### Step 6. Choose Random Intercepts

For each grouping factor, ask:
- do I expect the baseline level of the outcome to differ across these units?

If yes, add a random intercept.

Examples:

```r
(1 | pid)
(1 | subject)
(1 | item)
```

This is the first correction for clustered data.

### Step 7. Choose Random Slopes

Now ask the most important design question:
- which fixed effects vary within each grouping factor?

If a predictor varies within a grouping factor, and the design gives enough replication, that predictor often needs a matching random slope.

Core rule:

```text
within-unit fixed effect -> candidate random slope
between-unit fixed effect -> often not a random slope for that grouping factor
```

For interactions:
- apply the same logic to the interaction
- if the interaction is fully within-unit, it often needs a matching random slope

### Study-Design To Model Recipe

If you want to recognize what is necessary from a study design, use this order:
- dependent variable: what is being predicted?
- fixed effects: which predictors or conditions answer the research question?
- grouping factors: which units contribute repeated or clustered observations?
- random intercepts: which grouping factors need different baselines?
- random slopes: which fixed effects vary within each grouping factor?

Translate design features directly:
- same participant contributes multiple rows -> participant is a grouping factor -> candidate random intercept for participant
- same item or stimulus is reused -> item is a grouping factor -> candidate random intercept for item
- predictor changes within participant -> predictor is a fixed effect and a candidate random slope for participant
- predictor does not change within participant -> predictor can still be a fixed effect, but is usually not a random slope for participant
- two grouping factors recur across each other -> crossed structure -> separate random terms for each grouping factor
- one grouping factor lives inside another -> nested structure -> nested random structure
- interaction is fully within a grouping factor -> candidate random slope for that interaction
- only one observation per cell per unit -> some slopes or covariance terms may not be estimable even if the design would otherwise justify them

Quick recognition rule:
- fixed effect = average effect you want to estimate
- random effect = allowed variation around that average due to clustering or repeated measurement

### Step 8. Choose Coding And Inference Method

Before fitting, ask:
- do I have interactions?
- will I need Type 2 or Type 3 logic?
- does contrast coding matter here?

For the Week 4 style workflow:
- Type 2 and Type 3 differ only when interactions are present
- Type 3 requires appropriate coding

For LMMs, the course uses tools such as:
- `anova`
- `Anova`
- `PBmodcomp`
- `KRmodcomp`
- `afex::mixed`

For GLMMs, the course warns that KR-style F-tests do not carry over in the same way.

### Step 9. Fit The Model

Once the structure is justified, fit the model that matches:
- the DV type
- the fixed-effect structure
- the random-effect structure

Examples:

```r
lmer(distance ~ 1 + gender + (1 | pid), data = dfcp)
```

```r
lmer(Reaction ~ 1 + Days + (1 + Days | f_Subject), data = sleepstudy2)
```

```r
glmer(choice_SS0_LL1 ~ 1 + f_Now_Notnow + c_TimeDiff + c_rel_diff_Amounts +
      (1 + f_Now_Notnow + c_TimeDiff + c_rel_diff_Amounts | pp_code_ITC),
      family = binomial(link = "logit"), data = itc4)
```

### Step 10. Read The Output

Always read output in this order:
1. formula line
2. random-effects block
3. fixed-effects block
4. number of observations and groups
5. test output or confidence intervals

Do not jump straight to p-values.
First confirm that the fitted model is actually the model you meant to fit.

### Step 11. Diagnose The Model

Check:
- plots
- summary output
- residual patterns
- fitted-versus-observed patterns
- influential cases

For later weeks, diagnostics expand to:
- Cook's distance
- influence tools
- more formal residual checks

### Step 12. Handle Warnings If Needed

If warnings appear, do not panic and do not simplify immediately.

The course's order is:
1. check whether the model is conceptually misspecified
2. check centering, scaling, factor coding, and grouping variables
3. try optimizer or iteration changes
4. compare estimates across optimizers
5. compare with brms if needed
6. only then simplify the random-effects structure

Core distinction:
- convergence and singularity are not the same thing

### Step 13. Do Follow-Up Tests Only If Needed

After the main model:
- compute p-values or confidence intervals with the appropriate method
- do post-hocs or follow-up models only if the result structure calls for them
- do not mechanically run post-hocs just because software can

### Step 14. Report The Result

A complete mixed-model report needs:
- the model
- the testing method
- the substantive result
- text plus figures when appropriate

In plain language:
- what was modeled
- how it was tested
- what was found
- how that result should be interpreted

### Design-Driven Versus Data-Driven Branch

This is the final workflow warning.

If you are doing confirmatory testing:
- decide the model structure from the design and hypotheses as much as possible

If you are doing data-driven model search:
- the final model is better treated as an exploratory result
- do not pretend it emerged from a purely confirmatory pipeline

### What To Memorize

- first decide the question, then the DV type, then the dependence structure
- grouping factors come from who or what is repeated
- fixed effects are the effects of interest
- random intercepts and slopes come from the design
- method choice and coding matter for inference
- output reading comes before significance interpretation
- diagnostics and warnings are part of the workflow, not an afterthought

</details>

<details>
<summary>Source</summary>
<ul>
<li>Lecture slides, Week 6, slide 30</li>
<li>Lecture slides, Week 7, slide 70</li>
<li>Lecture slides, Week 8, slide 9</li>
</ul>
</details>

<details>
<summary>Source: Study-Design To Model Recipe</summary>
<ul>
<li>Lecture slides, Week 5, slides 47-56</li>
<li>Lecture slides, Week 6, slides 37 and 40</li>
<li>Lecture slides, Week 7, slides 42-44 and 62</li>
<li>Barr, Levy, Scheepers, and Tily (2013)</li>
</ul>
</details>

## 4. Core Concepts From The Syllabus

### 4.1 Why Mixed Models

#### Why This Matters

This is the first question the course keeps asking in different forms:
- why not just use ordinary regression or ANOVA?
- what is the actual statistical problem?
- what extra job does a mixed model do?

If you cannot answer that, later formula choices will feel arbitrary.
In the workflow, this is the point where you decide whether the dependence structure and grouping factors actually require a mixed model.

#### Statistical Formula

Ordinary linear-model logic:

$$
Y_{ij} = \beta_{0} + \beta_{1} X_{ij} + e_{ij}
$$

Mixed-model logic:

$$
Y_{ij} = \beta_{0} + \beta_{1} X_{ij} + u_{0j} + e_{ij}
$$

#### What Each Symbol Means

<details>
<summary>Open Symbol Meanings</summary>

- $Y_{ij}$: the outcome for observation `i` in unit `j`
- $\beta_{0}$: the average intercept in the population
- $\beta_{1}$: the average slope for predictor $X$
- $X_{ij}$: the predictor value for that observation
- $u_{0j}$: the group-specific deviation from the average intercept
- $e_{ij}$: residual observation-level noise

</details>

#### Plain-English Meaning

The ordinary model assumes one common baseline and one common slope, with all leftover variation pushed into the residual.
The mixed model adds one crucial idea:
- some variation is not just random noise
- some variation comes from the fact that observations belong to participants, items, classes, clinics, or other clusters

So the mixed model separates:
- average population structure
- cluster-specific structure
- leftover noise


#### Book / Literature Explanation

The book-style explanation is that mixed models are not "just regression with more terms."
They are models for data that vary at more than one level.
Baguley's key bridge is that they extend both regression and repeated-measures ANOVA by explicitly modeling variation at different levels of the data.

That means the question is not only:
- does $X$ predict $Y$?

It is also:
- do some participants start higher than others?
- do some items produce larger responses than others?
- do some participants respond more strongly to $X$ than others?

#### Equivalent R Syntax

Ordinary model:

```r
lm(Y ~ 1 + X, data = d)
```

Mixed model:

```r
lmer(Y ~ 1 + X + (1 | group), data = d)
```

#### How To Read It In Output

The ordinary model mainly gives:
- fixed coefficients
- one residual error structure

The mixed model adds:
- a `Random effects` block
- variance for the grouping factor
- residual variance separate from the grouping-factor variance

#### Common Trap

- Using mixed models because they feel more advanced, instead of because the data structure requires them.
- Thinking the main reason is "big data" rather than clustered or repeated data.

#### What To Memorize

- Mixed models exist because observations are often not independent.
- Their extra job is to model structured variation across clusters.
- They extend regression and repeated-measures logic rather than replacing them.

### 4.2 Minimum Ingredients Of A Mixed-Effects Model

#### Why This Matters


The example exam directly asks what counts as a mixed-effects model.
So you need one stable rule that works even when the formula looks simple.
In the workflow, this is the smallest defensible mixed model once you have established non-independence and identified a grouping factor.

#### Statistical Formula

The smallest clean mixed-model example in this course is:

$$
Y_{ij} = \beta_{0} + u_{0j} + e_{ij}
$$

#### What Each Symbol Means

<details>
<summary>Open Symbol Meanings</summary>

- $\beta_{0}$: the fixed intercept, the average baseline
- $u_{0j}$: the random intercept for unit `j`
- $e_{ij}$: residual error for observation `i` in unit `j`

</details>

#### Plain-English Meaning

Even this simple model is already mixed because it contains:
- a fixed part: the average intercept
- a random part: group-specific deviations from that intercept

So a mixed model is defined by structure, not by visual complexity.


#### Book / Literature Explanation


The teaching point here is subtle but important.
A mixed model does not need:
- many predictors
- an interaction
- a random slope
- multiple grouping factors

It only needs:
- fixed structure
- random structure

That is why an intercept-only model with a random intercept is still a real mixed model.

#### Equivalent R Syntax

```r
lmer(distance ~ 1 + (1 | pid), data = dfcp)
```

#### How To Read It In Output


For this minimal model you should expect:
- a fixed intercept estimate
- a variance for the grouping factor
- a residual variance

That is enough to call the model mixed.

#### Common Trap


- Thinking a model is only mixed if it has both random intercepts and random slopes.
- Thinking an intercept-only mixed model is "empty."

#### What To Memorize


- Minimum ingredients = fixed part + random part.
- Complexity is optional; mixed structure is not.
- `lmer(Y ~ 1 + (1 | group), data = d)` is already a mixed model.

### 4.3 Fixed Versus Random Effects

#### Why This Matters


This distinction controls the entire formula.
If you confuse fixed and random effects, you will misread both syntax and output.
In the workflow, this is the distinction you use when deciding which effects belong in the fixed part and which sampled units belong in the random part.

#### Statistical Formula

$$
Y_{ij} = \beta_{0} + \beta_{1} X_{ij} + u_{0j} + e_{ij}
$$

$$
u_{0j} \sim N(0, \sigma^2_{u})
$$

$$
e_{ij} \sim N(0, \sigma^2_{e})
$$

#### What Each Symbol Means

<details>
<summary>Open Symbol Meanings</summary>

- $\beta_{0}$, $\beta_{1}$: fixed effects, single average coefficients for the population-level relationship
- $u_{0j}$: random effect, a unit-specific deviation drawn from a distribution
- $\sigma^2_{u}$: variance of the random intercepts across units
- $e_{ij}$: residual error for each observation
- $\sigma^2_{e}$: residual variance

</details>

#### Plain-English Meaning

Fixed effects answer:
- what is the average effect we care about?

Random effects answer:
- how much do sampled units differ around that average?

So the core distinction is:
- fixed effects are the systematic effects of interest
- random effects are distributions of deviations tied to grouping units

<details>
<summary>Source</summary>
<ul>
<li>Lecture slides, Week 5, slides 31-35</li>
</ul>
</details>

#### Book / Literature Explanation


This is where the book-like explanation helps most.
Fixed effects are not called "fixed" because they never change in the sample.
They are fixed because the model estimates one population-level coefficient for them.
Random effects are not random because they are unimportant.
They are random because the model treats the observed levels as sampled from a broader population of possible units and models their variability as a distribution.

That is why the course keeps emphasizing generalization.
If subjects, items, clinics, or classes are sampled sources of variability, the model should usually treat them as random.

#### Equivalent R Syntax

```r
lmer(Y ~ 1 + treatment + (1 | subject), data = d)
```

In this example:
- `treatment` is a fixed effect
- `subject` is a grouping factor in the random part

#### How To Read It In Output


Look in different places for different jobs:
- `Fixed effects` block: coefficient estimates for effects of interest
- `Random effects` block: variance and standard deviation for grouping-factor deviations
- `Groups` column: tells you which sampled units those deviations belong to

#### Common Trap


- Treating any variable with many levels as automatically random.
- Confusing crossed versus nested with fixed versus random.

#### What To Memorize


- Fixed effects = average effects of interest.
- Random effects = distributions of unit-level deviations.
- Fixed effects are typically tested directly; random effects mainly structure the model.

### 4.4 Random Intercepts

#### Why This Matters


Random intercepts are the first real random effect in the course.
If you understand them properly, the rest of the random-effects logic becomes much easier.
This is still a random-intercept chapter: even if a fixed predictor is added, only the intercept varies across units here.
#### Statistical Formula

Intercept-only random-intercept model:

$$
Y_{ij} = \beta_{0} + u_{0j} + e_{ij}
$$

Random-intercept model with a fixed predictor in the fixed-effects part:

$$
Y_{ij} = \beta_{0} + \beta_{1} X_{ij} + u_{0j} + e_{ij}
$$

<details>
<summary>Source</summary>
<ul>
<li>Lecture slides, Week 2, slides 27-28</li>
<li>Bodo tutorial 2, pp. 2-3</li>
</ul>
</details>

#### What Each Symbol Means

<details>
<summary>Open Symbol Meanings</summary>

- $\beta_{0}$: average intercept across all units
- $\beta_{1}$: average effect of predictor `X`; this is the fixed predictor here, so the model estimates one population-level slope for `X`
- $u_{0j}$: how much unit `j` starts above or below the average intercept; `j` indexes the higher-level unit or cluster
- $e_{ij}$: leftover observation-level noise for observation `i` within unit `j`; `i` indexes the lower-level observation

</details>

#### Plain-English Meaning

A random intercept lets each unit have its own baseline.
That means:
- one overall average baseline ($\beta_{0}$)
- some participants are generally higher than others ($u_{0j}$ for participants)
- some items are generally easier or harder than others ($u_{0j}$ for items)
- some classes or clinics start from different average levels ($u_{0j}$ for those clusters)
- leftover observation-level noise remains ($e_{ij}$)

The model still estimates one overall intercept, but each unit is allowed to deviate from it.


#### Book / Literature Explanation


This is the cleanest example of the course's phrase "model variation at different levels."
The fixed intercept captures the average baseline in the population.
The random intercept captures how clusters depart from that average.

So the model is no longer forced to pretend that every participant or item begins from exactly the same starting point.

#### Equivalent R Syntax

```r
lmer(distance ~ 1 + (1 | pid), data = dfcp)
```

```r
lmer(Y ~ 1 + X + (1 | subject), data = d)
```

<details>
<summary>Source</summary>
<ul>
<li>Lecture slides, Week 2, slides 27-28</li>
<li>Bodo tutorial 2, pp. 2-3</li>
</ul>
</details>

#### Formula Decryption


For:

```r
lmer(distance ~ 1 + (1 | pid), data = dfcp)
```

read it term by term:
- fixed intercept: the `1` after `~`
- fixed slopes: none
- random intercept: the `1` inside `(1 | pid)`
- grouping factor: `pid`
- random correlation term: none, because only a random intercept is estimated here
- residual: still present even though it is not written explicitly in the R formula

This means:
- one average baseline for `distance` ($\beta_{0}$)
- different participant-specific baselines around that average ($u_{0j}$)
- leftover residual noise for each observation ($e_{ij}$)

#### How To Read It In Output


In the output, look for:
- the grouping factor under `Groups`
- the random-intercept variance for that grouping factor
- the residual variance
- the fixed intercept estimate

Interpretation rule:
- fixed intercept = average baseline
- random-intercept variance = how much baselines vary across units

#### Common Trap


- Thinking `(1 | group)` means `group` is just another fixed predictor.
- Thinking a random intercept already captures differences in the effect of `X`.

#### What To Memorize


- Random intercept = varying baseline.
- `(1 | group)` = allow the intercept to differ across the grouping factor.
- A random intercept fixes baseline non-independence, not slope heterogeneity.

### 4.5 Random Slopes

#### Why This Matters


This is where the course becomes design-sensitive.
Random slopes are the answer to the question:
- does the effect of the predictor differ across units?
In the workflow, this is the point where you ask which fixed effects vary within each grouping factor.

#### Statistical Formula

$$
Y_{ij} = \beta_{0} + \beta_{1} X_{ij} + u_{0j} + u_{1j} X_{ij} + e_{ij}
$$

#### What Each Symbol Means

<details>
<summary>Open Symbol Meanings</summary>

- $\beta_{0}$: average intercept
- $\beta_{1}$: average effect of predictor `X`; this is the fixed-effect slope shared on average across units
- $u_{0j}$: unit-specific deviation in the intercept; `j` indexes the higher-level unit or cluster
- $u_{1j}$: unit-specific deviation in the slope for `X`
- $u_{1j} X_{ij}$: the part that lets the effect of `X` differ by unit; `i` indexes the lower-level observation within unit `j`
- $e_{ij}$: leftover noise after accounting for fixed and random structure at observation `i` in unit `j`

</details>

#### Plain-English Meaning

A random slope says that units do not all respond to the predictor in the same way.
So instead of assuming one identical effect of `X` for everyone, the model allows:
- one average effect of `X` across all units ($\beta_{1}$)
- some participants to show a stronger effect ($u_{1j} X_{ij}$ in the positive direction)
- some to show a weaker effect ($u_{1j} X_{ij}$ in the negative direction)
- some perhaps almost no effect at all (a near-zero unit-specific slope deviation)
- leftover observation-level noise ($e_{ij}$)

This is often essential in repeated-measures designs.

<details>
<summary>Source</summary>
<ul>
<li>Lecture slides, Week 3, slides 28 and 46</li>
<li>Bodo tutorial 2, pp. 15-16</li>
</ul>
</details>

#### Book / Literature Explanation


The fixed slope answers the average question:
- on average, does `X` change `Y`?

The random slope answers the heterogeneity question:
- does that effect vary across participants, items, or other clusters?

This is why the course repeatedly warns that a random-intercept-only model can be too optimistic.
If units truly differ in slopes, omitting the slope forces the model to act as if everyone shares the same effect size.

#### Equivalent R Syntax

```r
lmer(Reaction ~ 1 + Days + (1 + Days | f_Subject), data = sleepstudy2)
```

<details>
<summary>Source</summary>
<ul>
<li>Lecture slides, Week 3, slides 28 and 46</li>
<li>Bodo tutorial 2, pp. 15-16</li>
</ul>
</details>

#### Formula Decryption


For:

```r
lmer(Reaction ~ 1 + Days + (1 + Days | f_Subject), data = sleepstudy2)
```

read it term by term:
- dependent variable: `Reaction`
- fixed intercept: the `1` after `~`
- fixed slope: `Days` in the fixed part
- random intercept: the `1` inside `(1 + Days | f_Subject)`
- random slope: `Days` inside `(1 + Days | f_Subject)`
- grouping factor: `f_Subject`
- random correlation term: implied because intercept and slope are estimated together inside the same random-effects term
- action status for the correlation term: automatically estimated by R; no extra action is needed unless you replace `|` with `||` or separate the random terms
- residual: still present even though it is not written explicitly in the R formula

This means:
- one average baseline reaction time ($\beta_{0}$)
- one average effect of `Days` ($\beta_{1}$)
- subject-specific baselines ($u_{0j}$)
- subject-specific `Days` effects ($u_{1j} X_{ij}$)
- correlation between those subject-specific baselines and slopes (automatically estimated)
- leftover residual noise ($e_{ij}$)

#### How To Read It In Output


For a random-slope model, expect to see:
- a random-intercept variance
- a random-slope variance
- often a correlation between intercept and slope
- the fixed slope estimate for the average effect

Interpretation rule:
- fixed slope = average effect of the predictor
- random-slope variance = how much that effect differs across units

#### Common Trap


- Assuming the fixed slope already captures participant-to-participant variability in the effect.
- Adding or removing random slopes without checking whether the design justifies them.

#### What To Memorize


- Random slope = varying effect of a predictor across units.
- `(1 + X | group)` = varying baseline and varying effect of `X`.
- Omitting a needed random slope can inflate Type 1 error for the corresponding fixed effect.

### 4.6 Interaction Logic

#### Why This Matters


An interaction is where the effect of one predictor depends on the level of another predictor.
In this course, interaction logic matters twice:
- in the fixed-effects interpretation
- in the random-effects design rule
In the workflow, this matters when you choose both the fixed-effects structure and the justified random slopes for models with interactions.

#### Statistical Formula

Fixed-effects interaction:

$$
Y_{ij} = \beta_{0} + \beta_{1} A_{ij} + \beta_{2} B_{ij} + \beta_{3} A_{ij} B_{ij} + e_{ij}
$$

Mixed-model interaction idea:

$$
Y_{ij} = \beta_{0} + \beta_{1} A_{ij} + \beta_{2} B_{ij} + \beta_{3} A_{ij} B_{ij} + u_{0j} + ... + e_{ij}
$$

<details>
<summary>Source</summary>
<ul>
<li>Lecture slides, Week 3</li>
<li>Barr (2013)</li>
<li>Lecture slides, Week 5</li>
</ul>
</details>

#### What Each Symbol Means

<details>
<summary>Open Symbol Meanings</summary>

- $\beta_{1}$: main effect of `A`
- $\beta_{2}$: main effect of `B`
- $\beta_{3}$: interaction effect, meaning the effect of one predictor changes depending on the other
- $u_{0j}$: group-specific deviation in baseline
- additional random terms may be needed depending on whether `A`, `B`, or `A:B` vary within the grouping factor

</details>

#### Plain-English Meaning

If there is no interaction, the effect of `A` is the same at every level of `B`, and vice versa.
If there is an interaction, the effect of `A` changes when `B` changes, or the effect of `B` changes when `A` changes.

In mixed models, that does not only affect interpretation.
It also affects which random slopes are justified.

#### Book / Literature Explanation


The main teaching point is that interaction logic is design-dependent.
You do not ask only:
- is there an `A:B` term in the fixed part?

You also ask:
- do both factors vary within subject?
- does only one vary within subject?
- is there enough replication to estimate the needed slope?

So the course's interaction rule is not a software trick.
It is a design rule about what pattern of variation the model should allow.

#### Equivalent R Syntax

If both `A` and `B` vary within subject and the design supports it:

```r
lmer(Y ~ 1 + A * B + (1 + A * B | subject), data = d)
```

If `A` is between subject and `B` is within subject:

```r
lmer(Y ~ 1 + A * B + (1 + B | subject), data = d)
```

#### How To Read It In Output


For an interaction model, look for:
- fixed estimates for `A`, `B`, and `A:B`
- the relevant random-slope variances for the within-unit effects
- whether the model actually contains the slope structure that the design calls for

Interpretation rule:
- the interaction estimate tells you whether one effect changes across levels of the other predictor

#### Common Trap


- Treating interactions as only a fixed-effects issue.
- Forgetting that the random-effects structure for an interaction depends on which factors are within-unit.

#### What To Memorize


- Interaction = effect of one predictor depends on another predictor.
- The interaction term itself is in the fixed part.
- The needed random slope depends on the design, not just on the presence of `A:B` in the formula.

### 4.7 Crossed Versus Nested Structures

#### Why This Matters


The course uses both repeated-measures subject-item examples and hierarchical examples such as students in classes.
You need to tell these structures apart because the formula changes with the data structure.
In the workflow, this matters when you identify the dependence structure and grouping factors, because getting crossed versus nested wrong changes the formula itself.

#### Statistical Formula

Crossed structure:

$$
Y_{ijk} = \beta_{0} + \beta_{1} X_{ijk} + u_{0j} + v_{0k} + e_{ijk}
$$

Nested structure:

$$
Y_{ijk} = \beta_{0} + \beta_{1} X_{ijk} + u_{0k} + v_{0jk} + e_{ijk}
$$

#### What Each Symbol Means

<details>
<summary>Open Symbol Meanings</summary>

In the crossed example:
- $u_{0j}$: subject-specific baseline
- $v_{0k}$: item-specific baseline
- the same subjects combine with the same items across the design

In the nested example:
- $u_{0k}$: school-specific baseline
- $v_{0jk}$: class-specific baseline within school
- the lower-level unit exists inside the higher-level unit

</details>

#### Plain-English Meaning

Crossed means two sources of grouping combine across each other.
The classic psychology example is:
- each sampled subject responds to each sampled item

Nested means one grouping factor lives inside another.
The classic social-science example is:
- students inside classes
- classes inside schools

These are both mixed-model problems, but they are not encoded the same way.

<details>
<summary>Source</summary>
<ul>
<li>R-sig-mixed-models email exchange on fixed and random effects</li>
<li>Lecture slides, Week 7, slides 42-44 and 62</li>
</ul>
</details>

#### Book / Literature Explanation


The core idea is still non-independence, but the source of that non-independence changes.
In crossed designs, observations are connected because they share subjects and items.
In nested designs, observations are connected because lower-level units belong to higher-level clusters.

So you should not memorize crossed and nested as abstract labels.
You should ask:
- what repeats with what?
- what belongs inside what?

#### Equivalent R Syntax

Crossed example:

```r
lmer(Y ~ 1 + X + (1 | subject) + (1 | item), data = d)
```

Nested example:

```r
lmer(DV ~ 1 + IV1 * IV2 + (1 + IV1 * IV2 | school/class), data = df)
```

#### How To Read It In Output


For crossed models, expect separate grouping lines such as:
- `subject`
- `item`

For nested models, expect output tied to the nested grouping structure, where lower-level clusters are interpreted within higher-level clusters.

Interpretation rule:
- crossed = multiple grouping factors combined across each other
- nested = one grouping factor contained inside another

#### Common Trap


- Confusing crossed versus nested with fixed versus random.
- Reading `school/class` as if it were an interaction rather than a nesting shorthand.

#### What To Memorize


- Crossed: subjects and items both vary and combine across each other.
- Nested: lower-level units live inside higher-level units.
- `school/class` means class nested in school.

### 4.8 Output Interpretation

#### Why This Matters


The exam explicitly tests whether you can interpret `summary(...)` output.
So reading output is not a side skill.
It is one of the main skills of the course.
In the workflow, this is the step immediately after fitting: confirm the formula and random structure before interpreting significance.

#### Statistical Formula

Use this working model:

$$
Y_{ij} = \beta_{0} + \beta_{1} X_{ij} + u_{0j} + u_{1j} X_{ij} + e_{ij}
$$

#### What Each Symbol Means

<details>
<summary>Open Symbol Meanings</summary>

- $\beta_{0}$: fixed intercept
- $\beta_{1}$: fixed slope
- $u_{0j}$: random intercept
- $u_{1j}$: random slope
- $e_{ij}$: residual error

These same parts reappear in different places in the output.

</details>

#### Plain-English Meaning

The output is the model translated into estimates.
So the job is not to stare at one p-value.
The job is to check whether the fitted model actually matches:
- the intended formula
- the intended grouping structure
- the intended random-effects structure

<details>
<summary>Source</summary>
<ul>
<li>Lecture slides, Week 2, slides 36-38</li>
<li>Lecture slides, Week 3, slides 48-52</li>
<li>Example exam questions</li>
</ul>
</details>

#### Book / Literature Explanation


The simplest way to read mixed-model output is in layers.
First confirm the formula.
Then confirm the grouping structure.
Then inspect how the model splits variation:
- random intercept variance
- random slope variance
- covariance or correlation terms
- residual variance

Only after that should you move to the fixed coefficients and their tests.
This is the opposite of the common bad habit of skipping straight to the bottom-line p-value.

#### Equivalent R Syntax

```r
m <- lmer(Reaction ~ 1 + Days + (1 + Days | f_Subject), data = sleepstudy2)
summary(m)
```

#### How To Read It In Output


Use this order every time:
1. `Formula:` line
2. `Random effects:` block
3. `Fixed effects:` block
4. `Number of obs` and `groups`
5. p-values, F-tests, likelihood-ratio tests, or confidence intervals

For the sleepstudy-style model, you should be able to identify:
- one fixed intercept
- one fixed slope for `Days`
- one random-intercept variance
- one random-slope variance
- one random correlation between intercept and slope
- one residual variance

Residual rule:
- the residual is always part of the full model anatomy
- some exam questions exclude it explicitly by saying `NOT counting the residual`
- if that phrase is absent, mention the residual as part of the full stochastic structure

#### Common Trap


- Jumping straight to p-values.
- Ignoring the random-effects block.
- Forgetting to count the covariance or correlation entry when the course asks about the random-effects structure.

#### What To Memorize


- Read output in a fixed order.
- Random-effects block first tells you what structure was actually estimated.
- Fixed-effects block gives the average effects, not the full clustering story.

### 4.9 Type 2 Versus Type 3 Tests

#### Why This Matters


Week 4 turns this into a core logic question.
If you do not understand Type 2 versus Type 3, you will not know what question the p-value is answering.
In the workflow, this matters after the model structure is fixed, when you choose the exact inferential test.

#### Statistical Formula

Use a model with an interaction:

$$
Y = \beta_{0} + \beta_{1} A + \beta_{2} B + \beta_{3} A:B + \text{error}
$$

#### What Each Symbol Means

<details>
<summary>Open Symbol Meanings</summary>

- $A$: first predictor
- $B$: second predictor
- $A:B$: interaction term
- $\beta_{1}$, $\beta_{2}$: main-effect coefficients
- $\beta_{3}$: interaction coefficient

The key issue is what the test conditions on when the interaction is present.

</details>

#### Plain-English Meaning

Type 2 and Type 3 agree about the interaction itself.
They differ for main effects when the model contains an interaction.

That means the real question is:
- what exactly am I testing the main effect against?

#### Decision Rule

Use this compact decision order:
- if the course question is about sequential, order-dependent entry of terms, that is Type 1; this is not the main local default
- if there is no interaction in the model, Type 2 and Type 3 give the same practical answer for the main effects
- if there is an interaction and you want main effects tested without conditioning on the interaction, think Type 2
- if there is an interaction and you want main effects tested in the presence of the interaction, think Type 3
- if you choose Type 3 for factors, use appropriate coding rather than treatment coding

<details>
<summary>Source</summary>
<ul>
<li>Lecture slides, Week 4, slides 41-43</li>
</ul>
</details>

#### Book / Literature Explanation


The easiest way to think about it is this:
- Type 2 asks whether a main effect matters after accounting for the other main effect
- Type 3 asks whether a main effect matters even while the interaction is in the model

So if there is no interaction, the distinction collapses.
If there is an interaction, the distinction becomes important because the meaning of a "main effect" is now conditional.

#### How This Course Determines Significance

In this course, significance for linear mixed models is not treated as a single default number that you simply read off one output table. The local Week 4 workflow distinguishes between significance of coefficients and significance of fixed effects as effects. If you are working at the coefficient level, confidence intervals can be used to judge whether a coefficient is credibly different from zero, but the slides explicitly distinguish between different kinds of intervals. Wald intervals are treated with caution, whereas likelihood-profile and bootstrap intervals are presented as the more trustworthy routes. The slides also note that this confidence-interval logic applies most directly to coefficients, not automatically to broader effect questions.

If you want to test fixed effects directly, the course moves to explicit testing methods. For Type 2 questions, the local routes are likelihood-ratio tests with `anova()`, bootstrapped likelihood-ratio tests with `PBmodcomp()`, and conditional F-tests with Kenward-Roger correction through `KRmodcomp()`. For Type 3 questions, the course instead uses functions such as `car::Anova(test = "F")` or `afex::mixed(...)`, together with the correct contrast coding. The Week 4 materials also stress that you should decide on the significance-testing method beforehand rather than switch methods opportunistically after seeing the data.

The clearest Week 4 decision tree is written as a fallback strategy. First choose Kenward-Roger p-values as the preferred route. If that fails because of technical problems, move to bootstrapped likelihood-ratio tests. If that also fails, fall back to regular likelihood-ratio tests. In other words, the course treats significance determination as a principled method choice, not as an afterthought.

<details>
<summary>Source: significance workflow for LMMs</summary>
<ul>
<li>Lecture slides, Week 4, p-values overview and method-comparison slides</li>
<li>Lecture slides, Week 4, "What should you use?" decision-tree slide</li>
<li>Example R script, Week 4</li>
</ul>
</details>

#### Equivalent R Syntax

```r
car::Anova(m, type = 2, test = "F")
car::Anova(m, type = 3, test = "F")
```

```r
afex::mixed(Y ~ A * B + (1 + B | subject), data = d, type = 3, method = "KR")
```

#### How To Read It In Output


Ask:
- does the model contain an interaction?

If no:
- Type 2 and Type 3 give the same practical answer

If yes:
- the main-effect tests can differ
- Type 3 interpretation depends on valid coding

#### Common Trap


- Thinking Type 2 and Type 3 are always interchangeable.
- Running Type 3 with treatment coding and trusting the result anyway.

#### What To Memorize


- No interaction -> no practical Type 2 versus Type 3 difference.
- Interaction present -> main-effect tests can differ.
- Type 3 requires appropriate coding.

### 4.10 Maximal Models

#### Why This Matters


This is one of the course's strongest best-practice messages.
For confirmatory testing, the course pushes you to start from the richest random-effects structure justified by the design.
In the workflow, this belongs to the confirmatory branch, where you choose the richest justified random structure before reacting to warnings.

#### Statistical Formula

Generic maximal logic:

$$
Y_{ij} = \text{fixed effects} + \text{all justified random intercepts} + \text{all justified random slopes} + \text{justified random covariance terms} + \text{residual}
$$

#### What Each Symbol Means

<details>
<summary>Open Symbol Meanings</summary>

This chapter is not about one single symbol.
It is about what must be included once the design is known:
- random intercepts for grouping factors
- random slopes for within-unit effects
- random slopes for relevant within-unit interactions
- random covariance terms when they are estimable

</details>

#### Plain-English Meaning

A maximal model is not "the biggest model you can type."
It is the most complete random-effects structure that the design justifies and the data can support.

So the question is not:
- what converges fastest?

The question is:
- what random structure is required if I want defensible confirmatory inference?

<details>
<summary>Source</summary>
<ul>
<li>Lecture slides, Week 5, slides 47-56</li>
<li>Lecture slides, Week 6, slides 37 and 40</li>
<li>Barr, Levy, Scheepers, and Tily (2013)</li>
</ul>
</details>

#### Book / Literature Explanation


The teaching logic is:
1. identify grouping factors
2. identify fixed effects and interactions of interest
3. ask which of those effects vary within each grouping factor
4. include the corresponding random slopes if the design and replication allow them
5. keep the justified covariance terms unless estimation or identifiability forces a principled simplification

This is why maximality is design-driven rather than software-driven.
The model is built from the structure of the experiment or study, not from trial-and-error searching for the easiest fit.

#### Equivalent R Syntax

Actual course example:

```r
lmer(frequency ~ 1 + attitude * gender +
     (1 + attitude | subject) +
     (1 + gender * attitude | f_scenario),
     data = politeness)
```

Generic confirmatory template:

```r
lmer(Y ~ 1 + A * B + (1 + justified_subject_terms | subject) +
     (1 + justified_item_terms | item), data = d)
```

<details>
<summary>Source</summary>
<ul>
<li>Lecture slides, Week 5, slides 47-56</li>
<li>Lecture slides, Week 6, slides 37 and 40</li>
<li>Barr, Levy, Scheepers, and Tily (2013)</li>
</ul>
</details>

#### Design-To-Model Decryption


Read the generic confirmatory template like this:
- `Y`: dependent variable
- `1`: fixed intercept
- `A * B`: fixed main effects for `A` and `B`, plus the `A:B` interaction
- `(1 + justified_subject_terms | subject)`: subject random intercept plus every subject-level random slope justified by the design
- `(1 + justified_item_terms | item)`: item random intercept plus every item-level random slope justified by the design

The design question behind it is:
- which effects are of substantive interest? -> fixed effects
- which units repeat? -> grouping factors
- which fixed effects vary within each grouping factor? -> candidate random slopes
- which covariance terms are estimable? -> keep them if the design supports them

#### How To Read It In Output


When checking a supposed maximal model, ask:
- which grouping factors are present?
- which justified slopes are present?
- are the covariance terms present?
- is the fitted structure actually the one the design implies?

The output is not only for interpretation after the fact.
It is also how you verify that the intended maximal structure was really fit.

#### Common Trap


- Calling a model "maximal" just because it looks complicated.
- Simplifying before checking whether the design actually justified the omitted slope.

#### What To Memorize


- Maximal = all random effects justified by the design, if estimable.
- Within-unit fixed effects are the main candidates for random slopes.
- Maximality is a confirmatory principle, not a convenience principle.

### 4.11 Syntax Decoding

#### Why This Matters


The example exam explicitly tests whether you can translate syntax into plain English.
So syntax decoding is not just a coding skill.
It is a reading skill.
This skill is used whenever you write a model, read output, or answer syntax-to-meaning questions.

#### Statistical Formula

Use this working example:

```r
lmer(Reaction ~ 1 + Days + (1 + Days | f_Subject), data = sleepstudy2)
```

#### What Each Symbol Means

<details>
<summary>Open Symbol Meanings</summary>

- $Reaction$: dependent variable
- $~$: is predicted by
- $1$: intercept
- $Days$: fixed predictor in the fixed-effects part; the model estimates one average `Days` slope before it allows any unit-specific deviations
- $(1 + Days | f_{Subject})$: random intercept and random slope for `Days`, varying across subjects
- $f_{Subject}$: grouping factor

</details>

#### Plain-English Meaning

This formula says:
- predict `Reaction`
- estimate an overall intercept (`1` in the fixed part)
- estimate an average effect of `Days` (`Days` in the fixed part)
- allow each subject to have a different baseline (`1` inside the random term)
- allow each subject to have a different `Days` effect (`Days` inside the random term)
- estimate the intercept-slope correlation automatically because both random coefficients appear inside the same `( ... | f_Subject )` term

Syntax decoding is therefore just model translation.

<details>
<summary>Source</summary>
<ul>
<li>Example exam questions</li>
<li>Lecture slides, Week 2, slide 26</li>
</ul>
</details>

#### Book / Literature Explanation


The easiest way to decode syntax is to read in layers:
1. identify the dependent variable
2. read the fixed part as ordinary regression
3. read each random term as "what varies" on the left of `|`
4. read the grouping factor as "who varies" on the right of `|`

If you do that consistently, the formula stops looking like shorthand and starts looking like a sentence.

#### Full Formula Decryption


For:

```r
lmer(Reaction ~ 1 + Days + (1 + Days | f_Subject), data = sleepstudy2)
```

identify each role explicitly:
- `Reaction` = dependent variable
- `~` = is predicted by
- `1` after `~` = fixed intercept
- `Days` before the random term = fixed slope
- `1` inside `(1 + Days | f_Subject)` = random intercept
- `Days` inside `(1 + Days | f_Subject)` = random slope
- `f_Subject` = grouping factor
- shared placement inside one `( ... | f_Subject )` term = estimate the intercept-slope correlation automatically
- action status for that correlation term = no extra action is needed unless you intentionally remove it with `||` or by separating the random terms
- no written residual term in the R syntax = residual still exists in the fitted LMM
- `data = sleepstudy2` = dataset declaration, not part of the model structure

Minimal sentence translation:
- predict `Reaction`
- estimate one average intercept
- estimate one average `Days` slope
- allow subjects to differ in their intercept
- allow subjects to differ in their `Days` slope
- estimate the correlation between those subject-specific deviations
- retain residual error

#### Equivalent R Syntax

Intercept-only random-intercept model:

```r
lmer(distance ~ 1 + (1 | pid), data = dfcp)
```

Random-intercept plus random-slope model:

```r
lmer(Reaction ~ 1 + Days + (1 + Days | f_Subject), data = sleepstudy2)
```

Crossed random-effects pattern:

```r
lmer(Y ~ 1 + X + (1 | subject) + (1 | item), data = d)
```

<details>
<summary>Source</summary>
<ul>
<li>Example exam questions</li>
<li>Lecture slides, Week 2, slide 26</li>
<li>Lecture slides, Week 3, slide 45</li>
</ul>
</details>

#### How To Read It In Output


The formula line in the output is your first check.
You should be able to translate it before reading the numerical estimates.

#### Common Trap


- Reading the grouping factor as if it were another fixed predictor.
- Forgetting that `1` means intercept, not "nothing."

#### What To Memorize


- left of `|` = what varies
- right of `|` = who varies
- `1` = intercept
- syntax questions are translation questions

### 4.12 Contrast Coding

#### Why This Matters


Contrast coding becomes important the moment you move from fitting the model to testing and interpreting categorical effects.
In this course it matters especially for Type 3 tests.
In the workflow, this matters right before formal testing, because coding changes what the coefficients and Type 3 tests mean.

#### Statistical Formula

For a factor with multiple levels, the model is still:

$$
Y = \beta_{0} + \beta_{1} C_{1} + \beta_{2} C_{2} + ... + \text{error}
$$

#### What Each Symbol Means

<details>
<summary>Open Symbol Meanings</summary>

- $C_{1}$, $C_{2}$, ... : coded columns representing the factor
- $\beta_{0}$: intercept under the chosen coding scheme
- $\beta_{1}$, $\beta_{2}$, ... : coefficients whose meaning depends on the coding

</details>

#### Plain-English Meaning

Contrast coding tells the model how to represent a categorical predictor numerically.
That changes:
- what the intercept means
- what the coefficients mean
- which tests are easy to interpret

It does not change the substantive data.
It changes the parameterization.

#### Decision Rule

Use the following rule set in this course. If a predictor is a factor, contrast coding already matters at the model-fitting stage because it changes the meaning of the intercept and the coefficients. If you are using Type 2 tests, the Week 4 materials state that the common contrast types are acceptable. If you are using Type 3 tests, however, you should not use treatment coding, also called dummy coding. For Type 3 tests on unordered factors, the main local default is sum-to-zero coding with `contr.sum`. For Type 3 tests on ordered factors, the main local default is polynomial coding with `contr.poly`. The slides also list Helmert coding as acceptable for Type 3 tests, but the actual local script and default workflow use `contr.sum` and `contr.poly`.

The number of factor levels also matters for interpretation. If a factor has only two levels, the model estimates one contrast, so the corresponding confidence interval is usually straightforward to interpret. If a factor has three or more levels, the factor is represented by multiple contrasts. In that situation, the default confidence intervals are often less meaningful unless you define custom contrasts for the exact comparison you want to interpret.

<details>
<summary>Source</summary>
<ul>
<li>Lecture slides, Week 4, slides 43 and 56</li>
<li>Example R script, Week 4</li>
</ul>
</details>

#### Book / Literature Explanation


The course's practical lesson is that coding is not an afterthought. Coding determines what the coefficient table means, and it therefore determines what a Type 3 test is actually testing. That is why Type 3 testing needs stricter control than Type 2 testing. If you use treatment coding in a Type 3 setup, the main-effect tests no longer line up with the interpretation the course is aiming for.

The most course-typical setup is therefore very explicit. For unordered factors, use `contr.sum`. For ordered factors, use `contr.poly`. If you use `afex::mixed(...)`, the slides also note that the function automatically applies sum-to-zero contrasts for your factors unless you disable that behavior.

#### Equivalent R Syntax

```r
options(contrasts = c("contr.sum", "contr.poly"))
```

```r
afex::mixed(Y ~ A * B + (1 + B | subject), data = d, type = 3, method = "KR")
```

#### How To Read It In Output


If a factor is coded with sum-to-zero contrasts:
- the intercept usually reflects a grand-mean style reference
- coefficients are deviations relative to that coding system

So when interpreting coefficients, always ask:
- what contrast system was used?

#### Common Trap


- Treating contrast coding as a software default issue instead of an interpretation issue.
- Running Type 3 tests with treatment coding.

#### What To Memorize


- Contrast coding changes parameter meaning.
- Type 3 needs appropriate coding.
- The course's main practical default is sum-to-zero coding for unordered factors.

### 4.13 Post-Hocs And Follow-Up Models

#### Why This Matters


Once a main effect or interaction is established, the next question is often:
- where exactly is the difference?

The course separates two answers to that question:
- post-hocs
- follow-up models

#### Decision Rule

Use post-hocs when:
- you want pairwise or conditional comparisons inside the fitted model

Use follow-up models when:
- you need separate targeted models for a more local question

#### Plain-English Meaning

Post-hocs stay inside one fitted model and compare estimated means or trends.
Follow-up models refit the analysis more locally to answer a narrower question.

So they are related, but not the same procedure.

<details>
<summary>Source</summary>
<ul>
<li>Lecture slides, Week 5, slides 13-16</li>
</ul>
</details>

The clean-analysis rule is that further decomposition is not automatic after a significant omnibus result. The next step has to match the substantive question, the fitted model, and the observed pattern in the data. If the fitted model already contains the comparison you need, use post-hocs. If the question becomes narrower than the fitted model, use a follow-up model.

#### R / Method Hook

```r
emmeans(mymodel, pairwise ~ factor)
emmeans(mymodel, pairwise ~ f_1 | f_2)
```

Follow-up logic:
- fit separate models for the relevant subset or reduced comparison

#### Common Trap


- Treating post-hocs as automatic and treating them as interchangeable with follow-up models.

#### What To Memorize


- Post-hoc = comparisons inside the fitted model.
- Follow-up = separate targeted model comparisons.

### 4.14 Convergence Versus Singularity

#### Why This Matters


The course treats warnings as part of model interpretation, not as a technical nuisance.
But it also insists that not all warnings mean the same thing.

#### Decision Rule

First ask:
- is this a convergence problem?
- is this a singularity problem?

Only then decide what to do.

<details>
<summary>Source</summary>
<ul>
<li>Lecture slides, Week 6, slides 42-43</li>
</ul>
</details>

The clean-analysis rule is to diagnose the warning before reacting to it. Convergence is an optimizer-solution question, whereas singularity is a random-effects-dimension question. That is why the course's order is to check specification, scaling, coding, and optimizer behavior first, and only then decide whether simplification is actually warranted.

#### R / Method Hook

```r
lmerControl(optimizer = "bobyqa")
lmerControl(optCtrl = list(maxfun = 1e+9))
lme4::allFit(model)
```

#### Common Trap


- Treating convergence and singularity as the same warning and simplifying before diagnosing which one it is.

#### What To Memorize


- Convergence = optimizer may not have found the best solution.
- Singularity = one or more variance/covariance dimensions are estimated as zero.

### 4.15 Diagnostics

#### Why This Matters


The course repeatedly places diagnostics inside the normal workflow.
That means diagnostics are not optional and not reserved for disaster cases.

#### Decision Rule

After fitting the model:
- inspect plots
- inspect summary structure
- inspect influence
- then proceed to inference

General clarification:
- winsorising means replacing extreme values with a less extreme cutoff value rather than deleting them
- this is not explicitly taught as a named main route in the accessible local course materials
- the closest local context is Baguley on trimmed means and outliers, where potential outliers are treated as deserving scrutiny rather than automatic deletion or trimming
- the local lecture emphasis is on plotting, diagnostics, influence checks, Cook's distance, leverage, and principled model specification before altering observed values

<details>
<summary>Source: winsorising and outlier context</summary>
<ul>
<li>Baguley, section 1.4.6 on trimmed means</li>
<li>Baguley, Box 9.3 on outliers, potential outliers, and extreme values</li>
<li>Baguley, Chapter 10 discussion of robust alternatives and trimmed means</li>
<li>Lecture slides, Week 6, diagnostics and outlier mention</li>
<li>Lecture slides, Week 7, influence diagnostics, Cook's distance, and leverage</li>
</ul>
</details>

<details>
<summary>Source</summary>
<ul>
<li>Lecture slides, Week 6, slide 30</li>
<li>Lecture slides, Week 7, slides 6-7</li>
</ul>
</details>

The clean-analysis rule is that diagnostics gate inference. You should understand the raw pattern, inspect the fitted-model summary, check visual diagnostics, and examine influential cases before you finalize p values, confidence intervals, or reporting. The course's emphasis is diagnostics-first, not value-alteration-first.

#### R / Method Hook

- diagnostic plots
- `influence()` from `lme4`
- `influence.ME`
- `HLMdiag`

#### Common Trap


- Treating diagnostics as optional or as something you only do after a warning appears.

#### What To Memorize


- Diagnostics gate inference.
- Visual checks come first, formal influence tools can follow.

### 4.16 Longitudinal Models

#### Why This Matters


Longitudinal models are one of the course's major later applications of mixed-model logic.
They show that repeated-measures thinking can become explicitly time-based.
In the workflow, this matters when time itself is a fixed effect of interest and you must choose both the time function and the corresponding random slopes.

#### Statistical Formula

Linear growth model:

$$
Y_{it} = \beta_{0} + \beta_{1} Time_{it} + u_{0i} + u_{1i} Time_{it} + e_{it}
$$

Possible extension:

$$
Y_{it} = \beta_{0} + \beta_{1} Time_{it} + \beta_{2} Time_{it}^2 + u_{0i} + u_{1i} Time_{it} + e_{it}
$$

<details>
<summary>Source</summary>
<ul>
<li>Lecture slides, Week 7, slides 23-24</li>
<li>Honeymoon example script, Week 7</li>
</ul>
</details>

#### What Each Symbol Means

<details>
<summary>Open Symbol Meanings</summary>

- $Y_{it}$: outcome for person `i` at time `t`; in this chapter `i` indexes the person-level unit and `t` indexes time
- $\beta_{0}$: average baseline
- $\beta_{1}$: average linear time trend
- $\beta_{2}$: average curvature, if quadratic time is included
- $u_{0i}$: person-specific baseline deviation
- $u_{1i}$: person-specific deviation in time slope
- $e_{it}$: residual error

</details>

#### Plain-English Meaning

A longitudinal model is still a mixed model, but now time is not just repeated measurement.
Time itself is one of the main predictors of interest.

That means the main questions become:
- does the outcome change over time?
- is the change linear, quadratic, or more complex?
- do people differ in those time trajectories?

#### Book / Literature Explanation


The important shift is that longitudinal modeling is not just "more repeated measures."
It is repeated measures where the shape of change is substantive.
So time may need:
- a linear term
- a quadratic term
- sometimes more complex representations

And the random-effects structure must still respect what the design can estimate.

#### Equivalent R Syntax

```r
lmer(LifeSatisfaction ~ 1 + Time_lin + Time_quad +
     (1 + Time_lin + Time_quad | f_Person), data = hm2)
```

#### How To Read It In Output


Look for:
- fixed time coefficients
- random time-slope variance
- whether the fitted time structure matches the number of available observations per person

Interpretation rule:
- fixed time terms describe the average trajectory
- random time terms describe person-to-person differences in that trajectory

#### Common Trap


- Treating every longitudinal example as if the most complex time structure must be estimable.
- Forgetting that too few repeated points limit the random-effects structure.

#### What To Memorize


- Longitudinal model = mixed model where time is a key predictor.
- The shape of time matters.
- The random-effects structure must still respect the design.

### 4.17 Design-Driven Versus Data-Driven Analysis

#### Why This Matters


This is one of the course's highest-level judgment questions.
It determines whether your inferential claims are confirmatory or exploratory.

#### Decision Rule

If the model is chosen from the design and hypotheses:
- treat it as design-driven confirmatory analysis

If the model is chosen through stepwise improvement or search:
- treat it as data-driven exploratory analysis

Do not casually mix the two.

<details>
<summary>Source</summary>
<ul>
<li>Lecture slides, Week 7, slides 66-70</li>
</ul>
</details>

The clean-analysis rule is to keep confirmatory and exploratory logic separate. If the model was chosen from the design and hypotheses, treat the later inference as confirmatory. If the model was found through search, treat the result as exploratory and disclose that search rather than presenting the final p values as if they came from a pre-specified model. There is no single function for this distinction because it is a modeling-strategy decision, not a package feature.

#### Common Trap


- Doing model search and then presenting the final p values as if the model had been specified in advance.

#### What To Memorize


- Design-driven = confirmatory; data-driven = exploratory.
- If model selection occurred, disclose it and do not present the final inference as cleanly confirmatory.

## 5. GLMMs And Non-Gaussian Outcomes

### 5.1 Why GLMMs Are Needed

#### Why This Matters


Earlier in the course, the dependent variable was treated as approximately Gaussian and continuous.
Week 8 changes that rule.
Once the dependent variable is binary, aggregated binary, ordinal, or another non-Gaussian type, the model family and link have to respect that scale.
This is the main Step 2 branch: once the DV is non-Gaussian, you leave the LMM path and choose a GLMM family and link.

#### Statistical Formula

Generic GLMM logic:

$$
g(E[Y_{ij}]) = \beta_{0} + \beta_{1} X_{ij} + u_{0j} + u_{1j} X_{ij}
$$

#### What Each Symbol Means

<details>
<summary>Open Symbol Meanings</summary>

- $E[Y_{ij}]$: expected value of the outcome
- $g(.)$: link function that maps the outcome scale to a linear-predictor scale
- $\beta_{0}$, $\beta_{1}$: fixed effects on the link scale
- $u_{0j}$, $u_{1j}$: random effects on the link scale

</details>

#### Plain-English Meaning

GLMMs keep the mixed-model idea:
- fixed effects for average structure ($\beta_{0}$, $\beta_{1}$, ...)
- random effects for clustered variation ($u_{0j}$, $u_{1j}$, ...)
- a link function `g(.)` that connects the expected outcome to the linear predictor

What changes is the way the dependent variable is modeled.
Instead of assuming a Gaussian residual structure with an ordinary $e_{ij}$ term, the model uses a family and link that match the actual outcome scale.

<details>
<summary>Source</summary>
<ul>
<li>Lecture slides, Week 8, slides 8-15</li>
<li>Jaeger (2008)</li>
</ul>
</details>

#### Book / Literature Explanation


The teaching logic is the same as in Week 1:
- respect the data-generating structure

For ordinary mixed models, that means respecting clustering.
For GLMMs, it means respecting clustering and the scale of the dependent variable.
So the Week 8 move is not a break from the earlier course.
It is the same principle applied more carefully.

#### Equivalent R Syntax

Binary-response example:

```r
glmer(Y ~ 1 + X + (1 + X | group), family = binomial(link = "logit"), data = d)
```

Ordinal-response example:

```r
ordinal::clmm(rating ~ 1 + X + (1 + X | judge), link = "logit", data = d)
```

<details>
<summary>Source</summary>
<ul>
<li>Lecture slides, Week 8, slides 8-15</li>
<li>Jaeger (2008)</li>
</ul>
</details>

#### How To Read It In Output


The main change is that fixed coefficients now live on the link scale, not necessarily on the original response scale.
So interpretation often needs back-transformation.

#### Common Trap


- Treating GLMMs as just `lmer` with one extra argument or forcing non-Gaussian outcomes into Gaussian models because the output feels more familiar.

#### What To Memorize


- GLMMs keep the mixed-model logic but change the outcome family and link.
- The DV type determines the family, and coefficients are often on the link scale rather than the response scale.

### 5.2 Binary Responses

#### Why This Matters


This is the clearest Week 8 example and the strongest locally supported GLMM case.
It is the model you need when the outcome is a trial-level yes/no, success/failure, or 0/1 response.
Use this branch when the dependent variable is trial-level binary.

#### Statistical Formula

$$
logit(P(Y_{ij} = 1)) = \beta_{0} + \beta_{1} X_{1ij} + \beta_{2} X_{2ij} + ... + u_{0j} + ...
$$

#### What Each Symbol Means

<details>
<summary>Open Symbol Meanings</summary>

- $P(Y_{ij} = 1)$: probability of the event of interest
- $logit(.)$: log-odds transformation
- $\beta$ terms: fixed effects on the logit scale
- $u$ terms: random effects on the logit scale

</details>

#### Plain-English Meaning

The model predicts the log-odds of the outcome.
That means:
- the intercept ($\beta_{0}$) is not directly a probability; it is a log-odds intercept
- the fixed-effect coefficients ($\beta_{1}$, $\beta_{2}$, ...) are not raw probability changes; they are log-odds effects
- the random effects (`u` terms) allow participant-specific or cluster-specific deviations
- if random intercepts and random slopes are placed inside one `( ... | group )` term, their random correlations are also estimated automatically
- interpretation often needs `exp()` for odds or `plogis()` for probabilities

<details>
<summary>Source</summary>
<ul>
<li>Lecture slides, Week 8, slides 17, 21-22, and 30</li>
<li>GLMER example script, Week 8</li>
</ul>
</details>

#### Book / Literature Explanation


This is still the same design logic as before:
- identify the fixed effects
- identify the grouping factor
- justify the random slopes from the design

The difference is only the outcome scale.
So the binary GLMM is best understood as:
- mixed-effects structure from Weeks 1 to 7
- logistic link from Week 8

#### Equivalent R Syntax

```r
glmer(choice_SS0_LL1 ~ 1 + f_Now_Notnow + c_TimeDiff + c_rel_diff_Amounts +
      (1 + f_Now_Notnow + c_TimeDiff + c_rel_diff_Amounts | pp_code_ITC),
      family = binomial(link = "logit"), data = itc4)
```

<details>
<summary>Source</summary>
<ul>
<li>Lecture slides, Week 8, slides 17, 21-22, and 30</li>
<li>GLMER example script, Week 8</li>
</ul>
</details>

#### How To Read It In Output


Read it in the same order as an LMM:
1. formula
2. random-effects block
3. fixed-effects block
4. observations and groups

But interpret fixed coefficients on the logit scale first.
Then, if needed:
- `exp(coef)` for odds ratios
- `plogis(value)` for probabilities

#### Common Trap


- Reading a logit coefficient as if it were already a probability difference and forgetting that the fixed-effect logic still follows the mixed-model structure from earlier weeks.

#### What To Memorize


- Binary GLMM = `family = binomial(link = "logit")`
- Coefficients are on the logit scale; use odds or probabilities for interpretation when needed.

### 5.3 Aggregated Binary Responses And Proportions

#### Why This Matters


This is one of the easiest places to make a modeling mistake.
A proportion looks continuous, but in this course it is treated as aggregated binary data, not as ordinary Gaussian data.
Use this branch when the outcome is an aggregated binary proportion with known trial counts.

#### Statistical Formula

Weighted-proportion formulation:

$$
logit(p_{ij}) = \beta_{0} + \beta_{1} X_{ij} + u_{0j} + ...
$$

Equivalent counts formulation:

$$
Y_{ij} \sim \text{Binomial}(n_{ij}, p_{ij})
$$

$$
logit(p_{ij}) = \beta_{0} + \beta_{1} X_{ij} + u_{0j} + ...
$$

<details>
<summary>Source</summary>
<ul>
<li>Lecture slides, Week 8, slides 38-43</li>
<li>GLMER example script, Week 8</li>
</ul>
</details>

#### What Each Symbol Means

<details>
<summary>Open Symbol Meanings</summary>

- $p_{ij}$: success proportion in unit `ij`
- $n_{ij}$: number of trials underlying that proportion
- $Y_{ij}$: number of successes
- $logit(p_{ij})$: log-odds of success

</details>

#### Plain-English Meaning

The important point is that a proportion is not enough by itself.
A proportion based on 2 trials and a proportion based on 200 trials do not carry the same information.
That is why the number of underlying trials must stay in the model.

#### Book / Literature Explanation


This chapter exists to stop a very common shortcut:
- compute percentages
- forget how many trials generated them
- run a Gaussian model

The course explicitly rejects that move.
Instead, it keeps the binomial structure so the model knows how much evidence underlies each proportion.

#### Equivalent R Syntax

Weighted-proportion version:

```r
glmer(p_LL_cond ~ 1 + f_Now_Notnow + (1 + f_Now_Notnow | pp_code_ITC),
      weights = ntrials_cond, family = binomial, data = itc3_Prop)
```

Counts version:

```r
glmer(cbind(c_LL_cond, n_trials - c_LL_cond) ~ 1 + f_Now_Notnow +
      (1 + f_Now_Notnow | pp_code_ITC),
      family = binomial, data = itc3_Prop)
```

#### How To Read It In Output


The fixed effects are still on the logit scale.
The key conceptual check is whether the model preserved the trial-count information.

#### Common Trap


- Treating aggregated percentages as ordinary continuous data and forgetting that the trial count still matters.

#### What To Memorize


- Aggregated binary data are still binomial data, so the trial count must stay in the model.
- Use weighted-binomial or `cbind(successes, failures)` formulations.

### 5.4 Ordinal Outcomes

#### Why This Matters


Ordinal outcomes are heavily overtreated as metric data in practice.
The course explicitly flags that as a problem.
Use this branch when the dependent variable is ordered categorical rather than continuous or binary.

#### Statistical Formula

Cumulative-link idea:

$$
logit(P(Y_{ij} \le  k)) = threshold_{k} - (\beta_{1} X_{ij} + u_{0j} + ...)
$$

#### What Each Symbol Means

<details>
<summary>Open Symbol Meanings</summary>

- $P(Y_{ij} \le  k)$: cumulative probability of being at or below category `k`
- $threshold_{k}$: category boundary or intercept for threshold `k`
- $\beta_{1}$: common slope across categories
- $u_{0j}$: random effect

</details>

#### Plain-English Meaning

The model assumes an underlying ordered latent tendency and multiple thresholds that split it into categories.
So the model respects the order of the categories without pretending the distances between them are truly metric.

<details>
<summary>Source</summary>
<ul>
<li>Lecture slides, Week 8, slides 48-55</li>
</ul>
</details>

#### Book / Literature Explanation


The teaching point is the same as for binary data:
- respect the scale of the DV

For ordinal outcomes, the model is not trying to recover equal intervals between categories.
It is trying to model ordered category probabilities correctly.
#### Equivalent R Syntax

```r
ordinal::clmm(rating ~ 1 + temp * contact +
              (1 + temp * contact | judge),
              link = "logit", data = wine)
```

#### How To Read It In Output


Look for:
- threshold parameters
- fixed slopes
- random-effects structure

Interpretation rule:
- slopes describe the shift on the latent cumulative scale
- thresholds separate the categories

#### Common Trap


- Averaging ordinal responses and automatically treating them as metric.
- Forgetting that ordinal models estimate thresholds, not just one ordinary intercept.

#### What To Memorize


- Ordinal outcomes need ordinal mixed models when the metric approximation is not defensible.
- Cumulative models use thresholds plus shared slopes.
- `clmm(...)` is the main local example.

### 5.5 What Changes For Diagnostics And P Values In GLMMs

#### Why This Matters


Week 8 does not simply copy Week 4 into a new family.
Some assumptions and testing methods change when you move to GLMMs.

<details>
<summary>Source</summary>
<ul>
<li>Lecture slides, Week 8, diagnostics and testing slides</li>
</ul>
</details>

#### Plain-English Meaning

The workflow stays the same at a high level:
- fit model
- inspect model
- test and report

But the specific assumptions and tools are different.
You do not carry over the Gaussian checklist unchanged.
And you do not assume KR-style F-tests still work.

#### How This Course Determines Significance

Week 8 changes the significance workflow in a very concrete way. The slides explicitly say that the Gaussian F-test routes do not carry over to GLMMs. That means you should not treat `Anova(..., test = "F")`, `KRmodcomp()`, or `mixed(..., method = "KR" or "S")` as the default way to obtain GLMM p-values. Instead, the local Week 8 route shifts toward likelihood-ratio, bootstrap, and interval-based methods.

For binary and related GLMMs, the course materials say that the methods that do work are `mixed(..., method = "PB")`, `mixed(..., method = "LRT")`, `PBmodcomp()`, `bootMer()`, `confint()`, and `anova()`. In practical terms, this means that significance is determined either by a model-comparison route, by a bootstrap route, or by interval-based inference, rather than by reusing the Week 4 F-test machinery unchanged.

The Week 8 slides also become more restrictive about Type 2 and Type 3 logic in GLMMs. They state that straightforward `anova()` gives only Type 2 likelihood-ratio tests. If you want Type 3 likelihood-ratio tests in that setting, the slides describe that as a more do-it-yourself route requiring custom numerical contrasts, not as the simple default. So the course-facing takeaway is that GLMM significance testing is narrower, less automated, and more family-specific than the LMM workflow.

<details>
<summary>Source: significance workflow for GLMMs</summary>
<ul>
<li>Lecture slides, Week 8, p-values and CIs slides</li>
<li>Week 8 GLMER example script</li>
</ul>
</details>

#### Practical Workflow

1. Fit the GLMM with the correct family and link.
2. Check model fit and influential cases.
3. Use GLMM-compatible inference tools such as LRT, PB, bootstrap, confidence intervals, or model comparison.
4. Report interpretation on the appropriate scale.

#### Common Trap


- Carrying over the full Week 4 Gaussian p-value workflow into GLMMs.

#### What To Memorize


- Not all LMM inference tools survive the move to GLMMs.
- KR-style F-tests are not the local Week 8 route.
- Diagnostics shift toward fit and simulation-based checks such as `DHARMa`.

## 6. Exam Traps And Fast Distinctions

### Why This Section Exists

The example exam does not only reward long explanations.
It rewards fast, correct distinctions.

<details>
<summary>Source</summary>
<ul>
<li>Example exam questions</li>
</ul>
</details>

### 6.1 Fast Exam Checklist

Before answering any item, silently ask:
1. what is the DV type?
2. what is the grouping structure?
3. what exactly is being claimed or tested?
4. is the issue formula meaning, output meaning, design logic, or method choice?

### 6.2 High-Yield Distinctions

- Correct versus incorrect: ask whether the claim is universally true, conditionally true, or false. For example, a mixed model does not have to contain random slopes, and a random intercept does not by itself allow the effect of `X` to vary across participants.
- Minimum ingredients: a mixed model needs fixed structure and random structure. It does not automatically need interactions, multiple grouping factors, or random slopes.
- Counting random effects: under the course counting convention, count the estimated random intercept, random slope, and random covariance or correlation terms when present. Do not count the residual only if the question explicitly tells you not to.
- Syntax to meaning: translate the formula before judging it. Remember that `1` means intercept, `|` introduces the grouping factor, and `X * Z` expands to `X + Z + X:Z`.
- Design to formula: identify the DV, then the grouping factors, then which predictors vary within each grouping factor. That is what tells you which random slopes are candidates.
- Output interpretation: read the formula first, then the random-effects block, then the fixed-effects block. Do not jump straight to p-values.
- Method distinction: `anova()` is not the same as `Anova()`, Type 2 is not the same as Type 3 when interactions are present, Type 3 depends on coding, and KR-style F-tests are not the main Week 8 GLMM route.
- GLMM recognition: decide the DV family before deciding the method. Binary trial-level outcomes point to a binomial logit GLMM, aggregated successes/failures still point to a binomial GLMM, and ordered ratings point to an ordinal mixed model.

## 7. Quick Reference Tables

### 7.1 Formula-To-English Table

| Formula | Plain-English Meaning |
| --- | --- |
| `Y ~ 1` | intercept-only fixed model |
| `Y ~ 1 + X` | intercept plus average effect of `X` |
| `Y ~ 1 + (1 | group)` | mixed model with varying baseline across `group` |
| `Y ~ 1 + X + (1 | group)` | average effect of `X` plus varying baseline across `group` |
| `Y ~ 1 + X + (1 + X | group)` | varying baseline and varying effect of `X` across `group` |
| `Y ~ 1 + A * B` | main effects of `A` and `B` plus their interaction |
| `Y ~ 1 + A * B + (1 + B | subject)` | fixed interaction model with subject random intercept and `B` slope |
| `glmer(Y ~ 1 + X + (1 | group), family = binomial(link = "logit"))` | binary-response mixed model on the logit scale |
| `clmm(rating ~ 1 + X + (1 | judge), link = "logit")` | ordinal mixed model with ordered-category thresholds |

### 7.2 Syntax-To-Meaning Table

| Syntax | Meaning |
| --- | --- |
| `~` | is predicted by |
| `1` | intercept |
| `+` | add another term |
| `*` | main effects plus interaction |
| `:` | interaction only |
| `|` | left side varies across the grouping factor on the right side |
| `||` | random terms without estimating their correlation |
| `(1 | group)` | varying intercept |
| `(1 + X | group)` | varying intercept and varying `X` slope |
| `(0 + X | group)` | slope for `X` without an intercept in that random term |
| `school/class` | class nested in school |
| `cbind(successes, failures)` | aggregated binomial outcome |
| `family = binomial(link = "logit")` | binary or binomial-response GLMM |

### 7.3 Output-Reading Table

| Output Part | What To Ask |
| --- | --- |
| `Formula:` | Did I fit the model I meant to fit? |
| `Random effects:` | Which grouping factors and random components were estimated? |
| `Residual` | What observation-level variation remains after the fixed and random structure? |
| `Groups` | Over which units do the random effects vary? |
| `Fixed effects:` | What are the average effects? |
| `Number of obs` | How much data is in the fitted model? |
| test output / CI output | What exact inferential question was tested? |

### 7.4 Method-Selection Table

| Situation | Main Local Route | Main Caution |
| --- | --- | --- |
| sequential order-dependent sums of squares question | Type 1 logic in principle | not the main local default; answer depends on term order |
| LMM, Type 2 comparison | `anova()`, `PBmodcomp()`, `KRmodcomp()` | understand which reduced model is being compared |
| LMM, Type 3 testing | `car::Anova(...)`, `afex::mixed(...)` | coding matters |
| Type 3 with unordered factors | `contr.sum` / sum-to-zero coding | do not use treatment coding |
| Type 3 with ordered factors | `contr.poly` / polynomial coding | keep interpretation tied to ordered-factor logic |
| GLMM significance testing | LRT, PB, bootstrap, `anova()`, `confint()` | KR-style F-tests are not the main Week 8 route |
| post-hoc decomposition | `emmeans(...)` | do not run mechanically |
| follow-up comparison | separate targeted models | be explicit about the question being narrowed |

### 7.5 Warning-Handling Table

| Warning Type | Meaning | First Response |
| --- | --- | --- |
| convergence | optimizer may not have reached the best solution | check specification, scaling, optimizer, iterations |
| singularity | one or more random-effects dimensions are estimated as zero | inspect whether the fitted random structure is estimable and justified |
| no warning | model fit completed without flagged estimation issue | continue with diagnostics and interpretation, not blind trust |

### 7.6 DV-Type Routing Table

| DV Type | Main Model Family | Main Local Example |
| --- | --- | --- |
| continuous approximately Gaussian | LMM | `lmer(...)` course examples from Weeks 2-7 |
| binary trial-level | binomial GLMM with logit link | Week 8 intertemporal-choice example |
| aggregated binary / proportion with trial counts | binomial GLMM | Week 8 weighted / `cbind` formulations |
| ordinal | ordinal mixed model | Week 8 wine-rating `clmm(...)` example |
| counts | count-family GLMM in principle | lighter local support than the three examples above |

## Glossary

| Term | Meaning | How To Recognize It | Why It Matters In This Course |
| --- | --- | --- | --- |
| intercept | baseline prediction when predictors are at their reference value | `1` in the fixed part; often $\beta_{0}$ in equations | many formula-reading questions start by asking what the baseline is |
| slope | effect of a predictor on the outcome | a predictor term such as `X`, `Days`, or $\beta_{1}$ in an equation | you must tell apart the average slope from unit-specific slope variation |
| residual | leftover observation-level noise after the fixed and random structure | `Residual` in output; often $e_{ij}$ in equations | the guide treats it as part of the full model anatomy even when R syntax does not write it explicitly |
| fixed effect | population-level average effect of interest | fixed part of the formula, such as `A`, `B`, `Days`, or their coefficients | these are the effects you usually interpret and test directly |
| random effect | distribution of unit-level deviations around the average pattern | random-effects block in output; terms such as $u_{0j}$ and $u_{1j}$ | random effects model clustering and repeated measurement |
| grouping factor | the unit across which random effects vary | right side of `|`, such as `subject`, `item`, or `school/class` | identifying grouping factors is one of the first model-building steps |
| random intercept | unit-specific deviation in the baseline | `(1 | group)` in R; often $u_{0j}$ in equations | this is the first random effect introduced in the course |
| random slope | unit-specific deviation in a predictor effect | `(1 + X | group)` in R; often $u_{1j} X_{ij}$ in equations | the course treats these as design-sensitive and often necessary for within-unit effects |
| covariance / correlation | association between random coefficients such as a random intercept and a random slope | correlation or covariance line in the random-effects block | the guide now makes explicit that R estimates this automatically when coefficients appear in the same `( ... | group )` term |
| nested | one grouping factor lives inside another | syntax such as `school/class` | nested and crossed designs require different formula structures |
| crossed | grouping factors combine across each other | separate random terms such as `(1 | subject) + (1 | item)` | many psychology designs in the course are crossed subject-item designs |
| repeated measures | multiple observations come from the same unit | repeated rows per participant, item, or cluster | this is one main source of non-independence |
| longitudinal model | mixed model where time is a substantive predictor | terms such as `Time_lin`, `Time_quad`, or equations with index `t` | the course treats growth-curve logic as a major later application |
| Type 1 test | sequential, order-dependent sums of squares test | order of terms matters | this is not the main course default, so use it only when the question is explicitly sequential |
| Type 2 test | main-effect test that conditions on the other main effect, not the interaction | `car::Anova(..., type = 2)` | you need this distinction to know what p-value is being asked for |
| Type 3 test | main-effect test that conditions on the interaction as well | `car::Anova(..., type = 3)` or `afex::mixed(..., type = 3)` | Type 3 interpretation depends on appropriate coding |
| contrast coding | numerical representation of categorical predictors | `options(contrasts = c("contr.sum", "contr.poly"))` and factor coefficient interpretation | it changes what coefficients mean, and Type 3 tests require the right coding |
| winsorising | replacing extreme values with a cutoff value rather than deleting them | usually discussed as an outlier-handling choice, not as a model term | this is not a highlighted local method in the accessible course materials, so it should not replace the guide's main diagnostics-first workflow |
| post-hoc | comparison performed inside the fitted model | `emmeans(...)` style comparisons | the course treats post-hocs as useful but not automatic |
| follow-up model | separate targeted model fit for a narrower question | refitting a model for a subset or local comparison | follow-up models are not the same as post-hocs |
| convergence | optimizer may not have found the best numerical solution | convergence warning in model fitting output | it requires diagnosis before simplification |
| singularity | one or more random-effects dimensions are estimated as zero | singular-fit warning or `isSingular(...)` | the course treats this as different from convergence |
| link function | function connecting the expected outcome to the linear predictor in a GLMM | `link = "logit"` or notation such as $g(E[Y_{ij}])$ | this is what changes when the DV is non-Gaussian |
| logit | log-odds transformation used in many binomial and ordinal models | `binomial(link = "logit")` or `clmm(..., link = "logit")` | Week 8 interpretation often happens on the logit scale first |
| odds | multiplicative event-likelihood scale derived from log-odds | often obtained with `exp(coef)` | binary GLMM coefficients are often easier to explain as odds ratios |
| family | outcome distribution used by a GLMM | `family = binomial`, or ordinal model family choices | choosing the family is the main non-Gaussian branching decision |
| binomial | model family for binary and aggregated binary outcomes | `family = binomial(...)`, weighted binomial models, or `cbind(successes, failures)` | binary and aggregated binary outcomes are the strongest Week 8 cases locally |
| ordinal model | mixed model for ordered categorical outcomes | `ordinal::clmm(...)` and threshold-based equations | the course warns against automatically treating ordinal data as metric |
| $i$ | lower-level observation index | appears in symbols such as $Y_{ij}$ or $e_{ij}$ | the guide uses this to mark observation-level quantities |
| $j$ | higher-level unit or cluster index | appears in symbols such as $u_{0j}$ or $u_{1j}$ | the guide uses this to mark participant-, item-, or cluster-level quantities |
| $t$ | time index | appears in longitudinal symbols such as $Y_{it}$ | it marks the repeated time dimension in growth-curve models |
