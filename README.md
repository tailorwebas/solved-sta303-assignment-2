Download Link: https://assignmentchef.com/product/solved-sta303-assignment-2
<br>






This assignment is worth 5% of your final grade. It is also intended as preparation for Test 2

(worth 20%) and your final exam, so making a good effort here can help you get up to 33% of your final grade. You will get your feedback on Assignment 2 before Test 2.

Submission is via Crowdmark NOT Quercus. You will receive an email from Crowdmark. Contact Head TA Crystal Chen (<a href="/cdn-cgi/l/email-protection" class="__cf_email__" data-cfemail="0b6863722568636e654b666a6267257e7f647964657f6425686a">[email protected]</a>) if you do not receive an email.

You should be able to do Question 1 by the end of week 4, Question 2 by the end of week 5 and Question 3 by the end of week 7.

<ul>

 <li><strong>Question 1 </strong>uses data about the IQ and language test scores for students in the netherlands, (school.csv). You will need to download this from the Assignment 2 Quercus page.</li>

 <li><strong>Question 2 </strong>uses <a href="http://pbrown.ca/teaching/303/data/smoke.RData">smoking data</a>, (smoking.RData) and instructions for obtaining the data are at the beginning of the question.</li>

 <li><strong>Question 3 </strong>uses Road accident data, (pedestrians.rds) and instructions for obtaining the data are at the beginning of the question.</li>

</ul>

<em>Note: You can use whatever packages are useful to you, i.e., tidyverse is not required if you prefer base R or something else. Just make sure you show which packages you are loading in a libraries chunk. Example code for this assignment is shown with tidyverse functions in the </em><em>sta303_Assignment2_example-code.Rmd file on the Assignment 2 Quercus page.</em>

<strong>Libraries used:</strong>

<strong>library</strong>(tidyverse)

