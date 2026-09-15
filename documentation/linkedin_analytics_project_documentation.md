# LinkedIn Analytics Project Documentation

## 1\. Project Background

This project is an individual business analytics project focused on evaluating the performance of LinkedIn content before and after sponsored promotion.

The analysis focused on five LinkedIn posts that were selected from approximately the previous 18 months of content based on their reach, impressions, and engagement. The selected posts were assigned the identifiers P01–P05.

The five selected posts were subsequently sponsored/boosted, allowing their organic and sponsored performance to be compared during the analysis period of 1–31 March 2026.

The objective was to understand how paid promotion affected content reach and engagement and to identify useful patterns that could support future LinkedIn content and promotion decisions.





## 2\. Business Problem

The business needed to understand whether sponsoring selected LinkedIn posts improved their performance compared with their organic distribution.

The analysis, therefore focused on comparing organic and sponsored results across key performance indicators, including:

* Impressions
* Clicks
* Reactions
* Engagement rate
* Click-through rate (CTR)

The analysis also examined performance by content type and at the individual-post level.





## 3\. Project Objectives

The project objectives were to:

1. Compare organic and sponsored LinkedIn performance.
2. Measure the effect of sponsorship on impressions and clicks.
3. Compare engagement efficiency between organic and sponsored content.
4. Evaluate performance across Carousel and Video content.
5. Analyse the performance of each selected post individually.
6. Develop an interactive Power BI dashboard to communicate the findings.
7. Provide business recommendations based on the results.



## 4\. Data Sources

LinkedIn provided three Excel datasets:

* Content data
* Followers data
* Visitors data

The datasets were brought into an analytical Excel workbook for preparation and analysis.

The final Power BI analysis focused on the content-related data used to compare organic and sponsored performance. The followers and visitors datasets were collected as part of the available LinkedIn exports but were not used in the final Power BI analysis.



## 5\. Post Selection

Approximately 18 months of LinkedIn content was reviewed to identify five strong-performing posts.

The selection considered:

* Reach
* Impressions
* Engagement

The selected posts were assigned internal identifiers:

|Post ID|Content Type|
|-|-|
|P01|Carousel|
|P02|Video|
|P03|Carousel|
|P04|Carousel|
|P05|Video|

These identifiers were used throughout the analytical workbook and Power BI report.



## 6\. Analysis Period

The final comparative analysis covered:

**1–31 March 2026**

This period represents the analysis window used to evaluate the organic and sponsored performance of the selected posts.



## 7\. Data Preparation in Excel and Power Query

The LinkedIn data was brought into an analytical Excel workbook and connected to Power BI.

Power Query was then used to prepare the dataset for analysis.


### 7.1 Promote Headers

The first row of the imported dataset was promoted to become the column headers.

```powerquery
= Table.PromoteHeaders(Sheet1\_Sheet, \[PromoteAllScalars=true])
```

### 7.2 Change Data Types

Appropriate data types were assigned to the fields.

Examples include:

* `Post ID` → Text
* `Date` → Date
* Impressions, clicks, reactions, comments and reposts → Whole number
* Engagement rates → Decimal number

This ensured that the fields were suitable for analysis and Power BI calculations.


### 7.3 Remove Unnecessary Columns

The following fields were removed because they were not required for the organic-versus-sponsored analysis:

* `Impressions (total)`
* `Impressions (organic)`
* `Clicks (total)`
* `Reactions (total)`
* `Comments (total)`
* `Reposts (total)`
* `Engagement rate (total)`

The resulting dataset retained the fields required for the organic and sponsored comparison.


### 7.4 Add Content Type

A conditional column named `Content Type` was added based on the Post ID.

The mapping was:

|Post ID|Content Type|
|-|-|
|P01|Carousel|
|P02|Video|
|P03|Carousel|
|P04|Carousel|
|P05|Video|

This additional field enabled the dashboard to analyse performance by content format.


### 7.5 Reorder Columns

The columns were reordered into a logical analytical sequence, placing the post identifier and date first, followed by performance metrics, content type and engagement metrics.



## 8\. Power BI Calculations

