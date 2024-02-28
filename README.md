1. Business Understanding

1.1 Background Information
This project explores the behavior of drivers receiving location-based coupons on their phones. Through data exploration valuable insights are revealed into the factors driving coupon acceptance. This can allow companies to develop effective marketing and perhaps optimize the coupon dissemination strategies.
Data Source: UCI Machine Learning repository, collected via a survey on Amazon Mechanical Turk.
Data Format: Drivers were asked if they would accept a coupon for various businesses (restaurant, coffee house, bar).  The survey reported Yes and labeled Y = 1 if they would drive to coupon redemption location ‘right away’ or ‘later before the coupon expired. If not, then the response was labeled as No and labeled as Y = 0. Survey recorded driver’s background such as gender, age, marital status, children, education, occupation, income, and lifestyle. It also included driving contextual attributes such as destination, time, weather, passengers. 

1.2 Business Goals
Increase coupon redemption rates: Understand driver behavior to effectively target coupons to increase coupon acceptance rate.
Personalize coupon delivery: Identify factors influencing acceptance, so, businesses can target customer and situation to increase their valuation.

1.3 Key Questions
What factors influence coupon acceptance? This is the central question to help achieve the business goal. 
What driver profiles can be created from acceptance patterns? Segmenting customers based on their coupon acceptance likelihood can lead to effective targeted marketing.
Can the model be used to predict future coupon acceptance? This would allow to optimize their coupon distribution strategies.

1.4 Additional Considerations
Weather and time of day: These factors may influence behavior (e.g., seeking shelter during bad weather, accepting a coffee offer in the morning).
Passenger presence: The presence of a minor may affect willingness to visit a bar, while a family may be more interested in restaurant or coffee house offers.
Coupon type and value: Understanding preferences for different business categories and price ranges can inform future coupon design and pricing strategies.


2. Data understanding
In this section, we will gather, describe, and explore the data to make sure it fits the business goal. A data frame is created from which its data format and its quality is assessed. 

2.1 Data Formatting and Clean Up: The starting data frame has 12684 entries with 8 int64 and 18 object categories. 74 duplicate corresponding to 0.58 % of duplicate entries are dropped from the analysis. Around 6% of the entries have NaN that can be dropped during situational analysis. Dataframe is manipulated to make it more readable and further convert some object categories into integer format. 

2.2 Early Data Exploration: Of the 12610 observers 56.76% accepted the coupons which intuitively suggests near 50% acceptance rate building trust in the survey results. On average, ~57% of the drivers were driving alone, followed by 26% with friends and ~ 8% with partners and kids. 

