# NHL-Playoffs

## Intro
This project was inspired by an interest in NHL hockey: Kristina played competitive ice hockey growing up in Boston; and Mark's kids started playing ice hockey several years ago.  Given our knowledge and understanding of the game, we thought it would be interesting to investigate the NHL's rich array of published statistics in order to see if we could predict what factors made a team successful during the regular season.

## Tech Stack
- Python
- Requests
- Pandas
- Matplotlib
- Seaborn
- Scikit-learn
- StatsModels

## Setting Up
We posed the question:  Which factors contribute to an NHL team’s success in the regular season?

Our expectation was that many aspects of the game would need to be included in our final model  given the structure and dynamics of the game.

More specifically, we wanted to investigate the relative importance of offense and defense in a season's games, as a measure of team performance.

## Process
We availed ourselves of the NHL's rich API for sourcing statistics.  Additionally, we used some webscraping techniques to source additional data contained on the NHL's site in JSON form.

After using the NHL's APIs to source data, we manipulated the data into the structures we chose to use for our analysis, namely, team-based statistics collected for a given team for a given season.

After cleaning and organizing the data we used Matplotlib and Seaborn Python libraries to develop an understanding of the relative distributions of our data and begin to determine important variables for our linear regression model.

### Data
Most of our data was quite clean and complete, for example there were no null values.  However,  there were cases in which we needed to remove outliers, for example, there is no data for the 2004-2005 season, due to a lockout; and we needed to remove the 2012-2013 season in its entirety, given that only half the games were played during that season, due to a partial lockout.

The images below show the distribution of our data for a particular variable (face-offs won) both before and after removing outliers.  Looking at these distributions helped us determine that we had outliers in the data.  

![](/plots/FaceOff_dist.png)

![](/plots/FaceOff_dist_no_outliers.png)

We made sure to check that each of our rows had a full set of data and therefore that we had no null values.

![](/plots/Null_values.png)

We added a new column for "win percentage" (total wins / total games played), which we selected as our dependent variable.  We also created three additional variables:  one was categorial, entitled the "Original 6", to reflect the original six NHL teams (Boston Bruins, Chicago Blackhawks, Toronto Maple Leafs, Montreal Canadiens, New York Rangers, and Detroit Red Wings).  This variable was created to investigate whether the history of those franchises had any impact on performance over the last twenty seasons.

We also created two interaction terms:
- "puck possession" (a combination of the columns "shots for", "missed shots", and "blocked shots")
- "defensive strength" (a combination of the columns "hits", "takeaways", "penalty kill percentage", and "shots allowed")

In total we had 516 individual observations, each reflecting an individual team in a given season.

Below are four scatter plots which show correlations between our target variable and four of our independent variables.  By running these scatter plots we were able to determine variables that would be important to our model, given clear linear relationships with our target variable.  For example, we believed that the number of hits a team made in a given season would be important to our model, given the physicality of the game; but as confirmed by our scatter plot below, there is no clear linear relationship between win percentage and total hits.  We confirmed this for all features by including them in earlier iterations of our model and noting they were not statistically significant (based on p-values over .05).

![](/plots/Corr1.png)

![](/plots/Corr2.png)

![](/plots/Corr3.png)

![](/plots/Corr4.png)


## Evaluating the Model
The first model shown below can explain forty percent of the variance in our target variable.  We recognize that by adding a given team’s goal counts (either for, or against) that our R-squared increases to 87% and the reason for that is that knowing on average how much a team scores can very closely predict win percentage.  However, our goal was to create a predictive model that didn’t account for goal metrics, given their obvious linear relationship with success.   One thing we can confidently say based on these two models is that our assumption that defensive team strength would contribute significantly to a team’s success did not hold.  

![](/plots/model_1.png)

![](/plots/model_2.png)

As a final step we confirmed that our residuals are generally normally distributed, and that they are relatively homoscedastic.


![](/plots/residuals.png)


Given the chance to improve this model with additional data, our process would be to revisit the NHL API and gather additional offensive metrics, such as shot type, as well as individual player statistics.  In this way, we might obviate the need to use goal data to predict a team’s success.


