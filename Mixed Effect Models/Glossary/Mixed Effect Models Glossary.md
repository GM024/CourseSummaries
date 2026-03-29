# Mixed Effect Models Glossary

This glossary is the course-level terminology aid for recurring key terms. Inline explanation in the week summaries remains primary, but this file now adds short code exemplars wherever the meaning of a term is tied directly to modeling syntax or testing workflow.

## A

### Aggregated Binary Response

A proportion-like outcome that is actually built from a count of successes out of a known number of trials, such as 12 successes out of 20 attempts.

Typical use:
- Use this when the DV is based on repeated binary outcomes and you still know the trial count for each row.
- The course treats these as binomial data, not as ordinary Gaussian proportions.

Example:

```r
glmer(
  cbind(c_LL_cond, ntrials_cond - c_LL_cond) ~ 1 + f_Now_Notnow +
    (1 + f_Now_Notnow | pp_code_ITC),
  family = binomial,
  data = itc3_Prop
)
```

First seen:
- Week 8
- `Week 8/Slides_Lecture_Class8_23March2026_19March2026a.pdf`

### Bootstrap Interval

A confidence interval built from repeated resampling rather than from a simple normal-theory approximation.

First seen:
- Week 2
- `Week 2/MixedModels_Class2_2Feb2026_30Jan2026a.pdf`

## B

### Binary Response

An outcome with only two possible values, such as yes/no, correct/incorrect, or one choice versus another.

Typical use:
- Use a binary-response mixed model when each observation is one of two outcomes.
- The course's default binary route is a binomial GLMM with a logit link.

Example:

```r
glmer(
  choice_SS0_LL1 ~ 1 + f_Now_Notnow + c_TimeDiff + c_rel_diff_Amounts +
    (1 + f_Now_Notnow + c_TimeDiff + c_rel_diff_Amounts | pp_code_ITC),
  family = binomial(link = "logit"),
  data = itc4
)
```

First seen:
- Week 8
- `Week 8/Slides_Lecture_Class8_23March2026_19March2026a.pdf`

## C

### Clustered Errors

Dependence among observations that arises because rows share a participant, item, class, or other grouping unit.

First seen:
- Week 1
- `Week 1/Aarts Verhage Veenvliet Dolan van der Sluis Nature Neuroscience 2014.pdf`

### Contrast Coding

The rule that determines how categorical predictors are translated into model parameters.

Typical use:
- In this course it matters especially for Type 3 tests.
- Type 3 tests should not be run with treatment coding; the local default is sum-to-zero coding for unordered factors and polynomial coding for ordered factors.

Example:

```r
options(contrasts = c("contr.sum", "contr.poly"))
```

Typical situation:

```r
m <- lme4::lmer(Reaction ~ Days * Group + (1 + Days | f_Subject), data = d)
car::Anova(m, type = 3, test = "F")
```

First seen:
- Week 4
- `Week 4/MixedModels_Class4_23Feb2026_19Feb2026a.pdf`

### Convergence Warning

A warning that the estimation procedure may not have found a fully stable optimum for the fitted model.

First seen:
- Week 6
- `Week 6/MixedModels_Class6_9March2026_6March2026a.pdf`

### Crossed Random Effects

Random effects for grouping factors that combine across each other rather than being nested one inside another, such as subjects and items.

Typical situation:
- Use crossed random effects when rows are clustered simultaneously by two grouping factors that are not nested inside one another.

Example:

```r
DV ~ 1 + X + (1 | subject) + (1 | item)
```

First seen:
- Week 5
- `Week 5/MixedModels_Class5_2March2026_28Feb2026a_BrSp.pdf`

### Credible Interval

A Bayesian interval that gives a posterior range of plausible parameter values.

First seen:
- Week 3
- `Week 3/MixedModels_Class3_9Feb2026_5Feb2026a_BrSp.pdf`

## E

### Effective Sample Size

The amount of truly independent information left after dependence within clusters has been taken into account. It is the sample size the data behave like after non-independence has been accounted for, not just the raw number of rows.

Typical use:
- This matters whenever many rows come from the same participant, item, class, or other grouping unit.
- If rows are highly dependent, the effective sample size can be much smaller than the observed sample size.

Typical situation:
- `100` rows from `100` independent people gives an effective sample size close to `100`.
- `100` rows from `10` people measured `10` times each still gives an observed sample size of `100`, but the effective sample size is smaller because the rows are not fully independent.

First seen:
- Week 1
- `Week 1/Aarts Verhage Veenvliet Dolan van der Sluis Nature Neuroscience 2014.pdf`

## F

### Fixed Effect

A population-average effect that represents the systematic relationship of a predictor to the outcome.

First seen:
- Week 1
- `Week 1/bw_LME_tutorial2.pdf`

## G

### Generalized Linear Mixed Model (GLMM)

A mixed model for outcomes that are not well modeled as continuous Gaussian data, such as binary or ordinal responses.

Typical use:
- Use a GLMM when the dependent variable is binary, aggregated binary, ordinal, count-based, or otherwise non-Gaussian.
- The family and link must match the DV scale.

