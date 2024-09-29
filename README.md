# Market Basket Optimization

## Table of Contents
1. [Overview](#overview)
2. [Data](#data)
3. [Analysis Steps](#analysis-steps)
    - [Data Preprocessing](#data-preprocessing)
    - [Apriori Algorithm](#apriori-algorithm)
    - [Eclat Algorithm](#eclat-algorithm)
4. [Results and Discussion](#results-and-discussion)
5. [Conclusion](#conclusion)
6. [References](#references)

## Overview

This project aims to identify ideal association rules between products to design a marketing campaign where purchasing one item offers a discount on another item. Both Apriori and Eclat algorithms are utilized to compare results and derive actionable insights.

## Data

The `Market_Basket_Optimisation.csv` dataset contains transactions collected over one week, comprising 7,501 different transactions. Each row represents the items purchased in a single transaction.

## Analysis Steps

### Data Preprocessing

- **Transaction Formatting**: Converted the dataset into a list of transactions, where each transaction is a list of items purchased together.

### Apriori Algorithm

- **Minimum Support**: Set to approximately 0.003, calculated based on a minimum of 3 purchases per day over one week:

   $\text{Minimum Support} = \frac{3 \times 7}{7501} \approx 0.003$

- **Minimum Confidence**: Set to 0.1 to ensure that in at least 10% of relevant transactions, the association rule holds.
- **Minimum Lift**: Set to 1 to focus on rules that occur more frequently than by random chance.
- **Minimum and Maximum Length**: Both set to 2 to identify pairs of items for the marketing campaign.

### Eclat Algorithm

The ECLAT algorithm was also applied to identify frequent itemsets of length 2, focusing on items commonly bought together without considering the direction of association.

## Results and Discussion

### Apriori Algorithm Results

The **Apriori algorithm** identifies directional association rules, providing insights into which products are likely to be purchased together. Below are some key rules:

| Left Hand Side        | Right Hand Side | Support  | Confidence | Lift     |
|-----------------------|-----------------|----------|------------|----------|
| fromage blanc         | honey           | 0.003333 | 0.245098   | 5.164271 |
| honey                 | fromage blanc   | 0.003333 | 0.116883   | 5.164271 |
| light cream           | chicken         | 0.004533 | 0.290598   | 4.843951 |
| pasta                 | escalope        | 0.005866 | 0.372881   | 4.700812 |
| pasta                 | shrimp          | 0.005066 | 0.322034   | 4.506672 |

**Fromage Blanc and Honey**: The strong association `fromage blanc -> honey` indicates that customers who buy fromage blanc are over five times more likely to also purchase honey than by random chance. However, the reverse rule (`honey -> fromage blanc`) has a much lower confidence, reflecting that honey is a frequent purchase, but it does not strongly predict the purchase of fromage blanc.

This highlights a key insight about **directionality** in the Apriori algorithm. While the association from `fromage blanc` to `honey` is strong and relevant for cross-promotions, the reverse relationship is too weak to act upon. This may be because **honey** is commonly bought with many other products, diluting its connection to fromage blanc.

### ECLAT Algorithm Results

In contrast, the **ECLAT algorithm** focuses purely on frequent itemsets without considering the direction of association. The top 10 frequent itemsets identified by ECLAT are:

| Itemset                    | Support  |
|----------------------------|----------|
| spaghetti & mineral water   | 0.059725 |
| chocolate & mineral water   | 0.052660 |
| eggs & mineral water        | 0.050927 |
| mineral water & milk        | 0.047994 |
| ground beef & mineral water | 0.040928 |

ECLAT results show which products are frequently bought together, but they do not provide information about whether one product drives the purchase of the other. For example, `spaghetti & mineral water` frequently co-occur, but we do not know if buying spaghetti leads to the purchase of mineral water or vice versa.

This reflects a fundamental difference between Apriori and ECLAT: while Apriori reveals directional rules for targeted cross-selling, ECLAT simply shows which products co-occur, making it useful for identifying general bundling opportunities.

## Conclusion

The **Apriori algorithm** provides directional insights, revealing product relationships that can inform targeted marketing strategies. For example, customers buying `fromage blanc` are significantly more likely to also purchase `honey`, which could inform cross-promotions.

The **ECLAT algorithm**, on the other hand, focuses purely on frequent itemsets, making it ideal for identifying frequently bought product pairs without directionality. Both algorithms provide valuable insights, but they serve different purposes in market basket optimization.

## References

Machine Learning A-Z: AI, Python & R [2024]  
Created by Hadelin de Ponteves, Kirill Eremenko, SuperDataScience Team, and the Ligency Team  
[https://www.udemy.com/course/machinelearning/](https://www.udemy.com/course/machinelearning/)
