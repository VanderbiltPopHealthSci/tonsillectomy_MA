# Tonsillectomy interventions meta-analysis

*2016-03-08*

We present a draft plan for the following key questions from the Vanderbilt EPC systematic review of tonsillectomy interventions.

## Key Question 5
**What are the benefits and harms of adjunctive perioperative pharmacologic agents intended to improve outcomes?**

A quantitative meta-analysis of the effects of pharmacologic agents will focus on three major classes, **Nonsteroidal anti-inflammatory drugs (NSAID)**, **steroids** and **antiemetics**. Outcomes of interest include:

+ post-operative medication use
+ time to normal diet
+ harms

The statistical approach for estimating the expected values of each outcome following the use of perioperative pharmacologic agents depends upon the outcome measure reported by each study. 

### Time to return to normal diet

Time is typically measured in hours, and hence the difference in return time between two treatments can be modeled as a continuous random variable (*e.g.* normal). Differences can be estimated relative to placebo/usual care or relative to another agent.

\\[
t_{1i} \sim N(\mu_{1i}, \sigma^2_{1i}) \\
t_{2i} \sim N(\mu_{2i}, \sigma^2_{2i}) 
\\]

where $t_{ki}$ is an observed time to normal diet for treatment $k$ in study $i$, and $\mu_{ki}$ and $\sigma_{ki}$ their associated parameters. Where appropriate, these parameters, in turn, may be modeled as random effects (particularly $\mu_{ki}$) to account for heterogeneity in effects among studies. For example:

\\[
\mu_{ki} \sim N(\theta_k, \sigma^2_k)
\\]

and the parameter on which inference would be performed is $\theta_k$, by comparing it to another treatment $j$:

\\[\delta_{kj} = \theta_k - \theta_j\\]

### Patients requiring rescue medications

Patients requiring rescue medications are reported as counts, and can therefore be modeled as a binomial or Poisson response, with inference derived from estimates of the probability or medication requirement. 

\\[x_{ki} \sim \text{Binomial}(n_i, p_{ki})\\]

These probabilities can be directly compared among interventions. For example, the probability $p_{ki}$ can be modeled as a logit-linear model with a treatment effect, and perhaps a study-specific random effect as follows:

\\[\text{logit}(p_{ki}) = \alpha + \beta_k I(k) + \epsilon_i \\]

With this formulation, $\beta_k$ can be interpreted as the log-odds of an event for treatment $k$, relative to placebo/usual care.

This covariate model can be expanded further to include the dosage of the pharmacologic agent in each study arm. This can be expressed in terms of $\beta_k$ as a hierarchical function:

\\[ \beta_{ik} = \gamma_{0k} + \gamma_{1k} d_{ik} \\]

where $d_{ik}$ is the dosage of agent $k$ in study arm $i$. In order to validly compare dosage effects among agents, dosages would likely need to be transformed using a bioequivalence model, to be expressed on a standard dosage scale such that a single standard dose is considered clinically equivalent among the suite of agents compared in the meta-analysis.

### Post-operative utilization of medications

Utilization appears most frequently to be reported in terms of cumulative number of doses, or quantity of medication consumed at followup. The most flexible approach for combining studies is to re-express utilization in terms of difference in usage, relative to a placebo/usual care baseline. Thus, each included study will yield zero or more outcome-specific differences associated with a pharmacologic intervention, which can be combined within each medication usage outcome in a random effects model. Inference across medications could only be achieved with the development of a bioequivalence model. 

### Risk of harms

The occurrence of harms within individual studies are most often reported as counts of adverse events within the study sample. The major classes of harms will include:

* primary hemorrhage
* secondary hemorrhage
* overall bleeding

This data may be modeled as binomial or Poisson random variables (depending on frequency) using the probability or rate parameter, respectively, for inference.

### Modeling approaches

Where there are 3 or more treatments to compare (or 2 + placebo), it may be possible to employ network meta-analysis (NMA) to allow the estimation of relative effect sizes in a single, joint model. This would also allow, where it is available, indirect evidence to be incorporated into the meta-analysis, possibly improving the precision of meta-estimates. NMA should be considered for both surgical and pharmacologic interventions.

In addition, it may be worth considering modeling two or more outcomes jointly, as a multivariate response. It is possible that outcomes covary, and modeling them jointly would allow for improved precision in the estimates of their effect sizes. Moreover, there may be a clinical interest in the correlation of beneficial and harmful outcomes. If, for example, a particular intervention provides relatively higher expected benefits than another intervention, but also incurs a higher risk of harms, then it would force an evaluation of that tradeoff.

Where possible, heterogeneity due to differing baseline dosages can be accounted for directly in the model, if this information is reported consistently. In the absence of reporting, however, we can apply study-specific random effects to account for differences in baseline dosages among study sites.


## Key Question 4
**Do benefits and harms differ by surgical technique?**

The approach to estimating the relative effects of surgical techniques on benefits (*i.e.* utilization) and harms mirror that for pharmacological interventions. That is, modeling count outcomes (*e.g.* occurrences of harms) as Poisson or binomial random variables and continuous outcomes as normal random variables, and estimating the effect sizes associated with each procedure.

The effect size model should include and indicator for indication (Obstructive sleep apnea (OSA), tonsillectomy, or mixed), as this is anticipated to influence outcomes.


## Key Question 3 
**Do benefits and harms differ between partial tonsillectomy and total tonsillectomy?**

The relative effect of full compared to partial tonsillectomy may be evaluated using an indicator variable for full tonsillectomy relative to a baseline effect of partial tonsillectomy (or the reverse, depending on the prevalence of each intervention in the available data). Depending on whether counts of harms or continuous differences in diet return times are being modeled as the response, this effect can be modeled as:

\\[\theta_{ki} = g(\beta_0 + \beta_1 I(x^{(full)}_{ki}))\\]

where $I$ is the indicator function that evaluates to one if $x^{(full)}_{ki}$ is true (indicating full tonsillectomy) and zero otherwise, and $g$ is an appropriate transformation, depending on the type of outcome (*e.g.* inverse-logit if we are modeling binomial counts of harms). As with KQ4, indication should also be included as a covariate.

An efficient approach to addressing this question may be to use a common model for KQ 3 and 4, with partial vs total removal simply included as a covariate in the KQ 3 model. Potentially, this would allow for comparisons of surgical technique within the partial/total subpopulation, using explicit interaction effects in the model.