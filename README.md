# NBA_team_score
This Repository is for the Data Incubator Semifinalist Challenge. For this challenge I need to propose a Capstone Project that I intend to finish during the Data Incubator.

I am proposing to design a NBA Trade and Draft Recommender System, in the hope that the following two questions can be answered:

1. Given a current team combination, which player in the league best fit the team in a certain salary range?
2. Whether a draft pick will improve my team or not? 

I believe that these two questions are concerned by NBA managers, as well as basketball fans and game developers. The data analysis in the basketball world has just started to show their power and I, being a basketball fan for 15 years, would love to give my thoughts and endeavor to this area.

Definition of the Elo score:
For these questions, it is essential to define a team score for a specific team in a specific season. For this we will need to first define a initial score (We will use the TeamPER score defined in the Python Notebook, and below), then update them using the Elo ranking algorithm to obtain a relative team score (We will call it the Elo score).  During the play-offs, we will adjust the weights to give the series-winning team more advantage in their Elo score.

For the next season, if a team does not change the roster too much (need to be defined specifically), the Elo score carries over. For those team who changed their rosters dramatically, we update their score using the initial TeamPER  score. Then we start the process again.

Definition of the TeamPER score:
The TeamPER score uses the very commonly used individual PER score in the NBA. PER stands for Player Efficiency Rating, which is defined by ESPN.com columnist John Hollinger. The score reflect how much contribution each player do to the team every minute on court. Our TeamPER score is defined as follows:
1. Pick top 12 players in each team that played the most minutes (MP).
2. We compute the product of individual PER score and the Minuted Played for each player.
3. We sum the value above among the top 12 players. Normalize the value to a reasonable range.
The reason for using the product of individual PER score and Minutes Played is due to PER score is computed per minute. The product reflect the total contribution a player does to the team. Also we only record the top 12 players that play the most minutes, because otherwise the player may only play in the trash time, which should be neglected.
We will see below that this TeamPER score behave relatively well. But during the capstone project, I will use a linear regression to find out the best coefficients for a polynomial in the definition of TeamPER.

Two approaches for question 1:
1. We will obtain an Elo score for each team at the end of each season, we can then use machine learning to study the relations between the composition of the team (meaning current roster & stats of each players) and the Elo score. We can thus fit in the potential new player (substitute with some player in the team, will discuss this later) and update the Elo score. We can then tell whether this will be a good fit or not by the increase/decrease of the Elo score.
2. Instead of using the machine learning, we can try to simulate a new season using the updated roster (with current composition of every other team in the league) and see if the will be an improvement in the result.

For question 2: 
We can basically do the same as for question 1, but we then need to use the stats of the player before the draft (for most players, their college basketball stats). We will need to figure out a weight to put on their college stats when we use them to compute the Elo score. This weight will also need to be find out using previous data on new drafts.

Data for 1: Player stats for each player until 2017. Also the game results in the same period.
Data for 2: Data for every college player in the year before nba(not done) + Data for every professional player (done)

For the two plots:
I have uploaded a Python Notebook that contains these two plots as well as my codes. 
In the notebook we define the TeamPER score, and to plot the correlations of the TeamPER score and the Winning Percentage. The other graph is an analysis on the rookie performances in the past 20 years. 

All basketball stats available for download
https://www.basketball-reference.com/

Link for Seasons_stats.csv
https://www.kaggle.com/drgilermo/nba-players-stats


Blog post: It appears that someone has studied the Elo rating for NBA!!
https://fivethirtyeight.com/features/how-we-calculate-nba-elo-ratings/

Blog post: For rookies-year performance compared to before-draft performance:
https://towardsdatascience.com/dissecting-the-nba-draft-ee175d7aec31