![Stacked Histogram of Coupons Accepted or Rejected by Drivers](https://github.com/amsc1985/WillCustomerAcceptCoupon/assets/37163650/dca1d07b-9fa4-41d1-96e2-03d15e2a65b6)


The high-level insights are revealed from correlation heat maps from the modified dataframe. Coupon acceptance rate is highest for coffee house followed by restaurant bar and carry away.  

![Correlation of Driver Attribute and Driving Environment after data manipulation](https://github.com/amsc1985/WillCustomerAcceptCoupon/assets/37163650/30891b21-55e8-43fb-bf2b-7da223891d33)

Amongst the various coupons, the drivers accepted <$20 restaurant coupon the most irrespective of the temperature of the day. Particularly, higher coupons accepted during warmer days. In colder weather, take away coupons dominated. Drivers income bracket suggests interests in accepting both <$20 and between $20 - $50 coupons for restaurants.

![Histogram of Coupon Type by Temperature](https://github.com/amsc1985/WillCustomerAcceptCoupon/assets/37163650/57e1d731-b272-447e-8ffa-4098693c65bb)


3 Data Deep Drive for Bar and Carry out - Take away type Coupon Allotment  

  3.1 Behavior Assessment of Driver that accepted Bar Coupon
Of the 2010 observers who were given bar coupons 41.00% accepted the coupons but some of the Bar coupons are NaNs so we will ignore them from our analysis. Now of the 1989 observers who were given bar coupons 41.03% accepted the coupons
In order to profile the driver, that accepted the coupon, we want to evaluate if it is dependent on his lifestyle, or salary, or age or occupation. Assuming Bar Categories with index "0" or "<1" or "1~3" constitute to 3 or fewer bar visits. Acceptance rate for users that went to a bar <3 times a month based on all bar coupons allotment is 33.33 %. Contrast against 7.68% who went more than thrice. When considering the lifestyle of the drivers by comparing how often they visit the bar the acceptance rate increases to 37% and 77% for drivers that go to the bar fewer than or more than 3 times a month to the bar. If we ignore the drivers that visit the bar fewer than 3 times a month and have never been to the bar before then the acceptance rate increases to 52.8%. 

![Bar Graph of %Coupon Accepted by User](https://github.com/amsc1985/WillCustomerAcceptCoupon/assets/37163650/5b84366e-3d6e-495f-a5f4-c4271585a564)

The acceptance rate between drivers who go to bars more than once a month and had passengers that were not a kid and had occupations other than farming, fishing, or forestry is 71.2 %
Similar acceptance rate of drivers that go to bars more than once a month,  had passengers that were not a kid, and were not widowed is 71.2 %. The acceptance rate of drivers that go to bars more than once a month,  are under the age of 30 is 70.03 %
![Histogram with Coupon for 21 - 30 year Driver](https://github.com/amsc1985/WillCustomerAcceptCoupon/assets/37163650/111badbb-6d96-41b6-9a7e-ea84f1436910)

The acceptance rate of drivers that go to cheap restaurants more than 4 times a month and with income <50K is 45.72 %

![ Users go to Resturants  4 per month   Income  $50k](https://github.com/amsc1985/WillCustomerAcceptCoupon/assets/37163650/ce756d0b-def7-4768-806d-507e7fc8ce92)

In summary, the opportunity exists for the 23% habitual drinkers who go to the bar >3 times a month and around 50% for drivers who go to the bar <3 times a month. Profiling the driver over the age of 25 and within the age 21 – 25 with lifestyle involving visiting bar at least once a month have comparable acceptance rate of 71% and ~77% respectively. Acceptance rate of the drivers that go to the bar less than once a month tend to be lower than 20% 
ased on the data explored, potential hypotheses about drivers who are more likely to accept bar coupons are as follows:
Bar visitation frequency: Drivers who visit bars more frequently (more than 3 times a month) are more likely to accept bar coupons compared to those who visit less frequently (less than 3 times a month). This suggests that habitual bar-goers are a good target audience for bar coupon promotions. In partcular opportunity exists to attract unserved 23% habitual drinkers who go to the bar >3 times a month and around 50% for drivers who go to the bar <3 times a month.
Age and lifestyle: Drivers over 25 years old and those between 21-25 years old who visit bars at least once a month have comparable and high acceptance rates (71% - 77%) for bar coupons. This suggests that age may not be a significant factor as long as drivers have a bar-going lifestyle. Drivers who visit bars less (<20%) than once a month tend to have a lower acceptance rate for bar coupons, regardless of age.
Passenger demographics: The acceptance rate for drivers who visit bars more than once a month and have non-kid passengers and non-farming/fishing/forestry occupations is high (71.2%). This suggests these passenger demographics might not significantly influence coupon acceptance.Similarly, the acceptance rate for drivers who visit bars more than once a month, have non-kid passengers, and are not widowed is also high (71.2%). This further suggests that marital status might not be a major factor either.
Additional factors: Drivers who visit bars more than once a month and are under 30 years old have a slightly lower acceptance rate (70.03%) compared to other age groups with similar bar-going habits. This suggests age might play a role for a specific younger demographic. Drivers who visit cheap restaurants frequently (more than 4 times a month) and have an income below $50,000 have a relatively low acceptance rate (45.72%). This suggests these factors might be associated with a lower propensity to spend at bars even with coupons.


3.2 Behavior Assessment of Driver that accepted Carry out - Take away type Coupon

3.2.1. Income and coupon acceptance:

![Income Distribution of Drivers who accepted the coupon](https://github.com/amsc1985/WillCustomerAcceptCoupon/assets/37163650/7f3e75c7-f143-4550-8056-5d6e0c444e06)

There is a positive correlation between driver income and the acceptance rate of carry-out and take-away coupons for both married and single individuals. As the driver's income bracket increases, the percentage of coupons accepted also appears to increase for both groups.Overall, married partners seem to have a higher acceptance rate of carry-out and take-away coupons compared to single individuals across all income brackets. The lines representing married partners are consistently above the lines representing single individuals.

![Carry out   Take away Coupons Accepted by Married partner](https://github.com/amsc1985/WillCustomerAcceptCoupon/assets/37163650/5f6fbbfc-d84d-4e3c-872b-74f91bb807ec)


Income disparity in acceptance rate: The difference in coupon acceptance rate between married and single individuals appears to be larger for lower income brackets and gradually narrows down for higher income brackets. This suggests that the income disparity in coupon acceptance between married and single individuals might be more pronounced at lower income levels.
ased on the data explored, potential hypotheses about drivers who are more likely to accept bar coupons are as follows:

![Carry out   Take away Coupons Accepted by Entire Population](https://github.com/amsc1985/WillCustomerAcceptCoupon/assets/37163650/676e752c-470f-4e0f-a2a8-a7865ae95e2d)

Driver age and marital status trend for the entire population:
Coupon acceptance increases with driver age, across all marital statuses. The increase in coupon acceptance with age might be steeper for married partners and singles compared to divorced drivers.  
Across most age groups, married partners tend to have the highest coupon acceptance rate, followed by single drivers, and then divorced drivers. The difference in coupon acceptance rate between married partners and other groups appears to be larger at younger ages and gradually narrows as drivers get older. The gaps between the lines are larger at younger ages and become smaller at older ages.
Possible explanations is related to age and marital status.
Age: As people age, their preferences and spending habits might change. Older drivers might be more likely to value the convenience and potential savings offered by carry-out and take-away options, leading to a higher acceptance rate.
Marital status: Married couples might have different dining habits and financial considerations compared to single individuals or divorced individuals. They might be more likely to use coupons to save money on meals or to simplify meal planning.


Age and Coupon Acceptance: Coupon acceptance appears to increase with driver age across all passenger categories.  
Passenger Type and Coupon Acceptance: Drivers who transport family (kids) tend to accept more coupons compared to drivers who transport friends or who drive alone. Drivers who drive alone tend to have the lowest coupon acceptance rate across all age groups. The difference in coupon acceptance between drivers who transport family and those who transport friends appears to be larger at younger ages and gradually narrows as drivers get older. Hypothesis: 
Age: As people age, their preferences and spending habits might change. Older drivers might be more likely to value the convenience and potential savings offered by carry-out and take-away options, leading to a higher acceptance rate.
Passenger type: Drivers who transport families, especially those with children, might have different dining needs and preferences compared to those who drive alone or with friends. They might be more likely to use coupons to find convenient and budget-friendly meal options that cater to the whole family.


4 Summary

Drivers who were alone accepted most number of coupons in particular, for all categories cheaper restaurants coupons were well accepted. Almost 50% of the coupons were used within 2 hours when driver had some passenger company and were not alone. For the drivers that accepted bar coupons, the results suggest that bar visitation frequency and lifestyle (including age to some extent) are the most prominent factors influencing drivers' acceptance of bar coupons. Targeting drivers who visit bars frequently, regardless of their age (as long as they are above 21), seems like a promising strategy. However, further investigation into other factors like income, occupation, and passenger demographics might be necessary to refine the target audience for bar coupon promotions.
More coupons were accepted in a warmer weather. Drivers who transport alone or with friends have a similar average income. Drivers who transport kids or a partner have a higher average income than those who transport alone or with friends. 
There might not be a significant difference in income between drivers who transport kids and those who transport a partner. A possible association between passenger category and driver's income, with drivers who transport kids or a partner potentially having higher average income than those who transport alone or with friends.

For Bar coupons, results suggest that bar visitation frequency and lifestyle (including age to some extent) are the most prominent factors influencing drivers' acceptance of bar coupons. Targeting drivers who visit bars frequently, regardless of their age (as long as they are above 21), seems like a promising strategy. However, further investigation into other factors like income, occupation, and passenger demographics might be necessary to refine the target audience for bar coupon promotions.

For Carry out - Take away coupons, focus on drivers with higher income brackets: As their acceptance rate is generally higher, cater marketing efforts towards them.
Segment marketing campaigns based on marital status: Design separate campaigns for married and single individuals, considering their observed differences in coupon acceptance behavior. Emphasize different aspects of the coupons for each segment. 
For married couples, highlight might be the convenience and potential savings associated with carry-out and take-away options, which might be more relevant for families or busy schedules.
For single individuals, focus on the variety and affordability of dining options offered by the coupons, appealing to their potentially more price-sensitive preferences.

Overall, the graph suggests a possible association between passenger category and driver's income, with drivers who transport kids tending to have the highest average income and those who transport partners having the lowest. There may be a possible trend of decreasing income with increasing passenger category complexity based on the observation that the bars decrease in height from "Kid(s)" to "Partner".
In summary, A possible association between driver age, passenger type, and the acceptance rate of carry-out and take-away coupons. Drivers who transport families tend to have a higher coupon acceptance rate compared to those who transport friends or drive alone. Additionally, coupon acceptance seems to increase with driver age across all passenger categories.

