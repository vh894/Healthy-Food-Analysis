# Healthy Food Analysis 

## Introduction and Question Identification

This dataset contains the ratings, reviews, and nutritional values of dishes from the website food.com, an online community where individuals can upload their own recipes. 

In the range of years that this dataset contains (2008 to present), there have been studies that show a increase amount of healthier diets because of growing awareness and social media (American Adults are Choosing Healthier Foods, Consuming Healthier Diets, Consumer trends shifting toward health and wellness, ADM finds, Influencer marketing and the rise of healthy eating habits, etc.). Healthy diets are essential for good health, nutrition, and boosting immunity. 

However, even with the growing popularity of improving diets, the production of quick processed foods has also boomed. These opposing trends led us to focus on the question: “Do healthier recipes tend to be more popular than unhealthy recipes?”. 

In the dataset, there are 234,429 responses to food.com recipes. We will be centered around the columns:
- “user_id” (the user number that left a rating)
- “recipe_id“ (the recipe identification number)
- “name” (the recipe name)

The three columns above will be used for reference purposes.

- “nutrition” (Nutrition information in the form [calories (#), total fat (PDV), sugar (PDV), sodium (PDV), protein (PDV), saturated fat (PDV), carbohydrates (PDV)] where PDV stands for “percentage of daily value”). This column will be used to determine how healthy a recipe is.
- “ratings” (the rating given by the user out of five stars). This column will be analyzed to see how popular healthy recipes are.

## Cleaning and EDA

<iframe src="assets/file-avg_rating.html" width=800 height=600 frameBorder=0></iframe>


<iframe src="assets/file-calories.html" width=800 height=600 frameBorder=0></iframe>


<iframe src="assets/file-healthy_and_rating.html" width=800 height=600 frameBorder=0></iframe>


<iframe src="assets/file-calories_and_rating.html" width=800 height=600 frameBorder=0></iframe>

<iframe src="assets/file_pivot.html" width=800 height=600 frameBorder=0></iframe>


## Assessment of Missingness

<iframe src="assets/file-reviews_missingness_1.html" width=800 height=600 frameBorder=0></iframe>


<iframe src="assets/file-reviews_missingness_2.html" width=800 height=600 frameBorder=0></iframe>


## Hypothesis Testing

<iframe src="assets/file-hypothesis_testing.html" width=800 height=600 frameBorder=0></iframe>
