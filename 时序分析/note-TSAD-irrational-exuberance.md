## Issues

- Spurious Precision 

  > - A recent paper published an experiment on this dataset, giving results with 4 significant digits! 
  >
  > - This implies ludicrously fine distinctions are being made. However, I argue the results should be binary (*detected* | *not-detected*).
  >
  > - If the precision relates to timing, then it is making **a distinction down to 1/250th of a second**, something that is **medically impossible**. (Quote from Cardiologist Dr. Greg Mason “*No one could meaningfully label the onset with a precision greater than 1/10**th* *of a second*”)

- Ground-truth uncertainty > claimed increase

- Labels are not independent 

## Suggestions

- About 95% of papers on Time Series Anomaly Detection (TSAD) have one or more flaws. These flaws include:

- Testing on **deeply flawed datasets**

  - Trivial : could be solved in one-liner
  - Mislabeled
  - Unrealistic Anomaly Density 

  - Run-to failure
  - Unrealistic anomaly density

- Use of inappropriate measures of success
- Non-reproducible experiments
- Assuming Deep Learning is the answer and ignoring competitive decade-year-old methods 
  - ==**Time Series Discords**== 
  - ==**Matrix Profile**==
- Stabbing William of Ockham in the Heart -> unjustified complexity

- Not doing anomaly detection, but then calling it anomaly detection.