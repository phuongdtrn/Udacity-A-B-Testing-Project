# Udacity-A-B-Testing-Project

## Experiment Overview
At the time of this experiment, Udacity courses currently have two options on the course overview page: "start free trial", and "access course materials". If the student clicks "start free trial", they will be asked to enter their credit card information, and then they will be enrolled in a free trial for the paid version of the course. After 14 days, they will automatically be charged unless they cancel first. If the student clicks "access course materials", they will be able to view the videos and take the quizzes for free, but they will not receive coaching support or a verified certificate, and they will not submit their final project for feedback.

In the experiment, Udacity tested a change where if the student clicked "start free trial", they were asked how much time they had available to devote to the course. If the student indicated 5 or more hours per week, they would be taken through the checkout process as usual. If they indicated fewer than 5 hours per week, a message would appear indicating that Udacity courses usually require a greater time commitment for successful completion, and suggesting that the student might like to access the course materials for free. At this point, the student would have the option to continue enrolling in the free trial, or access the course materials for free instead.

The hypothesis was that this might set clearer expectations for students upfront, thus reducing the number of frustrated students who left the free trial because they didn't have enough time—without significantly reducing the number of students to continue past the free trial and eventually complete the course. If this hypothesis held true, Udacity could improve the overall student experience and improve coaches' capacity to support students who are likely to complete the course.

The unit of diversion is a cookie, although if the student enrolls in the free trial, they are tracked by user-id from that point forward. The same user-id cannot enroll in the free trial twice. For users that do not enroll, their user-id is not tracked in the experiment, even if they were signed in when they visited the course overview page.

## Experiment Design
###  Metric Choice
Invariant metrics:
- Number of cookies: That is, number of unique cookies to view the course overview page
- Number of clicks: That is, number of unique cookies to click the "Start free trial" button (which happens before the free trial screener is trigger).
- Click-through-probability: That is, number of unique cookies to click the "Start free trial" button divided by number of unique cookies to view the course overview page. Till the time the user clicks the "start free trial" button the user experience is same for all the users. Hence, we expect equal distribution in both the groups.

Evaluation metrics
- Gross conversion: That is, number of user-ids to complete checkout and enroll in the free trial divided by number of unique cookies to click the "Start free trial" button. (dmin= 0.01) -- Enrollments/Clicks
- Retention: That is, number of user-ids to remain enrolled past the 14-day boundary (and thus make at least one payment) divided by number of user-ids to complete checkout. (dmin= 0.01) 
- Net conversion: That is, number of user-ids to remain enrolled past the 14-day boundary (and thus make at least one payment) divided by the number of unique cookies to click the "Start free trial" button. (dmin= 0.0075) -- Payments/Clicks

<img width="658" alt="Screen Shot 2022-04-20 at 11 25 52 PM" src="https://user-images.githubusercontent.com/77939423/164372074-8e702b08-450f-4827-83d4-cd69a5286207.png">

With a total of 4,741,212 pageviews, it would take around 119 days to run the experiment, which is a really long time. As a result, we can use the second highest number of pageview, 685,325 instead. Therefore, we will run the experiment for 18 days.

### Sanity Check
We run a sanity check to check whether the invariant metrics are equivalent between the two groups. The total number of cookies in the control group and the experiment group should each make up 50% of the total number of cookies.

<img width="914" alt="Screen Shot 2022-04-20 at 11 41 59 PM" src="https://user-images.githubusercontent.com/77939423/164373570-e07e8645-ec72-45a8-a8a3-ddd26814cbb0.png">
The test passed sanity check if Observed_fraction > Lower_bound and Observed_fraction < Upper_bound

### Effect Size Test
Calculate the confidence interval for the difference between the control and experiment groups or the evaulation metrics with a 95% confidence interval.

A metric is statically or practically significant if:
- statistically significant: the confidence interval does not include 0
- practically significant: the confidence interval does not include the practical significance boundary
<img width="764" alt="Screen Shot 2022-04-20 at 11 49 51 PM" src="https://user-images.githubusercontent.com/77939423/164374369-bafce323-389b-4271-8e09-53e80beba745.png">

-> There is a difference in Gross Conversion between the two groups, while there is no difference in Net Conversion between the two groups

### Sign Test
Check whether the signs of the difference of the metrics between the experiment and control groups agree with the confidence interval of the difference.
<img width="369" alt="Screen Shot 2022-04-20 at 11 53 17 PM" src="https://user-images.githubusercontent.com/77939423/164374789-be624cab-73fc-45e2-9ff3-85684de1e3b5.png">

## Recommendations
The purpose of this experiment is to reduce the number of frustrated students who left the free trial because they didn't have enough time without significantly reducing the number of students to continue past the free trial and eventually complete the course. Based on the results, we can say that the free trial screener will reduce enrollment. However, there is not enough evidence that the screener will help encourage more students to make payment.

As a result, I would not recommend launching the screener. Udacity should run more follow-up experiments to gather enough evidence before incorporating this new feature.
