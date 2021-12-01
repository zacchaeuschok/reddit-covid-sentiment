# Quantitative Analysis of COVID-19 Sentiment on r/Singapore

The COVID-19 pandemic has upended lives and livelihoods in Singapore. In managing the pandemic, the Singapore government has pivoted from an “eradication strategy” to a “living with Covid” approach. These pivots have become a source of tension, division and fear that poses a “communications conundrum” for policymakers. It is thus valuable to understand how Singaporeans’ sentiments on COVID-19 change as key policy decisions are made.

## Data

Since Reddit comments are short and constantly generated, they are a good source of public sentiment towards events throughout the COVID-19 period. Pushshift.io Reddit API was used to collect comments from r/Singapore for the period March 1st, 2020, to October 29th, 2021. For each Reddit comment containing predefined COVID-related keywords, the comment’s post ID was used to identify COVID-related threads. The cleaned dataset contains 11272 unique comments. NLTK’s
in-built VADER lexicon-based classifier was used to assign a 'compound' score to each Reddit comment.

Compound score
- Calculated by summing valence scores of each word
- Normalized to be between -1 (most extreme negative) and +1 (most extreme positive)


Positive and negative score
- Positive: compound score ≥0.5
- Negative: compound score ≤-0.5

| Category      | Example | Compound score    |
| :----:   |    :----:   |  :----: |
| Positive      | "100%, we're really quite blessed to have a government which is reacting  appropriately at most steps."  | 0.667  |
| Negative   | "yea but will the government and police go through all that, which will take time, or lock us down again and backtrack on their endemic rhetoric?  unfortunately i think it’s the latter. fed up of this shit"        | -0.874     |

## Hypothesis 

Three significant periods in Singapore’s COVID-19 timeline are analysed: Lockdown (3 April – 2 June 2020), Heightened Alert (16 May – 22 July 2021) and Stabilisation Phase (2 September 2021 - 21 November 2021).

1. Number of comments made during the Stabilisation Phase is higher than other key periods of COVID-19
2. Negative sentiment during the Stabilisation phase is more intense than other key periods of COVID-19

## Data Analysis

To track changes in key sentiment variables over time, moving averages with a time window of 30 days were generated:
- Total number of comments per day
- Proportion of positive/negative comments per day 
- Average compound score per day

The Kolmogorov-Smirnov test (KS test) was used to determine whether key sentiment variables changed during the Stabilisation Phase compared to other key periods. The KS test determines whether two data sets come from the same distribution by comparing their cumulative distributions. By using the KS test, we can study the continuous distribution of sentiment variables in each period without having to make assumptions about the underlying cumulative distribution function. For baseline measures, the KS-test was also used against all data since March 2020 (since COVID-19).

### Quantity of Discussion

![image](https://user-images.githubusercontent.com/55981443/144286687-98aacf77-4fef-4ad8-ac10-9fbad70ac00b.png)

The results suggest that the total number of comments per day during Stabilisation Phase shows a different distribution than during Lockdown and Heightened Alert 1 (p < 0.05). Q-Q plots (D & E) are used to compare the distribution of two samples. By plotting the quantiles of the Stabilisation phase data set against the quantiles of the comparison data sets (D, E), we observe that the total number of comments per day tended to be higher during Stabilisation Phase than during Lockdown and Heightened Alert.

### Negative Sentiment of Discussion

![image](https://user-images.githubusercontent.com/55981443/144286194-6afdf843-cff7-42ed-ac3c-317f93e470f0.png?style=centerme)

The results suggest that the proportion of negative comments per day and the compound score per comment during the Stabilisation Phase shows a different distribution than those during Heightened Alert (p < 0.05). The compound score of each comment was used instead of the average score per day to reflect the distribution of extreme sentiments.

Kernel density plots (H & I) are a variation of histograms used to determine distribution shape. The Q-Q plot in F shows a right skew, suggesting a higher proportion of negative comments per day during Heightened Alert than during Stabilisation Phase. In H, this corresponds to a flattening of the left tail of the distribution curve. It is difficult to discern the relationship between distributions in G. In I, we observe a slight flattening of the right tail of the distribution curve from Heightened Alert to Stabilisation Phase. Specifically, the proportion of positive comments over total comments decreased from 0.242 to 0.205.

# References

- [VADER Documentation](github.com/cjhutto/vaderSentiment)
