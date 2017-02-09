# A/B Testing to Determine an Effective Intervention to Decrease Early Udacity Course Cancellation

## Experiment Description

Udacity courses currently have two options on the home page: "start free trial", and "access course materials". If the student clicks "start free trial", they will be asked to enter their credit card information, and then they will be enrolled in a free trial for the paid version of the course. After 14 days, they will automatically be charged unless they cancel first. If the student clicks "access course materials", they will be able to view the videos and take the quizzes for free, but they will not receive coaching support or a verified certificate, and they will not submit their final project for feedback.

In the experiment, Udacity tested a change where if the student clicked "start free trial", they were asked how much time they had available to devote to the course. If the student indicated 5 or more hours per week, they would be taken through the checkout process as usual. If they indicated fewer than 5 hours per week, a message would appear indicating that Udacity courses usually require a greater time commitment for successful completion, and suggesting that the student might like to access the course materials for free.

## Experiment Design

### Metric Choice

The unit of diversion to control and experiment group is cookie, although once student enrolls in the free trial we track them by user-id since then. The same user-id can’t enroll in the free trial twice.
These are metrics available for us to use in the experiment. We need to select appropriate invariant metrics for sanity check and evaluation metrics to analyze experiment result. 

•	Number of cookies: That is, number of unique cookies to view the course overview page. (dmin=3000)

•	Number of user-ids: That is, number of users who enroll in the free trial. (dmin=50)

•	Number of clicks: That is, number of unique cookies to click the "Start free trial" button (which happens before the free trial screener is trigger). (dmin=240)

•	Click-through-probability: That is, number of unique cookies to click the "Start free trial" button divided by number of unique cookies to view the course overview page. (dmin=0.01)

•	Gross conversion: That is, number of user-ids to complete checkout and enroll in the free trial divided by number of unique cookies to click the "Start free trial" button. (dmin= 0.01)

•	Retention: That is, number of user-ids to remain enrolled past the 14-day boundary (and thus make at least one payment) divided by number of user-ids to complete checkout. (dmin=0.01)

•	Net conversion: That is, number of user-ids to remain enrolled past the 14-day boundary (and thus make at least one payment) divided by the number of unique cookies to click the "Start free trial" button. (dmin= 0.0075)

### Selected Metrics ###
_**Invariant Metrics:** number of cookies, number of clicks, click-through-probability_

_**Evaluation Metrics:** gross conversion, retention, net conversion_

### Invariant Metrics ###
Invariant metrics are metrics that shouldn’t change across control and experiment group. In this experiment, the experiment starts when that time question pops up. Therefore, any metrics that happen before this point could be considered as invariant metrics. 

**Number of cookies**: As this metric represents number of unique cookies to view the course overview page and we equally distribute traffic to control and experiment group, we can expect that this metric is invariant because this event happens before screener shows up.

**Number of clicks**: Number of unique cookie to click ‘Start free trial’ button shouldn’t change across control and experiment group because this event has not affected by screener. 

**Click-through-probability**: This metric is calculated by the number of clicks and the number of cookies. As these two metrics are invariant, we can conclude that Click-through-probability is invariant too. 

### Evaluation Metrics ###
Evaluation metrics are expected to change over the course of the experiment. By comparing differences between the control and experimental groups, we can measure the effect of the screener and test our hypothesis. Of the remaining metrics not considered to be invariant, user-id is excluded from the list of potential evaluation metrics. This is because user-id alone is a count, and gross conversion is a fraction that incorporates user-id while also offering a better way to track the effect of the screener. The evaluation metrics for this experiment are:

• Gross conversion rate (could measure whether or not the screener had an effect on enrollment)

• Retention rate (could measure whether or not the screener had an effect on the 14-day
dropout rate)

• Net conversion rate (could measure whether or not the screener had any effect on the 14-day completion rate, although not able to tell us where in this process)

If the hypothesis is correct, we would expect to see specific changes in the evaluation metrics. Gross conversion would be lower as those students likely to drop during the 14-day trial would be filtered by the screener. Retention rate would be higher as those likely to drop would not have enrolled, and those who enrolled would not be likely to drop. Last, net conversion would be unchanged as the amount of students to continue past the free trial and eventually complete the course would have been unaffected.

## Measuring Standard Deviation

Before conducting the experiment, data was collected to get daily values for cookies, enrollments, click through probability, gross conversion, retention, and net conversion on Udacity’s website. The data collected is referred to as the baseline.

In the experiment, we use 'default 5,000 cookies per day' approach in each group. From this, a rough estimate of the expected standard deviation for each evaluation metric can be calculated. First, to get an approximation of the number of clicks and enrollments for this daily sample of 5,000 cookies, we scale by the fraction of pageviews in the sample over the pageviews in the baseline.