Example:

```r
glmer(Y ~ 1 + X + (1 + X | group), family = binomial(link = "logit"), data = d)
```

First seen:
- Week 8
- `Week 8/Slides_Lecture_Class8_23March2026_19March2026a.pdf`

## H

### Hierarchical Data

Data in which observations are grouped within higher-level units, such as repeated rows within participants or students within classes.

Typical situation:
- The same dependence logic applies whether the higher-level units are participants, classes, schools, clinics, or families.

Example:

```r
DV ~ 1 + IV1 * IV2 + (1 + IV1 * IV2 | school/class)
```

First seen:
- Week 1
- `Syllabus.pdf`

## I

### Intercept-Only Model

A model that includes only the intercept as a fixed effect, with no additional fixed predictors.

First seen:
- Week 2
- `Week 2/MixedModels_Class2_2Feb2026_30Jan2026a.pdf`

### Intra-Class Correlation (ICC)

The share of total variance that lies at the grouping level rather than at the residual level.

First seen:
- Week 2
- `Week 2/MixedModels_Class2_2Feb2026_30Jan2026a.pdf`

## K

### Kenward-Roger Approximation

An approach for approximating denominator degrees of freedom for conditional F-tests in linear mixed models.

Typical use:
- In the course this is a preferred LMM route for effect testing.
- It is not the default route for GLMMs.

Example:

```r
KRmodcomp(full_model, reduced_model)
car::Anova(m, type = 3, test = "F")
```

First seen:
- Week 4
- `Week 4/MixedModels_Class4_23Feb2026_19Feb2026a.pdf`

## L

### Likelihood Ratio Test (LRT)

A nested-model comparison test that evaluates whether adding a fixed effect significantly improves model fit.

Typical use:
- Use this when you compare a fuller model to a reduced model.
- The course uses this especially for Type 2 logic and as one of the fallback routes in Week 4 and Week 8.

Example:

```r
anova(full_model, reduced_model)
```

First seen:
- Week 4
- `Week 4/MixedModels_Class4_23Feb2026_19Feb2026a.pdf`

### Link Function

A function that connects the linear predictor to the expected value of a non-Gaussian outcome in a generalized model.

Typical use:
- In Week 8, the most common link is the logit link for binary and ordinal examples.

Example:

```r
family = binomial(link = "logit")
link = "logit"
```

First seen:
- Week 8
- `Week 8/Slides_Lecture_Class8_23March2026_19March2026a.pdf`

### Logit

The log-odds scale used to model many binary and ordinal outcomes.

Typical use:
- Binary GLMM coefficients are often estimated on the logit scale first and then translated to odds or probabilities.

Example:

```r
glmer(Y ~ 1 + X + (1 | group), family = binomial(link = "logit"), data = d)
plogis(1.2691)
exp(1.2691)
```

First seen:
- Week 8
- `Week 8/Slides_Lecture_Class8_23March2026_19March2026a.pdf`

### Longitudinal Model

A mixed model in which repeated observations are indexed by time and the trajectory across time is itself part of the research question.

Typical use:
- Use this when time is substantively important, not just a nuisance repeated-measures index.
- The course treats growth-curve models as the main longitudinal example.

Example:

```r
LifeSatisfaction ~ 1 + Time_lin + Time_quad +
  (1 + Time_lin + Time_quad | f_Person)
```

First seen:
- Week 7
- `Week 7/MixedModels_Class7_16March2026_12March2026b_BrSp.pdf`

## M

### Maximum Likelihood (ML)

An estimation approach that fits model parameters by maximizing the likelihood of the observed data.

First seen:
- Week 4
- `Week 4/MixedModels_Class4_23Feb2026_19Feb2026a.pdf`

## N

### Nested Data

Data with a multilevel structure in which lower-level observations are grouped within higher-level units, such as trials within participants or students within schools.

Typical situation:
- Use nested syntax when one grouping factor lives inside another.
- The course's standard example is classes nested in schools.

Example:

```r
(1 + IV1 * IV2 | school/class)
```

First seen:
- Week 1
- `Week 1/Aarts Verhage Veenvliet Dolan van der Sluis Nature Neuroscience 2014.pdf`

### Non-Independence

The condition in which observations share information because they come from the same subject, item, cluster, or higher-level unit.

First seen:
- Week 1
- `Week 1/bw_LME_tutorial2.pdf`

## O

### Omnibus Test

An effect-level test that evaluates whether a predictor or interaction contributes overall, rather than testing only one coefficient at a time.

Typical use:
- Use this when an effect spans multiple coefficients, such as a multi-level factor or an interaction.

First seen:
- Week 4
- `Week 4/MixedModels_Class4_23Feb2026_19Feb2026a.pdf`

### Ordinal Model

A model for ordered categorical outcomes where category order matters but equal spacing between categories should not be assumed.

Typical use:
- Use this for rating scales and other ordered categories when the course does not want them treated as ordinary continuous variables.

Example:

```r
ordinal::clmm(
  rating ~ 1 + temp * contact + (1 + temp * contact | judge),
  link = "logit",
  data = wine
)
```

First seen:
- Week 8
- `Week 8/Slides_Lecture_Class8_23March2026_19March2026a.pdf`

## P

### Posterior Predictive Check

A Bayesian diagnostic that compares observed data patterns to data simulated from the fitted posterior model.

First seen:
- Week 3
- `Week 3/MixedModels_Class3_9Feb2026_5Feb2026a_BrSp.pdf`

### Profile Interval

A confidence interval based on the likelihood profile of a fitted parameter rather than only on a normal-theory approximation.

First seen:
- Week 2
- `Week 2/MixedModels_Class2_2Feb2026_30Jan2026a.pdf`

## R

### Random Effect

A grouped deviation that lets units such as participants or items differ from the overall population-average pattern.

Example:

```r
(1 | subject)
```

First seen:
- Week 1
- `Week 1/bw_LME_tutorial2.pdf`

### Random Intercept

A random effect that allows different groups or units to have different baseline levels of the outcome.

Example:

```r
(1 | subject)
```

First seen:
- Week 1
- `Week 1/bw_LME_tutorial2.pdf`

### Random Correlation

The estimated association between group-specific random effects, such as a random intercept and a random slope.

First seen:
- Week 3
- `Week 3/MixedModels_Class3_9Feb2026_5Feb2026a_BrSp.pdf`

### Random Slope

A random effect that allows the effect of a predictor to differ across groups or units.

Example:

```r
(1 + Days | f_Subject)
```

First seen:
- Week 3
- `Week 3/MixedModels_Class3_9Feb2026_5Feb2026a_BrSp.pdf`

### REML

Restricted maximum likelihood, an estimation approach commonly used in linear mixed models for variance-component estimation.

First seen:
- Week 2
- `Week 2/MixedModels_Class2_2Feb2026_30Jan2026a.pdf`

### Rhat

A Bayesian convergence diagnostic that compares within-chain and between-chain behavior; values close to 1 are desired.

First seen:
- Week 3
- `Week 3/MixedModels_Class3_9Feb2026_5Feb2026a_BrSp.pdf`

## S

### Satterthwaite Approximation

An approach for approximating degrees of freedom for F- or t-based inference in mixed models.

First seen:
- Week 4
- `Week 4/MixedModels_Class4_23Feb2026_19Feb2026a.pdf`

### Singularity Warning

A warning that the random-effects structure may be too rich for the information in the data, often because one or more variance components are estimated at or near zero.

First seen:
- Week 6
- `Week 6/MixedModels_Class6_9March2026_6March2026a.pdf`

## T

### Type 1 Test

A sequential, order-dependent effect test in which each term is tested in the order it enters the model.

Typical use:
- This is not the main course default.
- Use it only if the question is explicitly sequential, because changing the order of terms changes the result.

Typical situation:
- If `A` is entered before `B`, then `A` is tested before `B` has been accounted for.

First seen:
- Week 4
- `Week 4/MixedModels_Class4_23Feb2026_19Feb2026a.pdf`

### Type 2 Test

An effect-level test that evaluates each term after accounting for the others without testing higher-order terms that contain it.

Typical use:
- Use this when you want the main-effect question without conditioning that main effect on the interaction that contains it.
- In the course, manual comparison routes such as `anova()`, `KRmodcomp()`, and `PBmodcomp()` are mainly Type 2 style.

Example:

```r
car::Anova(m, type = 2, test = "F")
anova(full_model, reduced_model)
KRmodcomp(full_model, reduced_model)
PBmodcomp(full_model, reduced_model)
```

Typical situation:

```r
m <- lme4::lmer(Reaction ~ Days * Group + (1 + Days | f_Subject), data = d)
car::Anova(m, type = 2, test = "F")
```

First seen:
- Week 4
- `Week 4/MixedModels_Class4_23Feb2026_19Feb2026a.pdf`

### Type 3 Test

An effect-level test that evaluates each term in the presence of all other terms in the model, including higher-order interactions.

Typical use:
- Use this when you want to test a main effect while the interaction is still in the model.
- This is the main course workflow for omnibus testing in models with interactions.
- Correct contrast coding is part of the setup.

Example:

```r
options(contrasts = c("contr.sum", "contr.poly"))
car::Anova(m, type = 3, test = "F")
afex::mixed(Y ~ A * B + (1 + B | subject), data = d, type = 3, method = "KR")
```

Typical situation:

```r
m <- lme4::lmer(Reaction ~ Days * Group + (1 + Days | f_Subject), data = d)
car::Anova(m, type = 3, test = "F")
```

First seen:
- Week 4
- `Week 4/MixedModels_Class4_23Feb2026_19Feb2026a.pdf`

## W

### Wald Interval

A confidence interval built from the estimate plus or minus a standard-error-based normal approximation.

First seen:
- Week 2
- `Week 2/MixedModels_Class2_2Feb2026_30Jan2026a.pdf`
