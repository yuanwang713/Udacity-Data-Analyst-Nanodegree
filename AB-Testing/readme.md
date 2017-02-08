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
