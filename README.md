# econ3916-lab06-sampling
Lab 06 submission
# Sampling for Machine Learning — Train-Test Splits

## Objective
I tested how the way I split and sample data changes the estimates I get, using the Titanic dataset and a simulation of the 1936 Literary Digest poll.

## Methodology
- I explored the Titanic dataset (891 passengers) and looked at how survival differed by passenger class.
- I compared a naive random train-test split with a split stratified on survival, and checked that stratifying kept the survival rate the same in the training and test sets.
- I found and fixed data leakage in two steps: a StandardScaler and a SimpleImputer that had been fit on all the data before splitting. In both cases I split first, fit on the training rows only, and then applied the result to the test rows.
- I wrote a function, split_by_share(), that splits a table by a test share and a seed, and checked that it reproduces the lab's own split.
- I simulated the 1936 Literary Digest polling failure with a population of 10 million voters, comparing a sample whose chance of inclusion rose with income against a simple random sample of 50,000.
- I computed Meng's data defect correlation for the biased sample and compared the error his formula predicts with the actual error.
- I ran 100 replications of both samples to compare how far off and how spread out their estimates were.

## Key Findings
- Stratifying on survival kept the survival rate the same in both halves of the split. A naive split leaves that to chance.
- Fitting a preprocessing step on all the data lets the test rows shape the training data, which makes the model's test score look better than it should. Splitting first keeps the test set unseen.
- A biased sample of 4,382,503 responses was less accurate than a random sample of 50,000.
- Sample design beats sample size: a data defect correlation of 0.1475 produced an error of 8.3 percentage points.
- Across 100 replications, the biased estimates clustered tightly around the wrong answer, while the random estimates were more spread out but centered near the truth.
