# **LinkedIn Analytics Data Dictionary**



## Purpose



This data dictionary documents the fields used in the LinkedIn Analytics project and explains their meaning, data type, and role in the analysis.



The analysis compares the performance of organic and sponsored LinkedIn content for five selected posts during the period 1–31 March 2026.



\---



Core Fields

---

|Field|Data Type|Definition|Analytical Use|
|-|-|-|-|
|Post ID|Text|Identifier assigned to each of the five selected posts: P01–P05|Used to distinguish and compare individual posts|
|Date|Date|Date associated with the LinkedIn performance record|Used for date filtering and analysis|
|Content Type|Text|Identifies the format of the post: Carousel or Video|Used to compare performance by content format|



\---



Organic Performance Fields

---

|**Field**|**Data Type**|**Definition**|**Analytical Use**|
|-|-|-|-|
|Impressions (organic)|Numeric|Number of impressions generated through organic distribution|Measures organic visibility|
|Unique impressions (organic)|Numeric|Number of unique organic impressions|Used as the reach-related denominator in the organic CTR calculation|
|Clicks (organic)|Numeric|Number of clicks generated through organic distribution|Measures organic click activity|
|Reactions (organic)|Numeric|Number of reactions generated through organic distribution|Measures organic audience response|
|Engagement rate (organic)|Percentage|Engagement rate associated with organic distribution|Measures organic engagement efficiency|



\---



Sponsored Performance Fields

---

|**Field**|**Data Type**|**Definition**|**Analytical Use**|
|-|-|-|-|
|Impressions (sponsored)|Numeric|Number of impressions generated through sponsored or paid distribution|Measures paid visibility|
|Clicks (sponsored)|Numeric|Number of clicks generated through sponsored distribution|Measures paid click activity|
|Reactions (sponsored)|Numeric|Number of reactions generated through sponsored distribution|Measures paid audience response|
|Engagement rate (sponsored)|Percentage|Engagement rate associated with sponsored distribution|Measures sponsored engagement efficiency|



\---


### Power BI Measures



The following measures were created in Power BI to support the dashboard analysis.



|**Measure**|**Type**|**Definition**|
|-|-|-|
|Average Engagement Rate|Measure|Calculates the average organic engagement rate|
|Average Engagement Rate (Sponsored)|Measure|Calculates the average sponsored engagement rate|
|Total Clicks (Organic)|Measure|Calculates total organic clicks|
|Total Clicks (Sponsored)|Measure|Calculates total sponsored clicks|
|Total Impressions (Organic)|Measure|Calculates total organic impressions using the `Unique impressions (organic)` field|
|Total Impressions (Sponsored)|Measure|Calculates total sponsored impressions|
|Total Organic CTR|Measure|Calculates organic click-through rate using organic clicks divided by unique organic impressions|
|Total Reactions (Organic)|Measure|Calculates total organic reactions|
|Total Reactions (Sponsored)|Measure|Calculates total sponsored reactions|



\---



### DAX Definitions



Average Engagement Rate = AVERAGE(Data\[Engagement rate (organic)])



* Average Engagement Rate (Sponsored) = AVERAGE(Data\[Engagement rate (sponsored)])



* Total Clicks (Organic) = SUM(Data\[Clicks (organic)])



* Total Clicks (Sponsored) = SUM(Data\[Clicks (sponsored)])



* Total Impressions (Organic) = SUM(Data\[Unique impressions (organic)])



* Total Impressions (Sponsored) = SUM(Data\[Impressions (sponsored)])



* Total Organic CTR = CALCULATE(

&#x20;                              DIVIDE(

&#x20;                                      SUM(Data\[Clicks (organic)]),

&#x20;                                      SUM(Data\[Unique impressions (organic)])

&#x20;                                 )

&#x20;                               )





* Total Reactions (Organic) = SUM(Data\[Reactions (organic)])



* Total Reactions (Sponsored) = SUM(Data\[Reactions (sponsored)])



* Calculated Table


CTR ORGANIC: CTR ORGANIC is a calculated table created in Power BI.

It summarizes organic click-through rate by post.
The table provides an organic CTR value for each Post ID and supports post-level performance analysis.



CTR ORGANIC =

SUMMARIZE(

&#x20;   Data,

&#x20;   Data\[Post ID],

&#x20;   "Organic CTR",

&#x20;   DIVIDE(

&#x20;       SUM(Data\[Clicks (organic)]),

&#x20;       SUM(Data\[Unique impressions (organic)]),

&#x20;       0

&#x20;   )

)


---

Content Type Mapping

---

The five selected posts were assigned the following content types:



|Post ID|Content Type|
|-|-|
|P01|Carousel|
|P02|Video|
|P03|Carousel|
|P04|Carousel|
|P05|Video|



The Content Type field was added during the Power Query transformation process.

---

Fields Removed During Power Query
---



The following fields were removed during data preparation because they were not required in the final analytical model:



* Impressions (total)
* Impressions (organic)
* Clicks (total)
* Reactions (total)
* Comments (total)
* Reposts (total)
* Engagement rate (total)


**Important Note**



Impressions (organic) was removed during Power Query.



For the final Power BI model, organic visibility was represented using Unique impressions (organic), which was also used as the denominator in the organic CTR calculation.

This distinction is important when interpreting the Power BI measures.


\---



### Data Preparation Context



The data preparation process included the following Power Query steps:



* Promoted headers.
* Changed data types.
* Removed unnecessary columns.
* Added the Content Type field.
* Reordered columns.



The prepared dataset was then connected to Power BI for modelling, calculation, visualization, and analysis.

---

Analytical Scope
---



The final analysis focuses on:



* Organic impressions and visibility
* Sponsored impressions and visibility
* Organic clicks
* Sponsored clicks
* Organic reactions
* Sponsored reactions
* Organic engagement rate
* Sponsored engagement rate
* Organic click-through rate
* Performance by post
* Performance by content type


---


### Interpretation Notes



The metrics are intended to answer two main business questions:



**Visibility**: Did sponsored promotion increase the reach and visibility of the selected LinkedIn content?



**Engagement Efficiency:** Did the increased visibility generated through sponsorship translate into stronger audience engagement?



The analysis, therefore considers both scale (such as impressions and clicks) and efficiency (such as engagement rate and CTR).



\---





### Author

Gifty Dedaah Kumah



