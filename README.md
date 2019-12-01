1: Introduction to Data Set

The purpose of this report to analyze of fatality rates in the U.S. using 2016CarCrashes.csv . This document contains data from the U.S. Department of Transportation’s Fatality Analysis Reporting System (FARS) in 2016. It has 21 conditions of traffic crashes and 51 rows which contains the data of the 50 states and district of Columbia.

1. State : State name of the U.S.
2. Population : Population of the State
3. Vehicle miles traveled (millions) : Total traveled miles of the State vehicles’(millions)
4. Fatal crashes : Total fatal crash number with vehicles
5. Deaths : Total death number with vehicle
6. Deaths per 100,000 population : Average crash death number of the state in every 100,000 population
7. Deaths per 100 million vehicle miles traveled : Avg. crash death number of the state in every 100 million traveled miles
8. Car occupants : Total number of car occupants in the crashes
9. Pickup and SUV occupants : Total number of Pickup and SUV occupants in the crashes
10. Large truck occupants : Total number of Large truck occupants in the crashes
11. Motorcyclists : Total number of Motorcyclists in the crashes
12. Pedestrians : Total number of Pedestrians in the crashes
13. Bicyclists : Total number of Bicyclists in the crashes
14. Unknown mode of transport : Total number of Unknown mode of transport in the crashes
15. Single-vehicle : Total number of Single-vehicle existence in the crashes
16. Multiple-vehicle : Total number of Multiple-vehicle existence in the crashes
17. Unrestrained fatally injured occupants : Total number of wearing seat-belt in the crashes
18. Restrained fatally injured occupants : Total number of not wearing seat-belt in the crashes
19. Unknown restraint status of fatally injured occupants : Total number of unknown seat-belt situation in the crashes
20. Urban : Total number of crashes in urban area
21. Rural : Total number of crashes in rural area
 
 
 
 
2: Data Analysis

(a) Descriptive data analysis

i. Numerical summaries:

A. 5-number summaries

District of Columbia has minimum values in most of variables such as Vehicle miles traveled (millions), Fatal crashes, Deaths, Car occupants, Pickup and SUV occupants, Large truck occupants, Motorcyclists, Single-vehicle, Multiple-vehicle, Restrained fatally injured occupants, Unrestrained fatally injured occupants, Rural.
Also, California has maximum values in most of variables such as Population, Vehicle miles traveled (millions), Car occupants, Pedestrians, Single-vehicle, Urban.
Firstly, we should check the data accuracy (step by step from data entry to missing values) for such patterns or abnormal min and max values far from the average. But in that case, we know that the data belongs to the government and these states look normal as demographically. California has high population(~40million) and District of Columbia has low population (~700,000) . We accept the data is true.
Additionally, we see that Texas has the highest Pickup and SUV occupants and Large truck occupants’ numbers in crashes. It seems to be a relation between big vehicles and Deaths rates. We will check it with regression analysis in the future.

B. Correlations

We calculate correlation except State column. Because it is character data.
Deaths and Fatal crashes have perfect correlation (1.00). Already we know that fatal crashes mean there is a death in the crash. So, we should take one of them out in the regression analysis. 
Deaths expectancy in crashes appears to have fairly strong positive relationship with all valuables. Our correlation coefficients have results between +0.839 and +1.
Deaths per 100,000 population (per capita) is an average death rate in every 100,000 people (100,000 * Death / Population). Hence, we don’t use both of them in the analysis. 
Deaths per 100 million vehicle miles traveled is an average death rate in every 100 million miles (100,000 * Death / Vehicle miles traveled (millions)). Hence, we don’t use both of them in an analysis. 
We have pretty high correlation between Car.occupants and Single.vehicle - Multiple.vehicle - Restrained.fatally.injured.occupants variables. 

C. Variance etc.

The highest variance is Population and the lowest is Deaths.per.100.million.vehicle.miles.traveled.
Texas has the highest and Michigan has the lowest Death value in the data.



ii. Graphical summaries:

