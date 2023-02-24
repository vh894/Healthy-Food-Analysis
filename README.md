# Healthy Food Analysis 

## Introduction and Question Identification

There have been multiple studies that show an increased amount of awareness and concern for healthier diets in the range of years that this dataset contains (2008 to present).[^1] However, even with the growing interest in improving personal diets, the production of quick, processed foods has also boomed due to its convenience. Since healthy recipes are essential for our welbeing, it’s important to know what the general public thinks about them. Based on the ratings of healthy recipes, we can find ways to improve these recipes to encourage more nutritional eating habits. These concerns led us to focus on the question: “Are healthy recipes rated higher than unhealthy recipes?”.  

In order to answer this question, we utilized data from food.com, an online community where individuals can upload their own recipes. The data from this website contains the ratings, reviews, and nutritional values of various dishes, and we will be using a dataset of 234,429 reviews of various recipes from the website for our project.

Although the dataset contains a total of 15 columns, we will be mainly focusing on these columns:
- “user_id” 
  - The id of the user who left a rating
  - Type: integer
- “recipe_id“ 
  - The recipe identification number
  - Type: integer
- “name” 
  - The recipe name
  - Type: object
- “nutrition” 
  - Nutritional information of the recipe
  - Type: object
  - In the form [calories (#), total fat (PDV), sugar (PDV), sodium (PDV), protein (PDV), saturated fat (PDV), carbohydrates (PDV)] 
  - PDV: percentage of daily value
- “rating” 
  - The rating given by the user out of five stars
  - Type: float
- “description” 
  - The description of a recipe, written by the recipe developer
  - Type: object
- “review” 
  - The text within a review of the recipe
  - Type: object

[^1]:<a href="https://www.usda.gov/media/press-releases/2014/01/16/american-adults-are-choosing-healthier-foods-consuming-healthier">American Adults are Choosing Healthier Foods, Consuming Healthier Diets</a>, <a href="url">Consumer trends shifting toward health and wellness, ADM finds</a>, <a href="https://www.upfluence.com/influencer-marketing/influencer-marketing-healthy-food-industry#:~:text=The%20healthy%20food%20movement%20has,reformulating%20or%20remarketing%20their%20goods.">Influencer marketing and the rise of healthy eating habits</a>

## Cleaning and EDA
The first step that we took to analyze the dataset was that we split the “nutrition” column into 7 individual columns. The values in the “nutrition” column are lists with 7 elements, with each element being the amount of calories, total fat, sugar, sodium, protein, saturated fat, and carbohydrates, respectively. We accomplished this step by using the tolist numpy method. We then used the individual values from these 7 nutrition categories to analyze which was considered to be a healthy recipe. The nutrition values are in terms of the percent daily value with the exception of the calories column, which is in terms of the actual value itself. According to the FDA in their <a href="https://www.fda.gov/food/new-nutrition-facts-label/daily-value-new-nutrition-and-supplement-facts-labels">Daily Value on the New Nutrition and Supplement Facts Labels</a>, they suggest choosing foods that are “lower in saturated fat, sodium, and added sugars.” Furthermore, the FDA also mentioned in “The Lows and Highs of Percent Daily Value on the New Nutrition Facts Label” foods with a 20% PDV or higher are considered high. Therefore, we established a recipe as being healthy if it has less than 20% PDV of sugar, sodium, and saturated fat. Since the other categories are generally considered to be healthy, we decided to not apply a filter for the data in these columns. 

While we were looking through the dataset, we noticed that there were some ratings that had 0 stars. However, this rating is an inaccurate representation of the recipe because ratings typically start at 0 stars if they haven’t been rated yet. Therefore, the recipes only have 0 stars because it’s an unrated review on a recipe, not because a user gave the recipe 0 stars. To fix this issue, we decided to replace all of the recipes that had a rating of 0 to have a rating of np.NaN to represent the reviews on the recipes that have yet to be rated.

Another problem that we found with the data was that there were a few recipes that were inedible. For example, there are recipes for dishwasher detergent and neti pot saline solution. Although they are still recipes, our hypothesis question focuses only on recipes that are healthy or not, which means that all the recipes in our dataset need to be edible. In order to filter out the recipes for inedible creations, we determined that these inedible recipes shouldn’t have any calories. We queried the dataset to show all the recipes that have 0 calories, and analyzed the recipes within this queried dataset to get the inedible recipes. We used this list of inedible recipes to filter out the unnecessary data.

For one of the graphs in our report, we plan on comparing the distribution of healthy and unhealthy recipes for each rating. However, the ratings contain decimals, which would make the visualization harder to comprehend if we were to calculate the proportion of healthy recipes for each unique rating. In order to create a plot that would better display the relationship between the two variables, we created a new column in the dataframe that consists of the average rating of each recipe, rounded to the nearest integer. We used this new column as the bins for the histogram of the ‘Distribution of Healthy vs. Unhealthy Recipes per Star Rating” plot.

To measure the popularity of the different recipes, we decided to look at the distribution of the average ratings per recipe. By looking at this plot, which we separated into bins of the nearest whole star, we can see that the distribution of the ratings is left skewed, which means that the majority of the recipes are rated highly.

<iframe src="assets/file-avg_rating.html" width=800 height=600 frameBorder=0></iframe>

While we were analyzing our dataset, we noticed that there were some recipes with an abnormally high amount of calories, with one recipe having over 40000 calories. We plotted the distribution of calories to determine if there are more recipes we should look into before performing our testing, and we can see that the plot is extremely skewed to the right, with a majority of the recipes having at most 2500 calories.

<iframe src="assets/file-calories.html" width=800 height=600 frameBorder=0></iframe>

To see the distribution of “healthy” recipes with the ratings visually, we used a stacked histogram. The proportion of “healthy” per bins increases as the bin range increases.

<iframe src="assets/file-healthy_and_rating.html" width=800 height=600 frameBorder=0></iframe>

We wanted to see the relationship between the amount of calories a recipe had and the proportion of healthy recipes within a specified bin range. The stacked histogram shows that as the amount of calories increases, the proportion of healthy recipes within that bin decreases.

<iframe src="assets/file-calories_and_rating.html" width=800 height=600 frameBorder=0></iframe>

This grouped table displays data for each group of integer value ratings


|   calories (#) |   total fat (PDV) |   sugar (PDV) |   sodium (PDV) |   protein (PDV) |   saturated fat (PDV) |   carbohydrates (PDV) |   healthy |
|---------------:|------------------:|--------------:|---------------:|----------------:|----------------------:|----------------------:|----------:|
|        463.345 |           37.1243 |       76.4471 |        45.19   |         29.85   |               45.88   |               15.1329 |  0.187143 |
|        432.541 |           33.7407 |       70.995  |        35.9892 |         29.7432 |               45.2022 |               14.2486 |  0.18227  |
|        459.962 |           33.2098 |       94.367  |        39.5927 |         32.5997 |               41.5364 |               16.274  |  0.166993 |
|        428.62  |           31.8566 |       63.578  |        28.2143 |         35.1706 |               39.4801 |               13.7132 |  0.172237 |
|        413.743 |           31.7462 |       62.5115 |        29.1608 |         32.5769 |               39.22   |               12.9443 |  0.17514  |


## Assessment of Missingness

One column in the data frame that we determined to be NMAR is the description column. Since the description is written by the recipe developer, the description might be missing if the author chose not to write one.

The rating column is also NMAR because people will most likely only rate a recipe if they feel strongly about it. As a result, most of the ratings that exist in the dataset are extremely high. Since the probability of a rating being missing depends on the value of the rating itself, it’s NMAR.

The third column that had missing data was the review column, which we determined to be MAR. The probability of a review being missing could depend on a variety of factors, but we concluded that it was most likely to rely on the rating or the number of steps of a recipe. We conducted permutation tests for each of these two variables with the review variable. The p-value of the permutation test for review and rating was 0.682. Since this value is greater than 0.05, we failed to reject our null hypothesis that the missingness of reviews depends on the review’s rating. The p-value for review with the number of steps was 0, which means that the result for this test is statistically significant. Therefore, we reject the null hypothesis and can conclude that the missingness of reviews is dependent on the number of steps for a recipe. This may be explained by the fact that people are less likely to write a review if there are too many steps for that recipe.

<iframe src="assets/file-reviews_missingness_1.html" width=800 height=600 frameBorder=0></iframe>


<iframe src="assets/file-reviews_missingness_2.html" width=800 height=600 frameBorder=0></iframe>


## Hypothesis Testing

The goal of our testing is to answer the question: Are healthier recipes significantly higher rated than the general pool of recipes? Because this question is utilizes a sample of all the recipe reviews on food.com, we ran a hypothesis test with the following hypotheses: 
- Null hypothesis: The proportion of higher rated recipes among healthy recipes is equal to the proportion of higher rated recipes in the overall population.
- Alternative hypothesis: The proportion of higher rated recipes among healthy recipes is greater than the proportion of higher rated recipes in the overall population.

Because this was comparing proportions, we decided on the test statistic as the proportion of highly rated recipes. We set the significance level as 0.05. 

<iframe src="assets/file-hypothesis_testing.html" width=800 height=600 frameBorder=0></iframe>

As shown in the graph above, we got a p-value of 0.0. We reject the null hypothesis and conclude that the proportion of higher rated recipes among healthy recipes is greater than the proportion of higher rated recipes in the overall population.