Measures were created in Power BI to support the organic and sponsored performance comparison.


### 8.1 Average Engagement Rate

**Organic**

```DAX
Average Engagement Rate =
AVERAGE(Data\[Engagement rate (organic)])
```

**Sponsored**

```DAX
Average Engagement Rate (Sponsored) =
Average(Data\[Engagement rate (sponsored)])
```


### 8.2 Total Clicks

**Organic**

```DAX
Total Clicks (Organic) =
SUM(Data\[Clicks (organic)])
```

**Sponsored**

```DAX
Total Clicks (Sponsored) =
SUM(Data\[Clicks (sponsored)])
```


### 8.3 Total Impressions

**Organic**

```DAX
Total Impressions (Organic) =
SUM(Data\[Unique impressions (organic)])
```

**Sponsored**

```DAX
Total Impressions (Sponsored) =
SUM(Data\[Impressions (sponsored)])
```


### 8.4 Organic CTR

An overall Organic CTR measure was created:

```DAX
Total Organic CTR =
CALCULATE(
    DIVIDE(
        SUM(Data\[Clicks (organic)]),
        SUM(Data\[Unique impressions (organic)])
    )
)
```


### 8.5 Total Reactions

**Organic**

```DAX
Total Reactions (Organic) =
SUM(Data\[Reactions (organic)])
```

**Sponsored**

```DAX
Total Reactions (Sponsored) =
SUM(Data\[Reactions (sponsored)])
```


### 8.6 CTR ORGANIC Calculated Table

A separate calculated table named `CTR ORGANIC` was created using `SUMMARIZE()`.

```DAX
CTR ORGANIC =

SUMMARIZE(
    Data,
    Data\[Post ID],
    "Organic CTR",
    DIVIDE(
        SUM(Data\[Clicks (organic)]),
        SUM(Data\[Unique impressions (organic)]),
        0
    )
)
```

This table provides an Organic CTR calculation at the Post ID level.



## 9\. Power BI Dashboard Development

The Power BI report contains seven pages:

1. Organic Performance Review
2. Sponsored Performance Review
3. P01
4. P02
5. P03
6. P04
7. P05

The report was designed to provide both an overall performance view and individual post-level comparisons.



## 10\. Organic Performance Review

The Organic Performance Review page contains four KPI cards:

* Total Impressions
* Total Clicks
* Total Reactions
* Average Engagement Rate

The page also contains:


### Line and Stacked Column Chart

**Clicks vs Engagement Rate by Content Type (Carousel vs Video)**


### Pie Chart

**Clicks (Organic)**


### Clustered Bar Chart

**Engagement Rate (Organic)**


### Stacked Column Chart

**Reactions (Organic)**


### Area Chart

**Impressions (Organic)**



## 11\. Sponsored Performance Review

The Sponsored Performance Review page contains four KPI cards:

* Total Impressions
* Total Clicks
* Total Reactions
* Average Engagement Rate

The page also contains:


### Line and Stacked Column Chart

**Clicks vs Engagement Rate by Content Type (Carousel vs Video)**


### Pie Chart

**Clicks (Sponsored)**


### Clustered Bar Chart

**Engagement Rate (Sponsored)**


### Stacked Column Chart

**Reactions (Sponsored)**


### Area Chart

**Impressions (Sponsored)**


The organic and sponsored pages use a similar structure to make performance comparisons easier.



## 12\. Post-Level Analysis

Five individual pages were created for P01–P05.

Each post-level page contains filters for:

* Start Date
* End Date
* Content Type


The pages use clustered bar charts to compare organic and sponsored performance for:

* Impressions
* Engagement Rate
* Clicks
* Reactions

This provides a more detailed view of how sponsorship affected each individual selected post.



## 13\. Key Performance Results

The analysis produced the following overall results:

|KPI|Organic|Sponsored|
|-|-:|-:|
|Impressions|2.23K|15.6K|
|Clicks|397|573|
|Average Engagement Rate|14%|7.83%|
|Reactions|53|14|

