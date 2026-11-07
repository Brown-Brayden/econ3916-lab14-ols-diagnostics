# econ3916-lab14-ols-diagnostics
# OLS Diagnostics: When the Standard Error Is Lying

## Objective
I checked what happens to a regression's estimate and its standard error when the usual assumptions fail, and practised finding those failures in simulated and real data.

## Methodology
- Simulated errors whose spread grows with x and fitted the same regression with classical and with robust (HC3) standard errors.
- Ran 400 simulated samples to measure how often each 95% interval actually contained the true slope.
- Read four residual plots beside Breusch-Pagan and Jarque-Bera tests: a well-behaved control, heteroskedastic errors, a missing curve and an outlier.
- Measured leverage, standardised residuals and Cook's distance, then refitted without the most influential row.
- Fitted a California Housing regression with classical and HC3 standard errors and looked at the districts stuck at the $500,000 ceiling.
- Wrote a function, hc3_se(), that gives the HC3 standard error of any coefficient for any table and list of features.
- Compared classical, HC3 and firm-clustered standard errors on simulated workers who share a shock within each firm.
- Built a confounded regression that passes every diagnostic and still gets the slope wrong.

## Key Findings
- With heteroskedastic errors, both fits gave the same slope, 2.0147, but the standard error was 0.0264 classical and 0.0290 robust.
- Across 400 samples, the classical 95% interval covered the true slope in 91.8% of them and the robust one in 93.5% (Monte Carlo standard errors 1.4% and 1.2%). Only the classical shortfall was clearly more than chance.
- Deleting one outlier out of 600 rows moved the slope by 0.58 of its own standard error, but the standard error fell 33%. A single extreme residual mainly distorted the standard error, not the estimate.
- In California Housing, the HC3 standard error on AveRooms was 5.02 times the classical one.
- My hc3_se() function gave an HC3 standard error on AveRooms of 0.0121 with all districts and 0.0082 without the 965 at the 5.0 ceiling. A smaller standard error is not a reason to drop them.
- Five districts out of 20,640 carried 92% of the total Cook's distance.
- Clustering by firm made the standard error 3.14 times the classical one, because workers in the same firm share a shock.
- A regression of y on x that left out a confounder passed Breusch-Pagan (p = 0.36), Jarque-Bera (p = 0.66) and the Cook's distance check (largest 0.04), and still estimated a slope of 1.96 against a true 1.0. Diagnostics cannot detect a confounder.
