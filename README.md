# Top-5-Football-Leagues-Clustering-Analysis

## Project formulation
For this project my goal was to cluster teams in the top 5 leagues by their passing statistics and pass types to determine teams that are similar in playing style. These statistics are scraped from FB Reference and they are all from the 2022-23 season. I wanted to capture overall play styles: this includes type of ball progression from defense to attack, amount of crosses, through balls, and short vs. long passes. I used K-means clustering in python to do this. Often in the soccer world we classify teams on a scale somewhere between controlling possession and direct counter attack. I think this project is useful because it can show how these play styles can be quantified and how distinct the groups of tactical approaches are. If there are more distinct clusters, then it is evident that certain general patterns of play are effective across all of Europe’s best leagues. If there is more of a sliding scale of play styles, then we will have insight into how important individual managers’ philosophies are. Looking at contemporary literature, “K-means cluster analysis was also used by Gollan, Ferrar, and Norton [36] to recognize playing styles. Three game style clusters were identified: (1) moderately favoring established defense, (2) dominant in transition offense and transition defense, and (3) strong in established offense and set pieces. The disadvantage of this method is that it does neither recognize playing styles, nor is it capable of quantifying them; instead, it categorizes the teams based on the phases in which they excel” (Plakias S et al., Identifying Soccer Teams’ Styles of Play: A Scoping and Critical Review.) After Completing the project I definitely ran into similar issues with one cluster containing the worse teams and one containing mostly the best teams, however I will save that discussion for the end.

## Box Plots- Comparisons within each league
For this initial data exploration, I want to get a sense of the types of passing that are popular within each league. To do this, I will create box plots looking at each passing type (short, medium, long, through balls, crosses into the penalty area) as well as percent of passes completed. I will look at the median amount of each within each league, which will represent the 50th percentile team. I'm choosing this instead of the mean because it is a relatively small sample size and due to the presence of outliers in the form of the very best teams.