These results show that sponsored promotion substantially increased visibility and clicks, while organic content produced stronger engagement efficiency and more reactions.


## 14\. Key Findings

### 14.1 Sponsored Promotion Increased Visibility

Sponsored content generated approximately seven times the impressions of organic content.

This indicates that paid promotion was effective at expanding content reach and visibility.


### 14.2 Sponsored Content Generated More Clicks

Sponsored content generated 573 clicks compared with 397 organic clicks.

This shows that paid distribution increased the volume of clicks, although the increase in clicks was considerably smaller than the increase in impressions.


### 14.3 Organic Content Had Stronger Engagement Efficiency

The average organic engagement rate was 14%, compared with 7.83% for sponsored content.

Organic engagement rate was therefore substantially higher than sponsored engagement rate.


### 14.4 Organic Content Generated More Reactions

Organic content generated 53 reactions compared with 14 reactions from sponsored content.

This indicates stronger interaction efficiency from the organic distribution of the selected content.


### 14.5 Content Type Performance

The dashboard also compared Carousel and Video content using clicks and engagement rate.

The analysis indicated that carousel content performed strongly for clicks and engagement compared with video content.



## 15\. Business Recommendations

Based on the analysis, the following recommendations were identified:

1. **Use sponsorship to increase reach and visibility.** Paid promotion can be useful when the primary objective is to expose content to a larger audience.
2. **Amplify strong organic performers.** Content that already demonstrates strong organic engagement can be considered for paid amplification.
3. **Prioritize carousel content for interaction.** The analysis indicated strong performance from carousel content for clicks and engagement.
4. **Improve targeting for sponsored campaigns.** Since sponsored reach increased substantially while engagement efficiency was lower, audience targeting and campaign optimisation should be reviewed.
5. **Strengthen content hooks and calls to action.** Improving the opening message and CTA may help convert increased sponsored reach into stronger engagement.



## 16\. Project Limitations

The analysis focused on five selected LinkedIn posts and the 1–31 March 2026 analysis period.

The five posts were selected based on their previous performance in terms of reach, impressions and engagement. Therefore, the results should be interpreted in the context of these selected posts rather than as a complete assessment of every LinkedIn post.

The followers and visitors datasets were available but were not used in the final Power BI analysis.



## 17\. Data Privacy

The underlying LinkedIn data originated from company analytics and may contain confidential, commercially sensitive or restricted business information.

Before publicly distributing this project, any information that is not authorised for public release should be removed, anonymised or replaced with a portfolio-safe dataset.

The GitHub repository should therefore only contain data and supporting materials that are approved for public distribution.



## 18\. Project Outcome

This project produced an interactive Power BI report for evaluating the performance of selected LinkedIn posts before and after sponsored promotion.

The analysis demonstrated that:

* Sponsored promotion was effective for increasing visibility and clicks.
* Organic distribution produced stronger engagement efficiency and more reactions.
* Content format was a useful dimension for comparing performance.
* Post-level analysis provided additional insight into how individual posts responded to sponsorship.

The project demonstrates an end-to-end business analytics workflow involving data preparation, Power Query transformation, DAX calculations, data visualisation, comparative analysis and business recommendations.



## 19\. Skills Demonstrated

This project demonstrates practical experience in:

* Excel data preparation
* Power Query
* Power BI
* DAX
* Data transformation
* KPI development
* Data visualisation
* Organic vs sponsored performance analysis
* Content performance analysis
* Post-level analysis
* Business insight generation
* Data-driven recommendations
* Git and GitHub project documentation



## 20\. Repository Structure

```text
linkedin-analytics/
│
├── .gitignore
├── README.md
├── project-status.txt
│
├── assets/
│   ├── organic-performance-review.png
│   ├── sponsored-performance-review.png
│   └── post-level-analysis.png
│
├── data/
│   └── processed/
│       └── linkedin-analytics-data.xlsx
│
├── documentation/
│   └── linkedin-analytics-project-documentation.md
│
├── power-bi/
│   └── linkedin-analytics-dashboard.pbix
│
└── reports/
```


## 21\. Author

**Gifty Kumah**

Business Analytics 