<strong>install.packages</strong>(“Pmisc”, repos = “http://R-Forge.R-project.org”, type = “source”)

<h1>Question 1: Linear mixed models</h1>

The file school.csv (available on Quercus) contains data on 760 Grade 8 students (i.e., most are 11 years old) in 32 primary schools in the Netherlands. The data are adapted from Snijders and Boskers’ <em>Multilevel Analysis</em>, 2nd Edition (Sage, 2012).

Table 1: Variables in the school.csv data set

<table width="526">

 <tbody>

  <tr>

   <td width="127">Variable</td>

   <td width="399">Description</td>

  </tr>

  <tr>

   <td width="127">school</td>

   <td width="399">an ID number indicating which school the student attends</td>

  </tr>

  <tr>

   <td width="127">test</td>

   <td width="399">the student’s score on an end-of-year language test</td>

  </tr>

  <tr>

   <td width="127">iq</td>

   <td width="399">the student’s verbal IQ score</td>

  </tr>

  <tr>

   <td width="127">ses</td>

   <td width="399">the socioeconomic status of the student’s family</td>

  </tr>

  <tr>

   <td width="127">sex</td>

   <td width="399">the student’s sex</td>

  </tr>

  <tr>

   <td width="127">minority_status</td>

   <td width="399">1 if the student is an ethnic minority, 0 otherwise</td>

  </tr>

 </tbody>

</table>

<strong>Question of interest: Which variables are associated with Grade 8 students’ scores on an end-of-year language test?</strong>

<h2>Question 1a</h2>

Briefly describe why, without even looking at these data, you would have a concern about one of the assumptions of linear regression.

<h2>Question 1b</h2>

Create a scatter plot to examine the relationship between verbal IQ scores and end-of-year language scores. Include a line of best fit. Briefly describe what you see in the plot in the context of the question of interest.

<h2>Question 1c</h2>

Create two new variables in the data set, mean_ses that is the mean of ses for each school, and mean_iq that is mean of iq for each school.

<h2>Question 1d</h2>

Fit a linear model with test as the response and use iq, sex, ses, minority_status, mean_ses and mean_iq as the covariates. Show the code for the model you fit and the results of running summary() and confint() on the model you fit and briefly interpret the results. (A complete interpretation here should discuss what the intercept means, and for which subgroup of students it applies, as well as the location of the confidence intervals for each covariate, i.e. below 0, includes 0 or above zero. Address the question of interest.)

<h2>Question 1e</h2>

Fit a linear mixed model with the same fixed effects as 1c and with a random intercept for school.

Show the code for the model you fit and the results of running summary() and confint() on the model you fit and briefly interpret the results.

Hint 1: Consider the estimated standard deviations in the summary to make sure you understand the first two rows of the confint output.

Hint 2: If you want to suppress the ‘Computing profile confidence intervals …’ message you can use message=FALSE in the chunk.

<h2>Question 1f</h2>

Briefly describe similarities and differences between the coefficients of the fixed effects in the results from 1d and 1e and what causes the differences. You may wish to use the use summaries of the data to help you. See the example code document.

<h2>Question 1g</h2>

Plot the random effects for the different schools. Does it seem reasonable to have included these random effects?

<h2>Question 1h</h2>

Write a short paragraph summarising, what you have learned from this analysis. Focus on answering the question of interest. Remember that interpreting confidence intervals is preferred to point estimates and make sure any discussion of p-values and confidence intervals are statistically correct. Also mention what proportion of the residual variation, after fitting the fixed effects, the differences between schools accounts for.

<h1>Question 2: Generalised linear mixed models</h1>

Data from the 2014 American <a href="http://www.cdc.gov/tobacco/data_statistics/surveys/nyts/index.htm">National Youth Tobacco Survey</a> is available on <a href="http://pbrown.ca/teaching/303/data">http://pbro </a><a href="http://pbrown.ca/teaching/303/data">wn.ca/teaching/303/data</a>, where there is an R version of the 2014 dataset smoke.RData, a pdf documentation file 2014-Codebook.pdf, and the code used to create the R version of the data smokingData.R. You can obtain the data with:

smokeFile = “smokeDownload.RData” <strong>if </strong>(!<strong>file.exists</strong>(smokeFile)) { <strong>download.file</strong>(“http://pbrown.ca/teaching/303/data/smoke.RData”, smokeFile)

}

(<strong>load</strong>(smokeFile))

## [1] “smoke”    “smokeFormats”

The smoke object is a data.frame containing the data, the smokeFormats gives some explanation of the variables. The colName and label columns of smokeFormats contain variable names in smoke and descriptions respectively.

smokeFormats[smokeFormats[, “colName”] == “chewing_tobacco_snuff_or”, <strong>c</strong>(“colName”, “label”)]

##                  colName

## 151 chewing_tobacco_snuff_or

##                                                                label

## 151 RECODE: Used chewing tobacco, snuff, or dip on 1 or more days in the past 30 days

Consider the following model and set of results

<em># get rid of 9, 10 year olds and missing age and race </em>smokeSub = smoke[<strong>which</strong>(smoke$Age &gt; 10 &amp; !<strong>is.na</strong>(smoke$Race)),

] smokeSub$ageC = smokeSub$Age – 16

<strong>library</strong>(“glmmTMB”)

smokeModelT = <strong>glmmTMB</strong>(chewing_tobacco_snuff_or ~ ageC * Sex + RuralUrban + Race + (1 | state/school), data = smokeSub, family = <strong>binomial</strong>(link = “logit”)) knitr::<strong>kable</strong>(<strong>summary</strong>(smokeModelT)$coef$cond, digits = 2)

<table width="419">

 <tbody>

  <tr>

   <td width="135"></td>

   <td width="77">Estimate</td>

   <td width="87">Std. Error</td>

   <td width="63">z value</td>

   <td width="57">Pr(&gt;|z|)</td>

  </tr>

  <tr>

   <td width="135">(Intercept)</td>

   <td width="77">-3.08</td>

   <td width="87">0.17</td>

   <td width="63">-17.91</td>

   <td width="57">0.00</td>

  </tr>

  <tr>

   <td width="135">ageC</td>

   <td width="77">0.36</td>

   <td width="87">0.03</td>

   <td width="63">11.97</td>

   <td width="57">0.00</td>

  </tr>

  <tr>

   <td width="135">SexF</td>

   <td width="77">-2.04</td>

   <td width="87">0.13</td>

   <td width="63">-16.21</td>

   <td width="57">0.00</td>

  </tr>

  <tr>

   <td width="135">RuralUrbanRural</td>

   <td width="77">1.00</td>

   <td width="87">0.19</td>

   <td width="63">5.28</td>

   <td width="57">0.00</td>

  </tr>

  <tr>

   <td width="135">Raceblack</td>

   <td width="77">-1.53</td>

   <td width="87">0.19</td>

   <td width="63">-8.17</td>

   <td width="57">0.00</td>

  </tr>

  <tr>

   <td width="135">Racehispanic</td>

   <td width="77">-0.51</td>

   <td width="87">0.12</td>

   <td width="63">-4.29</td>

   <td width="57">0.00</td>

  </tr>

  <tr>

   <td width="135">Raceasian</td>

   <td width="77">-1.12</td>

   <td width="87">0.35</td>

   <td width="63">-3.16</td>

   <td width="57">0.00</td>

  </tr>

  <tr>

   <td width="135">Racenative</td>

   <td width="77">0.03</td>

   <td width="87">0.29</td>

   <td width="63">0.10</td>

   <td width="57">0.92</td>

  </tr>

  <tr>

   <td width="135">Racepacific</td>

   <td width="77">1.12</td>

   <td width="87">0.39</td>

   <td width="63">2.87</td>

   <td width="57">0.00</td>

  </tr>

  <tr>

   <td width="135">ageC:SexF</td>

   <td width="77">-0.33</td>

   <td width="87">0.06</td>

   <td width="63">-5.91</td>

   <td width="57">0.00</td>

  </tr>

 </tbody>

</table>

Table 3: Output of Pmisc::coefTable(smokeModelT)

<table width="290">

 <tbody>

  <tr>

   <td width="137"></td>

   <td width="44">est</td>

   <td width="54">2.5 %</td>

   <td width="54">97.5 %</td>

  </tr>

  <tr>

   <td width="137"><strong>ref prob</strong>M:Urban:white</td>

   <td width="44">0.04</td>

   <td width="54">0.03</td>

   <td width="54">0.06</td>

  </tr>

  <tr>

   <td width="137"><strong>ageC</strong></td>

   <td width="44">1.43</td>

   <td width="54">1.35</td>

   <td width="54">1.52</td>

  </tr>

  <tr>

   <td width="137"><strong>Sex </strong>F</td>

   <td width="44">0.13</td>

   <td width="54">0.10</td>

   <td width="54">0.17</td>

  </tr>

  <tr>

   <td width="137"><strong>RuralUrban </strong>Rural</td>

   <td width="44">2.72</td>

   <td width="54">1.88</td>

   <td width="54">3.95</td>

  </tr>

  <tr>

   <td width="137"><strong>Race</strong>black</td>

   <td width="44">0.22</td>

   <td width="54">0.15</td>

   <td width="54">0.31</td>

  </tr>

  <tr>

   <td width="137">hispanic</td>

   <td width="44">0.60</td>

   <td width="54">0.47</td>

   <td width="54">0.76</td>

  </tr>

  <tr>

   <td width="137">asian</td>

   <td width="44">0.33</td>

   <td width="54">0.16</td>

   <td width="54">0.65</td>

  </tr>

  <tr>

   <td width="137">native</td>

   <td width="44">1.03</td>

   <td width="54">0.58</td>

   <td width="54">1.82</td>

  </tr>

  <tr>

   <td width="137">pacific</td>

   <td width="44">3.07</td>

   <td width="54">1.43</td>

   <td width="54">6.60</td>

  </tr>

  <tr>

   <td width="137"><strong>ageC:Sex </strong>F</td>

   <td width="44">0.72</td>

   <td width="54">0.65</td>

   <td width="54">0.80</td>

  </tr>

  <tr>

   <td width="137"><strong>sd</strong>school:state</td>

   <td width="44">0.75</td>

   <td width="54">0.59</td>

   <td width="54">0.95</td>

  </tr>

  <tr>

   <td width="137">state</td>

   <td width="44">0.31</td>

   <td width="54">0.13</td>

   <td width="54">0.74</td>

  </tr>

 </tbody>

</table>

The results from this code are shown in fig. 1.

Pmisc::<strong>ranefPlot</strong>(smokeModelT, grpvar = “state”, level = 0.5, maxNames = 12)

Pmisc::<strong>ranefPlot</strong>(smokeModelT, grpvar = “school:state”, level = 0.5, maxNames = 12, xlim = <strong>c</strong>(-1, 2.2))

<h2>Question 2a</h2>

Write down a statistical model corresponding to smokeModelT. Briefly explain the difference between this model and a generalized linear model.

<h2>Question 2b</h2>

Briefly explain why this generalized linear mixed model with a logit link is more appropriate for this dataset than a linear mixed model.

<h2>Question 2c</h2>

Write a paragraph assessing the hypothesis that state-level differences in chewing tobacco usage amongst high school students are much larger than differences between schools within a state. If one was interested in identifying locations with many tobacco chewers (in order to

x

<ul>

 <li>state</li>

</ul>

x

<ul>

 <li>school</li>

</ul>

Figure 1: Conditional mean and 50pct prediction interval for random effects sell chewing tobacco to children, or if you prefer to implement programs to reduce tobacco chewing), would it be important to find individual schools with high chewing rates or would targeting those states where chewing is most common be sufficient?

<h1>Question 3: Death on the roads</h1>

The dataset below is a subset of the data from <a href="https://www.gov.uk/government/statistical-data-sets/ras30-reported-casualties-in-road-accidents">www.gov.uk/government/statistical-data</a><a href="https://www.gov.uk/government/statistical-data-sets/ras30-reported-casualties-in-road-accidents">sets/ras30-reported-casualties-in-road-accidents</a>, with all of the road traffic accidents in the UK from 1979 to 2015. The data below consist of all pedestrians involved in motor vehicle accidents with either fatal or slight injuries (pedestrians with moderate injuries have been removed).

<strong>dim</strong>(pedestrians)

## [1] 1159371    7

pedestrians[1:3, ]

##               time   age sex Casualty_Severity  Light_Conditions

<table width="640">

 <tbody>

  <tr>

   <td width="410">## 54 1979-01-01 22:40:00 26 – 35 Male</td>

   <td width="230">Slight Darkness – lights lit</td>

  </tr>

  <tr>

   <td width="410">## 65 1979-01-02 10:40:00 26 – 35 Male</td>

   <td width="230">Slight          Daylight</td>

  </tr>

  <tr>

   <td width="410">## 79 1979-01-02 14:25:00 46 – 55 Male##    Weather_Conditions   y## 54 Snowing no high winds FALSE ## 65 Raining no high winds FALSE## 79 Raining no high winds FALSE</td>

   <td width="230">Slight          Daylight</td>

  </tr>

 </tbody>

</table>

<strong>table</strong>(pedestrians$Casualty_Severity, pedestrians$sex)

##

##         Male Female

##   Slight 637919 481811 ## Fatal     24429 15212

<strong>range</strong>(pedestrians$time)

## [1] “1979-01-01 01:00:00 EST” “2015-12-31 23:35:00 EST”

Notice that men are involved in accidents more than women, and the proportion of accidents which are fatal is higher for men than for women. This might be due in part to women being more reluctant than men to walk outdoors late at night or in poor weather, and could also reflect men being on average more likely to engage in risky behaviour than women.

A glm adjusting for weather and light conditions is below.

theGlm = <strong>glm</strong>(y ~ sex + age + Light_Conditions + Weather_Conditions, data = pedestrians, family = <strong>binomial</strong>(link = “logit”)) knitr::<strong>kable</strong>(<strong>summary</strong>(theGlm)$coef, digits = 3)

<table width="627">

 <tbody>

  <tr>

   <td colspan="2" width="411">Estimate</td>

   <td colspan="3" width="96">Std. Error</td>

   <td width="63">z value</td>

   <td colspan="2" width="57">Pr(&gt;|z|)</td>

  </tr>

  <tr>

   <td width="354">(Intercept)</td>

   <td colspan="2" width="92">-4.177</td>

   <td width="52">0.020</td>

   <td colspan="3" width="94">-203.929</td>

   <td width="36">0.000</td>

  </tr>

  <tr>

   <td width="354">sexFemale</td>

   <td colspan="2" width="92">-0.275</td>

   <td width="52">0.011</td>

   <td colspan="3" width="94">-24.665</td>

   <td width="36">0.000</td>

  </tr>

  <tr>

   <td width="354">age0 – 5</td>

   <td colspan="2" width="92">0.186</td>

   <td width="52">0.032</td>

   <td colspan="3" width="94">5.831</td>

   <td width="36">0.000</td>

  </tr>

  <tr>

   <td width="354">age6 – 10</td>

   <td colspan="2" width="92">-0.357</td>

   <td width="52">0.030</td>

   <td colspan="3" width="94">-12.030</td>

   <td width="36">0.000</td>

  </tr>

  <tr>

   <td width="354">age11 – 15</td>

   <td colspan="2" width="92">-0.504</td>

   <td width="52">0.029</td>

   <td colspan="3" width="94">-17.668</td>

   <td width="36">0.000</td>

  </tr>

  <tr>

   <td width="354">age16 – 20</td>

   <td colspan="2" width="92">-0.338</td>

   <td width="52">0.027</td>

   <td colspan="3" width="94">-12.298</td>

   <td width="36">0.000</td>

  </tr>

  <tr>

   <td width="354">age21 – 25</td>

   <td colspan="2" width="92">-0.159</td>

   <td width="52">0.029</td>

   <td colspan="3" width="94">-5.457</td>

   <td width="36">0.000</td>

  </tr>

  <tr>

   <td width="354">age36 – 45</td>

   <td colspan="2" width="92">0.324</td>

   <td width="52">0.027</td>

   <td colspan="3" width="94">12.213</td>

   <td width="36">0.000</td>

  </tr>

  <tr>

   <td width="354">age46 – 55</td>

   <td colspan="2" width="92">0.660</td>

   <td width="52">0.026</td>

   <td colspan="3" width="94">25.030</td>

   <td width="36">0.000</td>

  </tr>

  <tr>

   <td width="354">age56 – 65</td>

   <td colspan="2" width="92">1.138</td>

   <td width="52">0.025</td>

   <td colspan="3" width="94">45.355</td>

   <td width="36">0.000</td>

  </tr>

  <tr>

   <td width="354">age66 – 75</td>

   <td colspan="2" width="92">1.760</td>

   <td width="52">0.023</td>

   <td colspan="3" width="94">75.234</td>

   <td width="36">0.000</td>

  </tr>

  <tr>

   <td width="354">ageOver 75</td>

   <td colspan="2" width="92">2.328</td>

   <td width="52">0.022</td>

   <td colspan="3" width="94">104.302</td>

   <td width="36">0.000</td>

  </tr>

  <tr>

   <td width="354">Light_ConditionsDarkness – lights lit</td>

   <td colspan="2" width="92">0.995</td>

   <td width="52">0.012</td>

   <td colspan="3" width="94">81.220</td>

   <td width="36">0.000</td>

  </tr>

  <tr>

   <td width="354">Light_ConditionsDarkness – lights unlit</td>

   <td colspan="2" width="92">1.176</td>

   <td width="52">0.052</td>

   <td colspan="3" width="94">22.415</td>

   <td width="36">0.000</td>

  </tr>

  <tr>

   <td width="354">Light_ConditionsDarkness – no lighting</td>

   <td colspan="2" width="92">2.765</td>

   <td width="52">0.021</td>

   <td colspan="3" width="94">131.303</td>

   <td width="36">0.000</td>

  </tr>

  <tr>

   <td width="354">Light_ConditionsDarkness – lighting unknown</td>

   <td colspan="2" width="92">0.259</td>

   <td width="52">0.068</td>

   <td colspan="3" width="94">3.788</td>

   <td width="36">0.000</td>

  </tr>

  <tr>

   <td width="354">Weather_ConditionsRaining no high winds</td>

   <td colspan="2" width="92">-0.214</td>

   <td width="52">0.017</td>

   <td colspan="3" width="94">-12.957</td>

   <td width="36">0.000</td>

  </tr>

  <tr>

   <td width="354">Weather_ConditionsSnowing no high winds</td>

   <td colspan="2" width="92">-0.751</td>

   <td width="52">0.092</td>

   <td colspan="3" width="94">-8.136</td>

   <td width="36">0.000</td>

  </tr>

  <tr>

   <td width="354">Weather_ConditionsFine + high winds</td>

   <td colspan="2" width="92">0.175</td>

   <td width="52">0.037</td>

   <td colspan="3" width="94">4.774</td>

   <td width="36">0.000</td>

  </tr>

  <tr>

   <td width="354">Weather_ConditionsRaining + high winds</td>

   <td colspan="2" width="92">-0.066</td>

   <td width="52">0.040</td>

   <td colspan="3" width="94">-1.648</td>

   <td width="36">0.099</td>

  </tr>

  <tr>

   <td width="354">Weather_ConditionsSnowing + high winds</td>

   <td colspan="2" width="92">-0.550</td>

   <td width="52">0.172</td>

   <td colspan="3" width="94">-3.193</td>

   <td width="36">0.001</td>

  </tr>

  <tr>

   <td width="354">Weather_ConditionsFog or mist</td>

   <td colspan="2" width="92">0.069</td>

   <td width="52">0.069</td>

   <td colspan="3" width="94">0.989</td>

   <td width="36">0.323</td>

  </tr>

  <tr>

   <td colspan="7" width="591">Here’s another GLM with interactions.theGlmInt = <strong>glm</strong>(y ~ sex * age + Light_Conditions + Weather_Conditions, data = pedestrians, family = <strong>binomial</strong>(link = “logit”))knitr::<strong>kable</strong>(<strong>summary</strong>(theGlmInt)$coef, digits = 3)</td>

   <td width="36"></td>

  </tr>

  <tr>

   <td width="354"></td>

   <td width="57"></td>

   <td width="36"></td>

   <td width="52"></td>

   <td width="9"></td>

   <td width="63"></td>

   <td width="21"></td>

   <td width="36"></td>

  </tr>

 </tbody>

</table>

Estimate      Std. Error       z value      Pr(&gt;|z|)

<table width="627">

 <tbody>

  <tr>

   <td width="314">(Intercept)</td>

   <td width="97">-4.103</td>

   <td width="87">0.023</td>

   <td width="72">-179.887</td>

   <td width="57">0.000</td>

  </tr>

  <tr>

   <td width="314">sexFemale</td>

   <td width="97">-0.545</td>

   <td width="87">0.044</td>

   <td width="72">-12.425</td>

   <td width="57">0.000</td>

  </tr>

  <tr>

   <td width="314">age0 – 5</td>

   <td width="97">0.021</td>

   <td width="87">0.039</td>

   <td width="72">0.544</td>

   <td width="57">0.587</td>

  </tr>

  <tr>

   <td width="314">age6 – 10</td>

   <td width="97">-0.460</td>

   <td width="87">0.035</td>

   <td width="72">-13.105</td>

   <td width="57">0.000</td>

  </tr>

  <tr>

   <td width="314">age11 – 15</td>

   <td width="97">-0.582</td>

   <td width="87">0.035</td>

   <td width="72">-16.625</td>

   <td width="57">0.000</td>

  </tr>

  <tr>

   <td width="314">age16 – 20</td>

   <td width="97">-0.369</td>

   <td width="87">0.032</td>

   <td width="72">-11.461</td>

   <td width="57">0.000</td>

  </tr>

  <tr>

   <td width="314">age21 – 25</td>

   <td width="97">-0.149</td>

   <td width="87">0.033</td>

   <td width="72">-4.501</td>

   <td width="57">0.000</td>

  </tr>

  <tr>

   <td width="314">age36 – 45</td>

   <td width="97">0.322</td>

   <td width="87">0.031</td>

   <td width="72">10.508</td>

   <td width="57">0.000</td>

  </tr>

  <tr>

   <td width="314">age46 – 55</td>

   <td width="97">0.656</td>

   <td width="87">0.031</td>

   <td width="72">21.281</td>

   <td width="57">0.000</td>

  </tr>

  <tr>

   <td width="314">age56 – 65</td>

   <td width="97">1.075</td>

   <td width="87">0.030</td>

   <td width="72">35.727</td>

   <td width="57">0.000</td>

  </tr>

  <tr>

   <td width="314">age66 – 75</td>

   <td width="97">1.622</td>

   <td width="87">0.029</td>

   <td width="72">56.315</td>

   <td width="57">0.000</td>

  </tr>

  <tr>

   <td width="314">ageOver 75</td>

   <td width="97">2.180</td>

   <td width="87">0.027</td>

   <td width="72">79.597</td>

   <td width="57">0.000</td>

  </tr>

  <tr>

   <td width="314">Light_ConditionsDarkness – lights lit</td>

   <td width="97">0.990</td>

   <td width="87">0.012</td>

   <td width="72">80.676</td>

   <td width="57">0.000</td>

  </tr>

 </tbody>

</table>

Figure 2: Predicted probability of being a case in baseline conditions (daylight, fine no wind) with 99% CI using theGlmInt

<table width="627">

 <tbody>

  <tr>

   <td width="334"></td>

   <td width="77">Estimate</td>

   <td width="92">Std. Error</td>

   <td width="67">z value</td>

   <td width="57">Pr(&gt;|z|)</td>

  </tr>

  <tr>

   <td width="334">Light_ConditionsDarkness – lights unlit</td>

   <td width="77">1.174</td>

   <td width="92">0.052</td>

   <td width="67">22.399</td>

   <td width="57">0.000</td>

  </tr>

  <tr>

   <td width="334">Light_ConditionsDarkness – no lighting</td>

   <td width="77">2.746</td>

   <td width="92">0.021</td>

   <td width="67">130.165</td>

   <td width="57">0.000</td>

  </tr>

  <tr>

   <td width="334">Light_ConditionsDarkness – lighting unknown</td>

   <td width="77">0.257</td>

   <td width="92">0.068</td>

   <td width="67">3.759</td>

   <td width="57">0.000</td>

  </tr>

  <tr>

   <td width="334">Weather_ConditionsRaining no high winds</td>

   <td width="77">-0.211</td>

   <td width="92">0.017</td>

   <td width="67">-12.764</td>

   <td width="57">0.000</td>

  </tr>

  <tr>

   <td width="334">Weather_ConditionsSnowing no high winds</td>

   <td width="77">-0.746</td>

   <td width="92">0.092</td>

   <td width="67">-8.075</td>

   <td width="57">0.000</td>

  </tr>

  <tr>

   <td width="334">Weather_ConditionsFine + high winds</td>

   <td width="77">0.176</td>

   <td width="92">0.037</td>

   <td width="67">4.803</td>

   <td width="57">0.000</td>

  </tr>

  <tr>

   <td width="334">Weather_ConditionsRaining + high winds</td>

   <td width="77">-0.062</td>

   <td width="92">0.040</td>

   <td width="67">-1.545</td>

   <td width="57">0.122</td>

  </tr>

  <tr>

   <td width="334">Weather_ConditionsSnowing + high winds</td>

   <td width="77">-0.548</td>

   <td width="92">0.172</td>

   <td width="67">-3.189</td>

   <td width="57">0.001</td>

  </tr>

  <tr>

   <td width="334">Weather_ConditionsFog or mist</td>

   <td width="77">0.065</td>

   <td width="92">0.069</td>

   <td width="67">0.943</td>

   <td width="57">0.346</td>

  </tr>

  <tr>

   <td width="334">sexFemale:age0 – 5</td>

   <td width="77">0.546</td>

   <td width="92">0.068</td>

   <td width="67">7.970</td>

   <td width="57">0.000</td>

  </tr>

  <tr>

   <td width="334">sexFemale:age6 – 10</td>

   <td width="77">0.367</td>

   <td width="92">0.066</td>

   <td width="67">5.606</td>

   <td width="57">0.000</td>

  </tr>

  <tr>

   <td width="334">sexFemale:age11 – 15</td>

   <td width="77">0.285</td>

   <td width="92">0.062</td>

   <td width="67">4.603</td>

   <td width="57">0.000</td>

  </tr>

  <tr>

   <td width="334">sexFemale:age16 – 20</td>

   <td width="77">0.150</td>

   <td width="92">0.062</td>

   <td width="67">2.408</td>

   <td width="57">0.016</td>

  </tr>

  <tr>

   <td width="334">sexFemale:age21 – 25</td>

   <td width="77">-0.041</td>

   <td width="92">0.069</td>

   <td width="67">-0.596</td>

   <td width="57">0.551</td>

  </tr>

  <tr>

   <td width="334">sexFemale:age36 – 45</td>

   <td width="77">0.029</td>

   <td width="92">0.062</td>

   <td width="67">0.475</td>

   <td width="57">0.635</td>

  </tr>

  <tr>

   <td width="334">sexFemale:age46 – 55</td>

   <td width="77">0.059</td>

   <td width="92">0.060</td>

   <td width="67">0.976</td>

   <td width="57">0.329</td>

  </tr>

  <tr>

   <td width="334">sexFemale:age56 – 65</td>

   <td width="77">0.246</td>

   <td width="92">0.056</td>

   <td width="67">4.417</td>

   <td width="57">0.000</td>

  </tr>

  <tr>

   <td width="334">sexFemale:age66 – 75</td>

   <td width="77">0.406</td>

   <td width="92">0.052</td>

   <td width="67">7.877</td>

   <td width="57">0.000</td>

  </tr>

  <tr>

   <td width="334">sexFemale:ageOver 75</td>

   <td width="77">0.411</td>

   <td width="92">0.049</td>

   <td width="67">8.348</td>

   <td width="57">0.000</td>

  </tr>

 </tbody>

</table>

Table 6: Odds ratios for theGlm and theGlmInt.

<table width="559">

 <tbody>

  <tr>

   <td rowspan="2" width="238"></td>

   <td rowspan="2" width="52">est</td>

   <td rowspan="2" width="52"><strong>model 1</strong>2.5</td>

   <td rowspan="2" width="68">97.5</td>

   <td width="39"></td>

   <td colspan="2" width="110"><strong>model 2</strong></td>

  </tr>

  <tr>

   <td width="39">est</td>

   <td width="65">2.5</td>

   <td width="44">97.5</td>

  </tr>

  <tr>

   <td width="238"><strong>ref prob</strong>Male:26 – 35:Daylight:Fine no</td>

   <td width="52">0.02</td>

   <td width="52">0.01</td>

   <td width="68">0.02</td>

   <td width="39">0.02</td>

   <td width="65">0.02</td>

   <td width="44">0.02</td>

  </tr>

  <tr>

   <td width="238"><strong>sex</strong>Female</td>

   <td width="52">0.76</td>

   <td width="52">0.74</td>

   <td width="68">0.78</td>

   <td width="39">0.58</td>

   <td width="65">0.53</td>

   <td width="44">0.63</td>

  </tr>

  <tr>

   <td width="238"><strong>age</strong>0 – 5</td>

   <td width="52">1.20</td>

   <td width="52">1.13</td>

   <td width="68">1.28</td>

   <td width="39">1.02</td>

   <td width="65">0.95</td>

   <td width="44">1.10</td>

  </tr>

  <tr>

   <td width="238">11 – 15</td>

   <td width="52">0.60</td>

   <td width="52">0.57</td>

   <td width="68">0.64</td>

   <td width="39">0.56</td>

   <td width="65">0.52</td>

   <td width="44">0.60</td>

  </tr>

  <tr>

   <td width="238">16 – 20</td>

   <td width="52">0.71</td>

   <td width="52">0.68</td>

   <td width="68">0.75</td>

   <td width="39">0.69</td>

   <td width="65">0.65</td>

   <td width="44">0.74</td>

  </tr>

  <tr>

   <td width="238">21 – 25</td>

   <td width="52">0.85</td>

   <td width="52">0.81</td>

   <td width="68">0.90</td>

   <td width="39">0.86</td>

   <td width="65">0.81</td>

   <td width="44">0.92</td>

  </tr>

  <tr>

   <td width="238">36 – 45</td>

   <td width="52">1.38</td>

   <td width="52">1.31</td>

   <td width="68">1.46</td>

   <td width="39">1.38</td>

   <td width="65">1.30</td>

   <td width="44">1.47</td>

  </tr>

  <tr>

   <td width="238">46 – 55</td>

   <td width="52">1.93</td>

   <td width="52">1.84</td>

   <td width="68">2.04</td>

   <td width="39">1.93</td>

   <td width="65">1.81</td>

   <td width="44">2.05</td>

  </tr>

  <tr>

   <td width="238">56 – 65</td>

   <td width="52">3.12</td>

   <td width="52">2.97</td>

   <td width="68">3.28</td>

   <td width="39">2.93</td>

   <td width="65">2.76</td>

   <td width="44">3.11</td>

  </tr>

  <tr>

   <td width="238">6 – 10</td>

   <td width="52">0.70</td>

   <td width="52">0.66</td>

   <td width="68">0.74</td>

   <td width="39">0.63</td>

   <td width="65">0.59</td>

   <td width="44">0.68</td>

  </tr>

  <tr>

   <td width="238">66 – 75</td>

   <td width="52">5.81</td>

   <td width="52">5.55</td>

   <td width="68">6.08</td>

   <td width="39">5.06</td>

   <td width="65">4.78</td>

   <td width="44">5.36</td>

  </tr>

  <tr>

   <td width="238">Over 75</td>

   <td width="52">10.26</td>

   <td width="52">9.82</td>

   <td width="68">10.71</td>

   <td width="39">8.84</td>

   <td width="65">8.38</td>

   <td width="44">9.33</td>

  </tr>

  <tr>

   <td width="238"><strong>Light Conditions</strong>Darkness – lighting unknown</td>

   <td width="52">1.30</td>

   <td width="52">1.13</td>

   <td width="68">1.48</td>

   <td width="39">1.29</td>

   <td width="65">1.13</td>

   <td width="44">1.48</td>

  </tr>

  <tr>

   <td width="238">Darkness – lights lit</td>

   <td width="52">2.70</td>

   <td width="52">2.64</td>

   <td width="68">2.77</td>

   <td width="39">2.69</td>

   <td width="65">2.63</td>

   <td width="44">2.76</td>

  </tr>

  <tr>

   <td width="238">Darkness – lights unlit</td>

   <td width="52">3.24</td>

   <td width="52">2.92</td>

   <td width="68">3.59</td>

   <td width="39">3.23</td>

   <td width="65">2.92</td>

   <td width="44">3.58</td>

  </tr>

  <tr>

   <td width="238">Darkness – no lighting</td>

   <td width="52">15.89</td>

   <td width="52">15.24</td>

   <td width="68">16.56</td>

   <td width="39">15.58</td>

   <td width="65">14.95</td>

   <td width="44">16.24</td>

  </tr>

  <tr>

   <td width="238"><strong>Weather Conditions </strong>Fine + high winds</td>

   <td width="52">1.19</td>

   <td width="52">1.11</td>

   <td width="68">1.28</td>

   <td width="39">1.19</td>

   <td width="65">1.11</td>

   <td width="44">1.28</td>

  </tr>

  <tr>

   <td width="238">Fog or mist</td>

   <td width="52">1.07</td>

   <td width="52">0.93</td>

   <td width="68">1.23</td>

   <td width="39">1.07</td>

   <td width="65">0.93</td>

   <td width="44">1.22</td>

  </tr>

  <tr>

   <td width="238">Raining + high winds</td>

   <td width="52">0.94</td>

   <td width="52">0.87</td>

   <td width="68">1.01</td>

   <td width="39">0.94</td>

   <td width="65">0.87</td>

   <td width="44">1.02</td>

  </tr>

  <tr>

   <td width="238">Raining no high winds</td>

   <td width="52">0.81</td>

   <td width="52">0.78</td>

   <td width="68">0.83</td>

   <td width="39">0.81</td>

   <td width="65">0.78</td>

   <td width="44">0.84</td>

  </tr>

  <tr>

   <td width="238">Snowing + high winds</td>

   <td width="52">0.58</td>

   <td width="52">0.41</td>

   <td width="68">0.81</td>

   <td width="39">0.58</td>

   <td width="65">0.41</td>

   <td width="44">0.81</td>

  </tr>

  <tr>

   <td width="238">Snowing no high winds</td>

   <td width="52">0.47</td>

   <td width="52">0.39</td>

   <td width="68">0.57</td>

   <td width="39">0.47</td>

   <td width="65">0.40</td>

   <td width="44">0.57</td>

  </tr>

  <tr>

   <td width="238"><strong>sex:age</strong>Female:0 – 5</td>

   <td width="52"></td>

   <td width="52"></td>

   <td width="68"></td>

   <td width="39">1.73</td>

   <td width="65">1.51</td>

   <td width="44">1.97</td>

  </tr>

  <tr>

   <td width="238">Female:11 – 15</td>

   <td width="52"></td>

   <td width="52"></td>

   <td width="68"></td>

   <td width="39">1.33</td>

   <td width="65">1.18</td>

   <td width="44">1.50</td>

  </tr>

  <tr>

   <td width="238">Female:16 – 20</td>

   <td width="52"></td>

   <td width="52"></td>

   <td width="68"></td>

   <td width="39">1.16</td>

   <td width="65">1.03</td>

   <td width="44">1.31</td>

  </tr>

  <tr>

   <td width="238">Female:21 – 25</td>

   <td width="52"></td>

   <td width="52"></td>

   <td width="68"></td>

   <td width="39">0.96</td>

   <td width="65">0.84</td>

   <td width="44">1.10</td>

  </tr>

  <tr>

   <td width="238">Female:36 – 45</td>

   <td width="52"></td>

   <td width="52"></td>

   <td width="68"></td>

   <td width="39">1.03</td>

   <td width="65">0.91</td>

   <td width="44">1.16</td>

  </tr>

  <tr>

   <td width="238">Female:46 – 55</td>

   <td width="52"></td>

   <td width="52"></td>

   <td width="68"></td>

   <td width="39">1.06</td>

   <td width="65">0.94</td>

   <td width="44">1.19</td>

  </tr>

  <tr>

   <td width="238">Female:56 – 65</td>

   <td width="52"></td>

   <td width="52"></td>

   <td width="68"></td>

   <td width="39">1.28</td>

   <td width="65">1.15</td>

   <td width="44">1.43</td>

  </tr>

  <tr>

   <td width="238">Female:6 – 10</td>

   <td width="52"></td>

   <td width="52"></td>

   <td width="68"></td>

   <td width="39">1.44</td>

   <td width="65">1.27</td>

   <td width="44">1.64</td>

  </tr>

  <tr>

   <td width="238">Female:66 – 75</td>

   <td width="52"></td>

   <td width="52"></td>

   <td width="68"></td>

   <td width="39">1.50</td>

   <td width="65">1.36</td>

   <td width="44">1.66</td>

  </tr>

  <tr>

   <td width="238">Female:Over 75</td>

   <td width="52"></td>

   <td width="52"></td>

   <td width="68"></td>

   <td width="39">1.51</td>

   <td width="65">1.37</td>

   <td width="44">1.66</td>

  </tr>

 </tbody>

</table>

<h2>Question 3a</h2>

Write a short paragraph describing a case/control model (not the results) corresponding the theGlm and theGlmInt objects. Be sure to specify the case definition and the control group, and what the covariates are.

<h2>Question 3b</h2>

Write a short report assessing whether the UK road accident data are consistent with the hypothesis that women tend to be, on average, safer as pedestrians than men, particularly as teenagers and in early adulthood. Explain which of the two models fit is more appropriate for addressing this research question.

<h2>Question 3c</h2>

It is well established that women are generally more willing to seek medical attention for health problems than men, and it is hypothesized that men are less likely than women to report minor injuries caused by road accidents. Write a critical assessment of whether or not the control group is a valid one for assessing whether women are on average better at road safety than man.

<h2>Some code</h2>

download data

pedestrainFile = Pmisc::<strong>downloadIfOld</strong>(

‘http://pbrown.ca/teaching/303/data/pedestrians.rds’) pedestrians = <strong>readRDS</strong>(pedestrainFile)

pedestrians = pedestrians[!<strong>is.na</strong>(pedestrians$time), ] pedestrians$y = pedestrians$Casualty_Severity == ‘Fatal’ Code for fig. 2 newData = <strong>expand.grid</strong>( age = <strong>levels</strong>(pedestrians$age), sex = <strong>c</strong>(‘Male’, ‘Female’),

Light_Conditions = <strong>levels</strong>(pedestrians$Light_Conditions)[1],

Weather_Conditions = <strong>levels</strong>(pedestrians$Weather_Conditions)[1])

thePred = <strong>as.matrix</strong>(<strong>as.data.frame</strong>( <strong>predict</strong>(theGlmInt, newData, se.fit=TRUE)[1:2])) %*% Pmisc::<strong>ciMat</strong>(0.99)

thePred = <strong>as.data.frame</strong>(thePred) thePred$sex =newData$sex

thePred$age = <strong>as.numeric</strong>(<strong>gsub</strong>(“[[:punct:]].*|[[:alpha:]]”, “”, newData$age))

toPlot2 = reshape2::<strong>melt</strong>(thePred, id.vars = <strong>c</strong>(‘age’,’sex’)) toPlot3 = reshape2::<strong>dcast</strong>(toPlot2, age ~ sex + variable) <strong>matplot</strong>(toPlot3$age, <strong>exp</strong>(toPlot3[,-1]), type=’l’, log=’y’, col=<strong>rep</strong>(<strong>c</strong>(‘black’,’red’), each=3), lty=<strong>rep</strong>(<strong>c</strong>(1,2,2),2), ylim = <strong>c</strong>(0.007, 0.11), xaxs=’i’, xlab= ‘age’, ylab=’prob’) <strong>legend</strong>(‘topleft’, lty=1, col=<strong>c</strong>(‘black’,’red’), legend = <strong>c</strong>(‘male’,’female’), bty=’n’)