A. Boxplots & B. Histograms

The shape of all the histograms (except Deaths.per.100.000.population) and the majority of boxplots show that the response variables are not normally distributed. The shapes of the histograms are right skewed. Hence, we apply log function to see if we can get normal distribution

C. Scatterplots

We can easily see CarData$Deaths.per.100.million.vehicle.miles.traveled don’t have linearity. There is linearity in some valuables for instance Car.occupants&Vehicle.miles.traveled..millions. , Car.occupants&Unrestrained.fatally.injured.occupants , Car.occupants&Restrained.fatally.injured.occupants


D. Barplots

Barplots are in the script file


(b) Determine the Best Predictive Model

i. Model Building

The fitted regression function: Y=b0+b1+b2+b3
Best fitted model is :  
Deaths.per.100.000.population = (71.9254) - (10.8533) * log(Vehicle.miles.traveled..millions.) + (5.0865) * log(Multiple.vehicle) + (5.8360) * log(Unrestrained.fatally.injured.occupants)


ii. t-tests

Exp1.  Analysis for rural - urban area crashes

We applied t-test for rural vs urban area to test whether two variables are statistically different.These variables are independent samples. Therefore, we did F test to find out if they are pooled or separate variances.   
H0 : σ1 = σ2   
H1 : σ1 ≠ σ2   
We reached that the p-value (0.3593) is greater than the significance level of 0.05. We fail to reject the null hypothesis that variance of the two samples are not significantly different. So, we use pooled variance to perform t-test for the difference in population means.   
H0 : μ1=μ2  
H1 : μ1≠μ2   
The p-value (0.602) is greater than the significance level 0.05. So, we fail to reject the null hypothesis that the two sample’s means are different. Urban area crashes and Rural area crashes are not statistically different.


Exp2.  Analysis for Single.vehicle - Multiple.vehicle crashes

We applied t-test for single.vehicle vs multiple.vehicle to test whether two variables are statistically different.
The p-value (0.3727) is greater than the significance level 0.05. We fail to reject the null hypothesis that variance of the two sample are not significantly different. So, we use pooled variance to perform t-test for the difference in population means.  
H0 : μ1=μ2   
H1 : μ1≠μ2   
The p-value (0.3524) is greater than the significance level 0.05. So, we fail to reject the null hypothesis that the two sample’s means are not significantly different. Single vehicle and Multiple vehicle crash rates are not statistically different.


Exp3.  We compare the difference of Occupants by using ONE-WAY ANOVA   

H₀: μ₁ = μ₂ = … = μκ   
H₁: At least one μ is different   
A one-way ANOVA was performed to compare the seven groups of Occupants. The p-value (2.2e-16) is smaller than the significance level 0.05. We reject the null hypothesis and conclude at least one group is different from the rest of the group mean. Post hoc Tukey test revealed that there were eleven significant differences between groups in 0.05 significant level:   
Large.truck.occupants-Car.occupants   
Motorcyclists-Car.occupants   
Pedestrians-Car.occupants   
Bicyclists-Car.occupants   
Unknown.mode.of.transport-Car.occupants   
Large.truck.occupants-Pickup.and.SUV.occupants   
Motorcyclists-Pickup.and.SUV.occupants   
Bicyclists-Pickup.and.SUV.occupants   
Unknown.mode.of.transport-Pickup.and.SUV.occupants   
Pedestrians-Large.truck.occupants   
Bicyclists-Pedestrians   


Exp4.  We compare the difference in Seatbelt by using ONE-WAY ANOVA
  
H₀: μ₁ = μ₂ = … = μκ      
H₁: At least one μ is different   
A one-way ANOVA was performed to compare the three groups of Seatbelt. (p-value (1.376e-06) < 0.05). We reject the null hypothesis and conclude at least one group is different from the rest of the group mean.
Post hoc Tukey test revealed that there were two significant differences between groups in 0.05 significant level. Unknown restraint status of fatally injured occupants is significantly different than other two group of values.