Therefore, from 3,200 clicks and 660 enrollments in the baseline, we predict 400 clicks and 82.5 enrollments per day in the sample.
Theoretical standard deviation calculation is as followed:
```
+ Gross conversion: se = sqrt(0.20625*(1-0.20625)/3200) = 0.00715.
For 5000 pageviews, we have new_se = 0.00715 * sqrt(40000/5000) = 0.0202 
+ Retention: se = sqrt((0.53*(1-0.53)/660) = 0.0194
For 5000 pageviews, we have new_se = 0.0194 * sqrt(40000/5000) = 0.0549
+ Net conversion: se = sqrt(0.1093125*(1-0.1093125)/3200) = 0.0055159.
For 5000 pageviews, we have new_se = 0.0055 * sqrt(40000/5000) = 0.0156 
```
| Evaluation Metric | Standard Deviation |
|:-------------------:|:--------------------:|
| Gross Conversion  | .0202 |
| Retention         | .0549 |
| Net Conversion    | .0156 |

## Sizing

The following calcations are based on [baseline conversion data](data/baseline_vals.csv).

### Number of Samples vs. Power

A sample size calculator will give us the required number of samples for each evaluation metric. Each metric has it's own
unit of size (clicks or enrolls), so once we arrive at the required sample size, we need to scale from the given unit to pageviews by the ratio seen in the baseline. Pageviews required for each metric were calculated using an alpha value of 0.05 and beta value of 0.2.

| Metric | Baseline (%) | Dmin (%)| Alpha (%)| Power (%)| Sample size per Group | Total Pageviews |
|:------:|:----------:|:----------:|:----------:|:-----------:|:------:|:------:|
| Gross Conversion | 20.63 | 1.00 | 5.00 | 80.00 | 25,835 clicks | 645,875 |
| Retention        | 53.00 | 1.00 | 5.00 | 80.00 |39,115 enrollments | 4,741,213 |
| Net Conversion | 10.93 | 0.75 | 5.00 | 80.00 | 27,413 clicks | 685,325 |

Total pageviews required: 4,741,213 

### Duration vs. Exposure

Considering the required pageviews, an exposure can be specified based upon the risk of the experiment, and from this a duration can be calculated. The exposure is dependent upon the risk involved and because the screener is a mild reminder about time commitment, it constitutes minimal risk. None of the participants could suffer physical harm as a result of the experiment, nor is sensitive data being collected, therefore a 100% exposure is a safe. 

Dividing total pageviews by the number of pageviews per day in the baseline (40,000), gives us a duration of 119 days were Udacity to divert it’s entire traffic. This is too long of an experiment and we should reduce the duration. We can exclude retention as an evaluation metric and consider the next limiting metric, net conversion. With a revised 685,275 necessary pageviews, it takes about 18 days to run the experiment with 100% diversion and about 35 days with 50% diversion.  

## Experiment Analysis

The experimental data can be found in the following links:

- [experiment group](data/Final Project Results - Experiment.csv)
- [control group](data/Final Project Results - Control.csv)

### Sanity Checks

For invariant metrics we expect equal diversion into the experiment and control group.  We will test this at the 95% confidence interval.

| Metric | Expected Value | Observed Value | CI Lower Bound | CI Upper Bound | Result |
|:------:|:--------------:|:--------------:|:--------------:|:--------------:|:------:|
| Number of Cookies | 0.5000 | 0.5006 | 0.4988 | 0.5012 | Pass |
| Number of clicks on "start free trial" | 0.5000 | 0.5005 | 0.4959 | 0.5042 | Pass |
| Click-through-probability | 0.0821 | 0.0822 | 0.0812 | 0.0830 | Pass | 

###  Effect Size Tests
For each of your evaluation metrics, give a 95% confidence interval around the difference between the experiment and control groups. Indicate whether each metric is statistically and practically significant.

Gross Conversion:

|               | Control Group | Experiment|
| ------------- |:-------------:| -----:    |
| Clicks        | 17293 | 17260 |
| Enrolment     | 3785  | 3423  |
| Gross Conversion  | 0.2188746892    | 0.1983198146 |
```
SE = 0.004371675385
m = SE * 1.96 = 0.00856848375
Pooled Probability = 0.2086
D hat = -0.02055
Confidence Interval = [-0.0291,-0.0120]

```
Result:
```
Gross conversion CI: [-.0291, -.0120]
- statistically significant (CI doesn't contain zero)
- practically significant (CI doesn't contain d_min value)
```
Net Conversion:

|               | Control Group | Experiment|
| ------------- |:-------------:| -----:    |
| Clicks        | 17293 | 17260 |
| Enrolment     | 2033  | 1945  |
| Net Conversion  | 0.1175620193    | 0.1126882966 |
```
SE = 0.003434133513
m = SE * 1.96 = 0.0067
Pooled Probability = 0.2086
D hat = -0.0049
Confidence Interval = [-0.0116,-0.0018]
```
Result:
```
Net conversion CI: (-0.0116, 0.0018)
- not statistically significant (CI contains zero)
- not practically significant (CI contain d_min = +/- 0.0075)
```

### Sign Tests

| Metric | p-value for sign test | Statistically Significant @ alpha .05? |
|:------:|:--------------:|:--------------:|
| Gross Conversion | 0.0026 | Yes |
| Net Conversion | 0.6776 | No |


