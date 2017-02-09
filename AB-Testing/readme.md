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

## Measuring Standard Deviation

**_Analytical Estimate of Standard Deviation_**
| Evaluation Metric | Standard Deviation |
|:-------------------:|:--------------------:|
| Gross Conversion  | .0202 |
| Retention         | .0549 |
| Net Conversion    | .0156 |

### Result Analysis

95% Confidence interval for the difference between the experiment and control group for evaluation metrics.

| Metric | dmin | Observed Difference | CI Lower Bound | CI Upper Bound | Result |
|:------:|:----------:|:----------:|:----------:|:-----------:|:------:|
| Gross Conversion | 0.01 | -0.0205 | -.0291 | -.0120 | Satistically and Practically Significant |
| Net Conversion | 0.0075 | -0.0048 | -0.0116 | 0.0019 | Neither Statistically nor Practically Significant |