(c) Preform analysis of the best regression model   

#Multiple Linear Regression

i. Coefficients and model fit    
(Intercept)                                              71.925382   
log(Vehicle.miles.traveled..millions.)                  -10.853285                   
log(Multiple.vehicle)                                     5.086453                                          
log(Unrestrained.fatally.injured.occupants)               5.835983    

The fitted regression function: Y=b0+b1+b2+b3   
Best fitted model is :    
Deaths.per.100.000.population = (71.9254) - (10.8533) * log(Vehicle.miles.traveled..millions.) + (5.0865) * log(Multiple.vehicle) + (5.8360) * log(Unrestrained.fatally.injured.occupants)   
P-value (5.753e-16) of final regression model is lower than the α value (0.05). So, our model is statistically reliable.
AIC of the final model is 219.461. Since the R-square value is 0.7911, nearly 79% of the variation in the dependent variable is explained by the model.   
For one unit increase in Vehicle miles per one million, we get a (10.85/100) ~ 0.1 decrease in Death rate in 100,000 population. It means that when Vehicle miles increase 1 million, Death number decrease 10,000.    
For one unit increase in Multiple vehicle crashes, we get a (5.1/100) ~ 0.05 increase in Death rate in 100,000 population. It means that when Multiple vehicle crashes increase 1 unit, Death number increases 5,000.    
For one unit increase in Unrestrained occupants for vehicle crashes, we get a (5.8/100) ~ 0.06 increase in Death rate in 100,000 population. It means that when Unrestrained occupants increase 1 unit, Death number increases 6,000.   




ii. Model Diagnostics   

-Residuals vs Fitted graphic spreads randomly. It shows that the residuals are independent.   
-Normal QQ graphic spreads in a straight line. It shows that the residuals are normally distributed.   
-Standardized residuals graphic spreads randomly and have no visible pattern. It shows that the residuals are randomly scattered and have equal variance (homoscedasticity).   
-Residuals vs Leverage graphic has no variable above the 1 line (Cook Distance). There are no outliers anymore in the model.   
iii. Outliers / Influential values   
   
There was an outlier (9 and 44th value) in the first model and removed in the iterations for more stable regression model. There is no outlier in the final.model anymore .   

iv. Possible Remedial Measures Section   
There are non-normal distributed valuables in the first model and we applied variable transformation (log function) in the iterations.   



3: Interpret the results   
   
We analyzed the data from the U.S. Department of Transportation’s Fatality Analysis Reporting System (FARS) in 2016. This data has 21 conditions of traffic crashes and 51 rows which contains the data of the 50 states and district of Columbia.
We conclude that Texas and Columbia have different distribution than other states. We removed them while implementing our regression model. It needs to be investigated more when we have an insurance application from these states.
We saw that for one unit increase in Multiple vehicle crashes, we get a 5,000 increase in the number of people expected to die. For one unit increase in Unrestrained occupants for vehicle crashes, we get a 6,000 increase in the number of people expected to die. Additionally, Single vehicle and Multiple vehicle crash rates are not statistically different.   



4: Conclusion and recommendation   
   
Multiple vehicle crashes and not to wear a seatbelt increase the death rates dramatically. Obeying the traffic rules when driving is highly important from this perspective. Hence, we can install tracking device our clients’ vehicles to ensure they are obeying the rules all the time. We can adjust insurance payments by scoring their driving skills and habits. We can also make public service advertisements or be a sponsor for a health organization for drawing attention to these points. 
According to our report we identified that death rates decrease as the travel miles increased. This could be because of drivers improved their experience during their long travels assuming that vehicle ownership not changes. If this is the case, we can decrease their insurance payments, but we haven’t got enough data to identify root cause of this finding. 
Normally, we expect to have less crashes in rural area because of the less population and vehicle ownership. But we conclude it is not statistically different than urban area when we analyze it. The reason may be tough road conditions, lack of lightening, climatic conditions vs. There is no need to make any adjustment in the insurance for these subsets.   
