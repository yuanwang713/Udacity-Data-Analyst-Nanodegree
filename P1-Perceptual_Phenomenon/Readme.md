#Project 1: Test a Perceptual Phenomenon
##Background information
In a Stroop task, participants are presented with a list of words, with each word displayed in a color of ink. The participant’s task is to say out loud the color of the ink in which the word is printed. The task has two conditions: a congruent words condition, and an incongruent words condition. In the congruent words condition, the words being displayed are color words whose names match the colors in which they are printed. In the incongruent words condition, the words displayed are color words whose names do not match the colors in which they are printed. In each case, we measure the time it takes to name the ink colors in equally-sized lists. Each participant will go through and record a time from each condition.

**Dataset:** [stroopdata.csv](stroopdata.csv)

##Questions for investigation

####1. What is our independent variable? What is our dependent variable?
**Dependent variable:** Response time from 24 participants.

**Independent variable:** Congruent or incongruent word list

####2. What is an appropriate set of hypotheses for this task? What kind of statistical test do you expect to perform?

**Hypothesis test**

**H<sub>0</sub>:** There is no difference in response time between viewing congruent & incongruent words

**H<sub>A</sub>:** here is significant difference in response time between viewing congruent & incongruent words

**Statistical test**

Because sample size is samller than 30, we can't use z-test as central limit theorm can't be applied here. The Dependent Samples t-Test is the appropriate statistical test as the same subjects are assigned two different conditions. The different conditions are dependent because, in theory, by doing the first test you have some practice doing it and you might have an unfair advantage due to this learning effect in doing the similar type of test second. In addition, we don't have any population parameters provided (so a z-test would not be appropriate here).



####3. Report some descriptive statistics regarding this dataset.

|	|Congruent | Incongruent|
|:----:|:-----:|:----:|
|count|24.000000	|24.000000|
|mean|	14.051125|	22.015917
|std	|3.559358	|4.797057
|min	|8.630000	|15.687000
|25%	|11.895250	|18.716750
|50%	|14.356500	|21.017500
|75%|	16.200750	|24.051500
|max	|22.328000|	35.255000


####4. Provide one or two visualizations that show the distribution of the sample data. Write one or two sentences noting what you observe about the plot or plots.

**Completion times of congruent and incongruent tasks**

![alt tag] (https://github.com/yuanwang713/Udacity-Data-Analyst-Nanodegree/blob/master/P1-Perceptual_Phenomenon/hist_congrent.png)

Congruent tasks appear to be consistently completed faster than incongruent tasks.

####5. What is your confidence level and your critical statistic value? Do you reject the null hypothesis or fail to reject it? Come to a conclusion in terms of the experiment task. Did the results match up with your expectations?
```
µD: -7.9648
S: 4.86482691
df: 23
t-stat: -8.020706944
at α 0.05, t-critical: -2.06865761; 2.06865761
P: 4.103E-08
95% CI: (-25.3527231, 9.42314)
```

**Null hypothesis rejected.** At α 0.05, the *time to name colours is significantly
different* between congruent and incongruent tasks. People do not name colours
at the same speed when the word’s meaning and its colour match, as when they
do not match. The result confirms my expectations.

####6. Optional: What do you think is responsible for the effects observed? Can you think of an alternative or similar task that would result in a similar effect?

The brain has an image association between the shape of the word and the colour. When there is a mismatch, additional time is necessary for the prefrontal cortex to process the information and decide on its meaning.

A similar effect would likely be observed if the participants were shown words of the correct colour but the wrong text. My hunch, however, is that the difference would be less pronounced as I’d expect the visual colour representation to be more ingrained in the brain that word shape associations.
