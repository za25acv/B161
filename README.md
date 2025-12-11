# Employee Turnover Chi-Square Analysis


This repository investigates whether there is a significant difference in the proportion of employees who leave the company based on gender.


## Research Question
Is there a difference in the proportion of employees who leave the company between males and females?


## Team Members
1. Ajay
2. Jenin Jaban Harry
3. Rahul Bingi
4. David Ajeibi
5. Affaz Ahmad Khan


---
## Statistical Method
A **Chi-square test of independence** was used to examine the relationship between gender and employee leaving behavior.


### Chi-square Formula
\[
\chi^2 = \sum \frac{(O - E)^2}{E}
\]


### Results
- Chi-square Statistic: **227.81**
- Degrees of Freedom: **1**
- p-value: **< 0.0001**


### Interpretation
Since the p-value is significantly less than 0.05, the null hypothesis is rejected. There is a statistically significant relationship between gender and leaving the company. The observed counts indicate that females have higher chances of leaving than males.


---
## Files
- `analysis.R`: Runs the full chi-square analysis.
- `data.csv`: Replace this file with your actual dataset.
- `.gitignore`: Standard R project ignores.
- `requirements.txt`: Notes on reproducibility.


---
## How to Run
```bash
Rscript analysis.R


---


## analysis.R


```r
# ------------------------------------------------------------
# Employee Turnover Chi-square Analysis
# ------------------------------------------------------------


# Load dataset (must contain columns: Gender, Status)
data <- read.csv("data.csv")


# Build contingency table
contingency <- table(data$Gender, data$Status)


print("Observed counts:")
print(contingency)


# Run chi-square test
chi <- chisq.test(contingency, correct = FALSE)


# Output results
cat("\nChi-square Statistic: ", chi$statistic)
cat("\nDegrees of Freedom: ", chi$parameter)
cat("\np-value: ", chi$p.value, "\n")


cat("\nExpected Counts:\n")
print(round(chi$expected, 2))


# Interpretation
if (chi$p.value < 0.05) {
cat("\nDecision: Reject H0. Gender and leaving are significantly related.\n")
} else {
cat("\nDecision: Fail to reject H0. No significant relationship.\n")
}

# ------------------------------------------------------------
# Chi-square test: Difference in proportion of leavers 
# between males and females
# ------------------------------------------------------------

# Observed counts from your description:
# Female left = 884
# Male left = 716

# Replace the stayed values with your actual numbers if needed
male_stayed <- 1200    # placeholder
female_stayed <- 900   # placeholder

# Create contingency table
observed <- matrix(
  c(male_stayed, male_left <- 716,
    female_stayed, female_left <- 884),
  nrow = 2,
  byrow = TRUE
)

rownames(observed) <- c("Male", "Female")
colnames(observed) <- c("Stayed", "Left")

observed

# Run chi-square test
chi_result <- chisq.test(observed, correct = FALSE)

# Print outputs
cat("\n-------------------------------------------\n")
cat("Chi-Square Test: Gender vs Leaving\n")
cat("-------------------------------------------\n")

cat("\nObserved Counts:\n")
print(observed)

cat("\nExpected Counts:\n")
print(round(chi_result$expected, 2))

cat("\nChi-square Statistic:", chi_result$statistic)
cat("\nDegrees of Freedom:", chi_result$parameter)
cat("\np-value:", chi_result$p.value, "\n")

# Interpretation
if (chi_result$p.value < 0.05) {
  cat("\nDecision: Reject the null hypothesis.\n")
  cat("Conclusion: Gender and leaving status are significantly related.\n")
} else {
  cat("\nDecision: Fail to reject the null hypothesis.\n")
  cat("Conclusion: No significant relationship between gender and leaving.\n")
}
