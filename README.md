
## Introduction
In this project we are going to examine different factors in the Northwind database and their influence on sales. We will be exploring the effects of discounts, order frequency and individual employees on the quantities of items sold and the average prices of orders. The Northwind Database contains sample sales records for a company named "Northwind Traders." Below is a schema for the shape of the database.

![Northwind_ERD_updated.png](attachment:Northwind_ERD_updated.png)

The project will be broken down into individual questions and each question will follow a similar pattern. We will present the null and alternate hypothesis, collect our sample, examine and clean our data, then test the data to determine an effect. We will use a variety of tests to examine the data.

## Question 1: Does discount amount have a statistically significant effect on the quantity of a product in an order? If so, at what level(s) of discount?
We will begin by looking at the effect of discount on the quantity of items that are ordered. This question will be broken down into two hypothesis. The first will test for the effect of any discount on quantity. If that test demonstrates a significant effect, then we will test different discount levels to determine at what levels the effect is noticeable.

### First Hypothesis
𝐻𝑂 : Discounted orders will have the same quantity of items as non-discounted orders.

𝐻𝐴 : Discounted orders will contain more items than non-discounted orders.

For this test we will run a one-tailed (only looking for a larger effect) t-test with an alpha level of 0.05.

### Exploratory Analysis
Before we run our t-test, we will look a graphical representations of our data. First, we will look at the average quantity ordered with a discount and without a discount; then, we will break down this information by product ID to make sure that overall trends are present across multiple products.

![items_ordered_by_discount.png](attachment:mod3_project_charts.items_ordered_by_discount.png)

![items_ordered_by_product_id.png](attachment:mod3_project_charts.items_ordered_by_product_id.png)

The graphs indicate that discounted orders generally contain a larger quantity of items, but let's determine if this is a significant difference.

### Welch's t-test
We will run Welch's t-test to determine a p-value that we can check against our alpha level. If this produces a significant effect, we will also determine an effect size (Cohen's d) to judge the magnitude of difference.

We will reject the null hypothesis because our p-value(5.66e-10) is much lower than our alpha level of 0.05. It appears that discounted orders do have a larger quantity of items ordered. Our effect size is .286, so we have a small, though not inconsequential effect. Let's see if we can determine what discount levels have a significant effect.

### Second Hypothesis
𝐻𝑂 : The quantity of items ordered will be the same between all discount levels.

𝐻𝐴 : The quantity of items ordered will not be the same between all discount levels.

For this test, we will run a one-way anova with an alpha level of 0.05.

### Exploratory Analysis
We will start by looking at the mean quantity for each discount level.

![items_ordered_by_discount_level.png](attachment:mod3_project_charts.items_ordered_by_discount_level.png)

My first impression from the graph is that we will not have a significant difference between discount levels as the means are very close to each other. To test this, we will run a one-way ANOVA.

As expected, our p value of 0.61 is much higher than our critical value of .025. We cannot reject the null hypothesis, and thus we assume all discount levels have a similar effect on quantities ordered.

### Question 1 Wrap Up
Discounted orders do contain higher quantities of items on average. Further, this trend is visible in all levels of discount as there was no significant differences between means of discounted quantities.

## Question 2: Are repeat customers likely to have a higher discount? How does this vary based on the frequency of orders versus the amount the companies spend?
Next we want to see if returning customers are likely to get a discount. We will look at two factors of the companies, the number of orders placed and the amount that the company has spent. We will again test two hypotheses for this question looking at how discount levels are affected by these independent variables.

### Exploratory Analysis
Before we outline our hypotheses, we will look at boxplots of our data to check for outlies. We will look at the number of orders first.
![boxplot_num_orders.png](attachment:mod3_project_charts.boxplot_num_orders.png)

![boxplot_total_spent.png](attachment:mod3_project_charts.boxplot_total_spent.png)

### First Hypothesis
𝐻𝑂 : All companies will have the same disount level

