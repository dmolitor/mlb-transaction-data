# MLB Data

This repo houses the following MLB data sources
1. [MLB Transaction Data](http://mlb.mlb.com/mlb/transactions/) 
2. Injury Data (extracted from the Transaction Data)

The data spans January, 2001 to the beginning of the current month.

## Importing the Data

To have this data available locally, simply clone the repository and you should be set. Alternatively you can import this data directly from Github.
Below are two short helper functions for importing the data in both R and Python.

- **R**
```r
library(readr)

read_transactions <- function(year = "all-years", type = "injuries") {
  if (!type %in% c("injuries", "transactions")) {
    stop("'type' should be one of 'injuries' or 'transactions'", call. = FALSE)
  }
  github_raw <- "https://raw.githubusercontent.com/dmolitor/mlb-transaction-data/main/"
  transactions_url <- paste0(github_raw, type, "/", year, "/", type, ".csv")
  read_csv(transactions_url)
}

# Import all transactions
transactions <- read_transactions(type = "transactions")

# Import all injuries
injuries <- read_transactions(type = "injuries")
```

- **Python**
```python
import pandas as pd

def read_transactions(year = "all-years", type = "transactions"):
  if not type in ["transactions", "injuries"]:
    raise ValueError("'type' should be one of 'injuries' or 'transactions'")
  github_raw = "https://raw.githubusercontent.com/dmolitor/mlb-transaction-data/main/"
  transactions_url = github_raw + type + "/" + str(year) + "/" + type + ".csv"
  dat = pd.read_csv(transactions_url)
  return dat

# Import all transactions
transactions = read_transactions(year = "all-years", type = "transactions")

# Import all injuries
injuries = read_transactions(year = "all-years", type = "injuries")
```

## Issues with the Data

On several random baseball forums I've seen people complaining about the quality of MLB's Transaction data. I'm sure this complaining is warranted.
Additionally, all this data is being scraped with no direct manual oversight. As such, some mistakes are likely!
