# Stochastic-Frontier-Analysis-Poster-PMRC-#

**Tutorial Videos**

 Panel Example by Brian Mazorodze https://youtu.be/12ipB--Z4C0 
 
 Cross Sectional Example by Brian Mazorodze https://www.youtube.com/watch?v=EXIhQB44GdI 

/*STATA CODE TEMPLATE*/

/*Use Panel Data 1*/

/*install sfpanel command*/

ssc install sfpanel 

/*install sfcross command*/

ssc install sfcross

/*tells STATA that this data set is panel data use ID variable and year variable*/

xtset code yr

/*Make sure variables are logged*/

gen lnDV = log(DV)
gen lnIV1 = log(IV1)
gen lnIV2 = log(IV1)

/*sfpanel command DV, IVs, Model type (True fixed effects, distribution type (truncated normal, exponential, gamma, half normal)*/

sfpanel lnDV lnIV1 lnIV2 yr, model(tfe) dist(exp)

/*True fixed effects Greene 2005 separates time invariant data  across industries with time varying technical efficiency. When you observe output overtime across several industries you may deviate from the frontier because of two things unobserved time invariant factors and time varying technical efficiency */

/*Diagnostic test*/
/* sigma_u^2 + sigma_v^2  = sigma^2. Sigma_u^2 / sigma^2 --- Between 0-1 closer to 1 means that inefficiency acccounts for a greater percent of the variation*/

/*Predict levels of technical efficiency*/

sfpanel lnDV lnIV1 lnIV2 yr, model(tfe) dist(exp)

predict te, jlms

sum te

sfpanel lnDV lnIV1 lnIV2 yr, model(tfe) dist(exp)

predict exp, jlms

/*How to graph*/

histogram te
