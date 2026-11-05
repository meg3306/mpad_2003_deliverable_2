Date: November 4, 2026  
Course: MPAD 2003 Introductory Data Storytelling  
Student: Emilie Megan Kazadi 
Presented to Jean-Sébastien Marier 

# Deliverable 2: Exploratory Data Analysis - Ottawa 311 Housing Complaints


## 1. Getting Data

For this exploratory data analysis (EDA), I am investigating municipal code enforcement and landlord accountability across Ottawa's 24 electoral wards using official municipal open data. The primary source for this analysis is the [City of Ottawa 311 Service Requests](https://open.ottawa.ca/search?q=311%20Service%20Requests) dataset, published on the Open Ottawa portal. 

To prepare the dataset for analysis, I downloaded the raw CSV file from Open Ottawa and imported it into Google Sheets by selecting **File > Import > Upload** and converting the file into a native Google Sheets workbook. The dataset can be accessed and reviewed via this public link: [Public 311 Dataset on Google Sheets](https://docs.google.com/spreadsheets/d/1fOboSIXGo16XOb3LthHVG-RAPcQN8D3IzvEiu214r8A/edit?usp=sharing).

![Raw Dataset in Google Sheets](raw_data.jpg)

## 2. Understanding Data

### 2.1. VIMO Analysis

To assess the accuracy, validity, and overall quality of the City of Ottawa 311 Service Requests dataset, I conducted a systematic **VIMO analysis** (**V**alid, **I**nvalid, **M**issing, and **O**utlier data values) focusing on key enforcement variables (Statistics Canada, 2021). Accuracy is one of the foundational dimensions of data quality, ensuring that administrative records reflect municipal reality (Statistics Canada, 2021).


 **Valid Data:** The majority of entries in `WARD_NAME` and `CREATED_DATE` represent valid administrative records that conform to standard municipal naming conventions across Ottawa's 24 electoral wards.

 **Invalid Data:** Initial frequency distributions revealed formatting inconsistencies within qualitative labels. For instance, several `SUBJECT` entries contained trailing whitespaces (e.g., `"Property Standards "` vs `"Property Standards"`), causing identical complaint categories to be processed as separate groups (Marier, 2021).

 **Missing Data:** Unresolved 311 tickets contained blank `CLOSED_DATE` cells. As Statistics Canada (2021) emphasizes, missing values must not be confused with zeros; a blank closure date indicates an active ongoing municipal investigation rather than a zero-day resolution time.

 **Outlier Data:** Calculating resolution durations revealed extreme statistical outliers. While the average response time for vital service complaints was approximately 12 days, select property standard cases in lower-income urban wards exceeded 180 days before ticket closure.


### 2.2. Cleaning Data

To transform the raw administrative file into a clean dataset, I executed three data-cleaning operations in Google Sheets:
1. **Whitespace Removal & Duplicate Filtering:** Using **Data > Data cleanup > Trim whitespace**, I eliminated leading and trailing spaces across all categorical text columns. I then used **Remove duplicates** to verify record uniqueness.
2. **Formula-Based Duration Calculation:** To measure enforcement delays, I created a new calculated column (`RESPONSE_TIME_DAYS`) and implemented a conditional date difference formula:
   ```excel
   =IF(ISBLANK(C2), "", DATEDIF(B2, C2, "D"))

### 2.3. Analyzing Data

To examine wheter municipal code enforcement delays vary across Ottawa's geographic areas, I conducted an exploratory data analysis in Google Sheets using a pivot table and an exploratory column chart. I specifically selected `WARD_NAME`, `TICKET_ID`, and `RESPONSE_TIME_DAYS` because comparing ticket counts alongside average resolution durations across electoral wards directly tests my core research hypothesis.

## Pivot Table Setup

I made a Pivot Table with `WARD_NAME` in the rows, summarizing `TICKET_ID` using **COUNTA** (to measure total complaint volume per ward) and `RESPONSE_TIME_DAYS` using **AVERAGE** (to calculate mean resolution duration in days).

![Pivot Table Summary of 311 Complaints by Ward](pivot_table.png)

## Exploratory Visualization

Using the pivot table summary, I generated an **exploratory bar chart** comparing average response times across Ottawa's electoral wards.

![Exploratory Chart of Response Duration by Ward](exploratory_chart.png)

## Key Analytical Findings & Journalistic Story Angle

 **Geographic Disparities:** Wards in Ottawa's urban core—such as **Rideau-Vanier (Ward 12)** and **Somerset (Ward 14)**—log high volumes of property standards complaints and experience an average resolution delay of **24.5 days**.
* **Suburban Comparison:** By contrast, suburban wards such as **Kanata South (Ward 23)** and **Barrhaven East (Ward 24)** average significantly shorter resolution times of **8.2 days**.
* **Standout Statistic:** Urban core tenants wait nearly **three times longer** on average for municipal enforcement action on property standards compared to suburban property owners.
* **Potential News Story:** These statistical findings point toward a compelling investigative story: *a systemic municipal code enforcement gap where low-income tenants in urban core wards face prolonged delays for vital housing repairs compared to residents in suburban areas.*
* **Variables for Further Investigation:** Next steps would require analyzing `SUBJECT` (to break down response times by specific complaint sub-types like heating vs. noise) and cross-referencing ward boundaries with Statistics Canada median income data.

## 3. Delivering Data

## Further Investigative Story angle

While the exploratory data analysis confirms a geographic gap in municipal code enforcement times between urban core and suburban wards, fully reporting this story requires moving beyond administrative data to examine human impacts and policy roots. To develop a comprehensive news story, I would investigate the core question: Are low-income tenants in Ottawa's ubran core facing systemic municipal neglect when reporting vital housing violations compared to property owners in high-income surburban wards?

## Additional Data & Records Needed

To ground this investigation, quantitative 311 metrics must be combined with institutional records:
1. **Freedom of Information (FOI) Requests:** Submitting municipal access requests for internal By-law inspection logs, inspector staffing allocations per ward, and escalation histories for repeat-offender landlords.
2. **Socioeconomic Cross-Referencing:** Mapping 311 complaint density against Statistics Canada census data for median household income and tenant proportions across Ottawa's 24 electoral wards.

## Expert & Community Interview

To humanize the data, I would conduct qualitative interviews with key stakeholders:
**Tenant Advocate:** A spokesperson from **Ottawa ACORN** (Association of Community Organizations for Reform Now) to discuss systemic landlord negligence and tenant intimidation.
**City Enforcement Official:** The Director of **City of Ottawa By-law and Regulatory Services** to address why response delays are longer in urban core wards and whether staffing shortages exist.
**Affected Resident:** A tenant residing in Ward 12 (Rideau-Vanier) who has experienced unaddressed heating failures or pest infestations during winter months.

## Contextual Sources

**Ottawa ACORN Community Survey:** Reports on housing conditions and landlord accountability in tenant-heavy Ottawa neighborhoods.
**Social Planning Council of Ottawa (SPCO)** Data reports analyzing low-income housing equity and neighborhood inequality across municipal wards.

## 4. References

* Gray, J., Chambers, L., & Bounegru, L. (Eds.). (2012). *The Data Journalism Handbook: How Journalists Can Use Data to Improve the News*. O'Reilly Media. https://datajournalism.com/search?q=The+Data+Journalism+Handbook%3A+How+Journalists+Can+Use+Data+to+Improve+the+New 
* Statistics Canada. (2020). *Data accuracy and validation: Methods to ensure the quality of data* (Catalogue No. 892000062020008). Government of Canada. https://www.statcan.gc.ca/en/wtc/data-literacy/catalogue/892000062020008
* Statistics Canada. (2021). *Assessing data in a time of misinformation: A step-by-step guide* [PDF]. Government of Canada. https://www.statcan.gc.ca/en/wtc/data-literacy/catalogue/assessing-data-time-misinformation.pdf
* Statistics Canada. (2021). *Statistics: Power from Data!* Government of Canada. https://www150.statcan.gc.ca/n1/edu/power-pouvoir/toc-tdm/5214718-eng.htm

## AI Disclosure Statement

I used AI assistant during the preparation of this assignment. The AI was used to assist with formatting the Markdown structure, troubleshooting Git/GitHub terminal commands, and reviewing report syntax. All dataset cleaning, pivot table calculations, visual chart design, data interpretations, and final reporting decisions were performed independently by me(Emilie Megan Kazadi).