𝐻𝐴 : Companies with more orders will have a higher discount level

We will be conducting a one-tailed linear regression to test this hypothesis. We will again use an alpha level of .05.

With a p-value lower than .001 and a positive coefficient, we are able to reject the null hypothesis. Companies with more orders do have a significantly higher average discount rate. It is interesting to note that our interept is not significant with a p-value of .773; however, since there are no companies with zero orders, this is not a particularly useful metric. Let's chart the regression analysis to get a better idea of our effect.
![discounts_per_num_orders.png](attachment:mod3_project_charts.discounts_per_num_orders.png)

With an  𝑅2  of .235, we can see that the number of orders a company has placed with Northwind Traders has a significant, but not necessarily strong effect on discount. The variance in discount level is not adequately explained by our regression model.
### Second Hypothesis
Ho: All companies will have the same disount level.

Ha: Companies who have spent more will have a higher discount level.

We will also use a one-tailed linear regression analysis for this test.
Again we have a p-value(0) lower than our alpha level. We can reject the null hypothesis. The amount that a company has spent does have a significant effect on discount level. Let's look at a plot of this model.
![discounts_per_total_spent.png](attachment:mod3_project_charts.discounts_per_total_spent.png)

This model doesn't look any better than the first one. Both the  𝑅2  (.216) and the regression coefficient are smaller than those in the model with order frequency. Overall this model also doesn't explain enough variance in discount levels to be satisfactory.

### Question 2 Wrap up
While both higher numbers of orders and higher spending at Northwind Traders had significantly higher discount levels, neither variable was particularly useful in determining discount levels.

## Question 3: Are some employees statistically more likely than others to sell items when discounted? If so, does discount level have an effect?
Next, we want to see how the sales record of discounted items varies between employees. Is our sales team equally good at selling discounted products, or do some employees sell more than others? For this question we will be looking at the quantities of discounted items sold by each employee as well as the discount levels of each order.

### Hypothesis
𝐻𝑂 : The quantities of discounted items sold will be the same between employees.

𝐻𝐴 : Different employees will have different quantities of discounted items sold.

### Exploratory Analysis
First we will look at a bar chart of discounted items versus non discounted items broken down by employee ID numbers. This will give us an idea of how sales change for each employee when items are discounted.

![quantity_sold_by_employee_id.png](attachment:mod3_project_charts.quantity_sold_by_employee_id.png)


It looks like most employees have somewhat improved sales when items are discounted, but some make large jumps. Lets break this chart down further by looking at each discount level by employee ID.

![quantity_sold_by_employee_id_and_discount_level.png](attachment:mod3_project_charts.quantity_sold_by_employee_id_and_discount_level.png)

There are noticeable differences between employees at each discount level. Let's run an ANOVA testing the effect of discount level and employee ID on the quantity of items sold with an alpha level of .05.

There is a significant effect between employee ID (p-value = .01) and the quantity of discounted items sold, but there is not a significant effect for the discount level (p-value = .12).

## Question 4: Are certain types of items more likely to be discounted?
Finally we are going to look at the categories of our products. We are going to see if different categories are more likely to be discounted.

### Hypothesis
𝐻𝑂 : There will be no differences in discount level between product categories.

𝐻𝐴 : There will be significant differences in discount level between product categories.

### Exploratory Analysis
Let's take a look at a barchart of our data. We will look at the average discount level for each category.

![discount_by_category.png](attachment:mod3_project_charts.discount_by_category.png)

With a p-value of .149, we cannot reject the null hypothesis. There is no significant difference in discount levels between types of products.

## Summary
Discount does have a significant effect on the quantity of items ordered, but the level of discount is not significant.
Customers who order more often from Northwind Traders have a significantly higher discount level. Similarly, customers who spend more at Northwind Traders have a signifiantly higher discount level.
Some employees sell significantly more discounted items than other employees, but there is no effect by discount level.
There is no significant difference in discount level between categories of products.