# survMOD

This repository contains the `survMOD` R package, which implements modified survival tests for analyzing survival data with \( k > 2 \) groups. The package provides two main functions:

- `modified_score_k`: Computes the modified score test statistic and p-value.
- `modified_logrank_k`: Computes the modified log-rank test statistic and p-value.

Before using this package, ensure the required dependencies (`dplyr` and `MASS`) are installed and loaded.

## Installation

To install the package from a local `.tar.gz` file, run the following command in R:

```R
install.packages("path/to/survMOD_0.1.0.tar.gz", repos = NULL, type = "source")
```

## Functions Overview

### `modified_score_k`

**Description:**  
Calculates the modified score test statistic and p-value for \( k > 2 \) groups in survival analysis.

**Parameters:**  
- `list_of_dfs`: A list of data frames, each representing a group. Each data frame must contain:
  - `X_ij`: Survival times.
  - `delta_ij`: Event indicators (1 for event, 0 for censoring).

**Returns:**  
- A list containing:
  - `statistic`: The test statistic.
  - `p_value`: The p-value for the test.
  - `Sigma`: The covariance matrix.

---

### `modified_logrank_k`

**Description:**  
Calculates the modified log-rank test statistic and p-value for k > 2 groups in survival analysis.

**Parameters:**  
- `list_of_dfs`: A list of data frames, each representing a group. Each data frame must contain:
  - `X_ij`: Survival times.
  - `delta_ij`: Event indicators (1 for event, 0 for censoring).

**Returns:**  
- A list containing:
  - `statistic`: The test statistic.
  - `p_value`: The p-value for the test.
  - `Sigma`: The covariance matrix.

---

## Example Usage

Here is an example using data from the `survELtest` package:

```R
# Load the survELtest package
library(survELtest)

# Use the threearm dataset
threearm

# Rename the columns in the threearm dataset
colnames(threearm) <- c("X_ij", "delta_ij", "group")

# Partition the data into groups
df1 <- subset(threearm, group == 1)
df2 <- subset(threearm, group == 2)
df3 <- subset(threearm, group == 3)

# Combine the three data frames into a list
list_of_dfs <- list(df1, df2, df3)

# Run the Modified Score Test
mod_score_result <- modified_score_k(list_of_dfs)
print("Modified Score Test Results:")
print(mod_score_result)

# Run the Modified Log-rank Test
mod_logrank_result <- modified_logrank_k(list_of_dfs)
print("Modified Log-rank Test Results:")
print(mod_logrank_result)