![short passes![medium passes](https://github.com/Owenp25/Top-5-Football-Leagues-Clustering-Analysis/assets/77632947/0bb12fdc-bcba-46b2-aa84-dba21a3e7c76)
](https://github.com/Owenp25/Top-5-Football-Leagues-Clustering-Analysis/assets/77632947/ab6f2c93-53fa-4b8e-bd66-ee410586d863)
![long passes](https://github.com/Owenp25/Top-5-Football-Leagues-Clustering-Analysis/assets/77632947/b606e69e-33bd-4bbc-ada5-4d8f4b5da59d)

Short passes: fewest in bundesliga, most in la liga and premier league
Medium passes: fewest in la liga, most in ligue 1 and bundesliga
long passes: By far the least in premier league and most in serie A and ligue 1
In terms of pass completions the prem is much more focused on short passing while it appears that ligue 1 is the most direct followed by the serie A.

## Scatter Plots Based on Assists

Now I want to look at what kind of passing style might be the most effective. I will create 4 scatter plots plotting short passing, crosses, through balls, and then long passes against assists to see if there is a strong positive linear relationship between any of these pairs. I want to see if any of these passing styles is connected to a higher output of assists.

![Assists by long](https://github.com/Owenp25/Top-5-Football-Leagues-Clustering-Analysis/assets/77632947/6fc54a82-e9f8-43e0-bc19-8296145dde41)
![Assists by crosses](https://github.com/Owenp25/Top-5-Football-Leagues-Clustering-Analysis/assets/77632947/68bdb4d7-25e9-40eb-89f1-50e69b615721)
![Assists by tbs](https://github.com/Owenp25/Top-5-Football-Leagues-Clustering-Analysis/assets/77632947/02532bcd-b7a6-43c0-a811-e13398db3a8d)
![assists by short ](https://github.com/Owenp25/Top-5-Football-Leagues-Clustering-Analysis/assets/77632947/dcb8c5cd-6493-4169-8f98-4c19662c40bc)

In these scatterplots each point represents an individual team. Looking at the plot and the correlation coefficients, it is clear that a higher amount of completed short passes is most closely associated with a higher amount of assists. The correlation is fairly high at 0.706. It is interesting that a high number of assists is not very closely associated with a high amount of crosses as many teams rely on crosses as the main way of providing service to their strikers. This does not mean that increasing short passing equals more assists and increasing crossing is problematic, it merely backs up the fact that quality teams are able to complete more short passes and that crossing is a more unpredictable way of trying to fashion scoring chances.

![scatter grid](https://github.com/Owenp25/Top-5-Football-Leagues-Clustering-Analysis/assets/77632947/f2a0e20d-de4c-40ca-8362-809dd2f0ba45)

Looking at 5 of the passing variables, there appears to be a fairly strong positive correlation between most pairs of these. When looking at their distributions, their appears to be some skew present so I will definitely have to standardize the data before conducting PCA.

## PCA and K Means Clustering

Doing K Means clustering will split the data into groups centering around centroids specified by the algorithm. Due to the sheer number of features in the data, I will have to use PCA (Principal Component Analysis) to reduce the dimensions into fewer dimensions. This will take all of my numeric, correlated variables and reduce them into uncorrelated variables that contain as much of the information in the original data set as possible. I'm hoping to reduce the feature space down into 2 dimensions for visualization sake. Total distance and progressive distance have large variances compared to the other variables, this will be an issue with PCA because their large variances will dominate the principal components meaning that other variables' information will be lost out on. Because of this I will standardize the data. Also, I will drop all other columns that aren't necessary for analysi

![Final scree](https://github.com/Owenp25/Top-5-Football-Leagues-Clustering-Analysis/assets/77632947/e672d8bf-841f-4973-8aa8-aa14b6dbeb81)

This confirms the need to use 3 PCs for my analysis.

![Biplot 1](https://github.com/Owenp25/Top-5-Football-Leagues-Clustering-Analysis/assets/77632947/b2b1e3a5-d175-4856-9058-bcb3876e1915)

![Biplot 2](https://github.com/Owenp25/Top-5-Football-Leagues-Clustering-Analysis/assets/77632947/3ccd15d3-7a48-4af7-b451-5b065655d37f)

With this final pruned data set about 86.9% of the variability in the data is captured in the first 3 principal components which is satisfactory for me. The bi plots of the combinations of PCs show that there are now no variables extremely correlated with each other in this plane and that there are distinct differences between PC3/PC2 and PC1. Long passes, crosses, and switches of play are important for PC 3 and PC 2 while through balls, short passes, and progressive passes are important for PC 1. I will now use these PCs to create a 3D scatterplot in order to try and visualize the clusters of teams.

## Final 3D Cluster Plot

![zoomed in](https://github.com/Owenp25/Top-5-Football-Leagues-Clustering-Analysis/assets/77632947/8c6385a5-484b-40c1-8165-a1a8795a0024)

Zoomed-in Version

![Full](https://github.com/Owenp25/Top-5-Football-Leagues-Clustering-Analysis/assets/77632947/528c0e62-b553-4dac-bd5e-fbecd80d3d37)

Full Version

Principal component 1 measures a team’s tendency to play shorter passes, progressive passes and through balls while principal component 2 measures a team’s tendency to play long passes, switches of play, and crosses. Principal component 3 measures a team’s tendency to switch the play and play crosses. This is useful because it does divide teams into styles of play. Those that are near each other in the PC1 direction do shorter build up play and work the ball into the box. Those that are close to each other in the PC2 and PC3 direction rely more on long balls and crosses, i.e. direct play. The location of each point represents its score on each principal component, So for example Fiorentina, Osasuna, and Vallecano are similar in play style. In another location, Lazio, Leipzig, and Manchester City are similar in play style. It is cool to see that teams from different leagues are clustered in this way. While there are not 3 distinct groups (there is overlap between the blue and green cluster) like I hypothesized, I think this is still a good graph to get a general sense of teams with similar passing styles.

## Continued Analysis

Now I will pull another set of data from FB ref. I'm taking the overall statistics and will merge the two data frames in order to have some more statistics such as league rank, wins, points per match, goals scored, and goals conceded. This way I can see which cluster has the highest average league rank, best goal scoring average, etc.

Average League Rank of Each Cluster (Rounded to Whole Number)

Cluster 0: 14

Cluster 1: 4

Cluster 2: 11

Cluster 1 clearly contains the best teams while cluster 0 and 2 contain similarly ranked teams, with cluster 0 containing slightly worse clubs on average.

## Analysis of Cluster Style

I will use some histograms to see which statistics stand out in each cluster, comparing these to the important variables for each principal component.

![end long](https://github.com/Owenp25/Top-5-Football-Leagues-Clustering-Analysis/assets/77632947/dfc3d977-d71b-4a3c-a262-a1cc86309ab0)
![end cross](https://github.com/Owenp25/Top-5-Football-Leagues-Clustering-Analysis/assets/77632947/ba3b7616-eee6-4fa5-b731-b2d3cd08b60e)
![end through ball](https://github.com/Owenp25/Top-5-Football-Leagues-Clustering-Analysis/assets/77632947/181e0b0c-8069-40f0-9c37-a08b7fb9bc70)
![end switches](https://github.com/Owenp25/Top-5-Football-Leagues-Clustering-Analysis/assets/77632947/558d0013-7637-43ba-b1eb-b553b7243df4)
![end short](https://github.com/Owenp25/Top-5-Football-Leagues-Clustering-Analysis/assets/77632947/4c84c4cc-a93e-4b1b-9e7e-08912901531f)
![end prog](https://github.com/Owenp25/Top-5-Football-Leagues-Clustering-Analysis/assets/77632947/65878f4a-e633-4aac-8b10-4462eb8be04f)
![end points](https://github.com/Owenp25/Top-5-Football-Leagues-Clustering-Analysis/assets/77632947/db9e3074-0f99-4f28-9147-4a47d8917131)

These histograms line up with the variable importance in each cluster/principal component. Cluster 1 has the best performing teams and they tend to attempt lots of short passes, medium passes, through balls, and progressive passes. The only stylistic information we can get about cluster 2 is that these teams tend to play more long balls and crosses than teams in the other clusters. Cluster 0 appears to be the weakest teams in terms of league rank and the amount of passes they attempt in all categories.

## Conclusions, Limitations & Takeaways: 
While I was successfully able to cluster teams based on a few features, the use of principal components combined with clustering does not lend itself well to interpretability. I know that teams within each cluster that are close to each other have similar scores based on the principal components, and I know the most important variables for those principal components, but nailing down the exact way of playing that each cluster represents is not entirely possible with my analysis. However, what I have done is useful for seeing which teams are at their very core similar in terms of how they pass. This has applications in scouting and opponent analysis. When searching for new signings that may fit a team's play style, one could look at this 3D scatter plot or search in the data frame for teams within the cluster that their team belongs to. Say West Ham were looking to further bolster their midfield after losing Declan Rice. They could look at this graph and identify Hoffenheim or Athletic Club as teams with potentially suitable midfielders based on passing style. Of course this would only be a very small part of the scouting process but it would allow the scouting staff to gain insight into play style compatability. There is so much that goes into a transfer being successful so any unique information such as this could be a very important piece in the puzzle. Additionally, this could be used to look at opponents, especially those in European competitions such as the Europa League or Champions League. If hypothetically Rennes had to play Roma in the Europa League, they could look at this plot and notice that Roma is very similar to Toulouse in terms of passing style, who they play domestically and far more frequently.
