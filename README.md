# Google-Data-Analytics-Capstone-Case-Study-2
## Buisness Objective
Finding trends in smart device usage (for fitness purposes) of non-Bellabeat users that can help influence Bellabeat marketing strategy and growth.

#### Stakeholders:
The Key Stakeholders are:
- Urška Sršen: Bellabeat’s cofounder and Chief Creative Officer
- Sando Mur: Mathematician and Bellabeat’s cofounder; key member of the Bellabeat executive team
- Bellabeat marketing analytics team: A team of data analysts responsible for collecting, analyzing, and reporting data 
  that helps guide Bellabeat’s marketing strategy. You joined this team six months ago and have been busy learning about Bellabeat’’s 
  mission and business goals — as well as how you, as a junior data analyst, can help Bellabeat achieve them.

## Data Preparation
Dataset used is FitBit Fitness Tracker Data, made available via Mobius.
This Kaggle dataset contains information of 33users. These datasets were generated by respondents to a distributed
survey via Amazon Mechanical Turk between 03.12.2016-05.12.2016. Thirty three eligble Fitbit users consented to submission
of personal tracker data, including minute-level output for physical activity, heart rate, and sleep monitoring. Individual 
reports can be parsed by export session ID (column A) or timestamp (column B). Variation between output represents use of 
different types of Fitbit trackers and individual tracking behaviors / preferences.
It's in the form of csv.

The datasets are from 2016, so it may not accurately represent the current consumers.
Metadata is missing so it is not possible to confirm everything without a stakeholder.
	(example - TotalDistance value not having a proper metric like km or miles, 
	  	   value column in minuteSleep table not producing any context)

Changes made during data preparation (considering we cannot communicate with a stakeholder):
- '_merged' removed from file names because it doesn't add any context.
- Redundant datasets containing data already present in one of the dataset is not used (example - dailySteps, dailyCalories, dailyIntensities already in dailyActivity)
- minuteSleep table's value column doesn't produce any context so it is not used.
- sleepDay table contains information of only 24 users out of 33 users. So the analysis won't produce accurate conclusion and is hence discarded.
- weightLog table is inconsistent because every user didn't log their info (ignoring the factor of human error) so it is not considered
- Calorie is burned as the body uses energy, we have to distinguish between calorie burned through exercise and calorie burned through other 
day-to-day activities. Since total steps is taken into account, we are going to measure the amount of steps taken hourly as better indicator of 
exercise performed rather than by minutes. Hence only hourly tables are taken.
- The minuteMET table consists of large values usually not found in typical MET calculation. We don't know how the MET was calucalated. So it's not required.
So the tables taken for processing are dailyActivity, hourlySteps, hourlyCalories, and hourlyIntensities.

## Data Processing
User id consistency is checked. All contain info about 33 distinct users except sleepDay table (24 users) and heartrate_seconds table (14 users).
Since the 33 users is a sample representing overall fitbit users, sleepDay and heartrate_seconds table will cause inconsistent analysis. It is possible
that the other users didn't record that info into the respective tables. Also heartrate baseline is different for different people. so 80 bpm could be the
normal for some person or a result of physical activity for another person. Therefore heartrate_seconds table will not be considered during the final analysis.

minuteSteps, minuteCalories and minuteIntensities data is consistent with hourly tables so only hourly tables can be taken into consideration.
The hourly tables, that are, hourlySteps, hourlyIntensities, hourlySteps are therefore joined and used instead of minute tables.

For analysis - dailyActivity and hourlyCalories, hourlySteps, hourlyIntensities joined are taken into account.

## Data Visualization and Analysis
The following graphs are created using Tableau
- Calories Per Day 
- Sedantary Minutes vs Calories Burnt
- Steps, Intensity and Calorie Per Hour

The following conclusions can be drawn from each graph:
- People burn the most calorie on Tuesday and the rate drops throughout the week.
- The sedentary minutes seem to be correlated to calorie burnt.
- More calorie burnt effect seems to carry over to the next day. So more workout on one day compensates for the next day.

[Link to the tableau dashboard](https://public.tableau.com/app/profile/siddhartha.roy.chowdhury/viz/Book1_16357038602870/Dashboard1)

## Act / Recommendation

- The Bellabeat app could introduce rest days so the users could work every alternating day with more intensity. Since an intensive has its effect for a prolonged period of time, a HIIT type of workout every alternating day would be more beneficial to burn calories.
- Since people work out more only when the sedentary minutes are more as well, they lose out extra work benefit if the sedentary minutes were less. So they could be actively resting which will help Bellabeat users outperform other non-Bellabeat users. All of it could be instructed on the Bellabeat App and can be tracked through the Leaf bracelet or Time watch. 
