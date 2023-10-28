#  Call Center Analysis | Pwc Switzerland Power BI Virtual Case Experience 

## Table of contents
- [Problem Statement](https://github.com/calmk/PWC-Virtual-Case-Experience/tree/main/Task%202:%20Call%20Center%20Dashboard#Problem-Statement)
- [Data Preparation](https://github.com/calmk/PWC-Virtual-Case-Experience/tree/main/Task%202:%20Call%20Center%20Dashboard#Data-Preparation)
- [Data Modeling](https://github.com/calmk/PWC-Virtual-Case-Experience/tree/main/Task%202:%20Call%20Center%20Dashboard#Data-Modeling)
- [Data Visualization](https://github.com/calmk/PWC-Virtual-Case-Experience/tree/main/Task%202:%20Call%20Center%20Dashboard#Data-Visualization)

# Problem Statement

- **Problem:** The manager at PhoneNow (a big telecom company) is seeking transparency and insight into the Call Center dataset to gain an accurate overview of long-term customer and agent behavior trends.
- **Objective:** The purpose of this analysis is to create a dashboard in Power BI for Call Center Manager that reflects all relevant Key Performance Indicators (KPIs) and metrics to:
    - Self-exploratory call trends
    - Overview of the agent’s performance and behaviors
    - Overview the customer satisfaction
    
- **Possible KPIs** include (but are not limited to):
    - Overall customer satisfaction
    - Overall calls answered/abandoned
    - Calls by time
    - Average speed of answer
    - Agents performance quadrant -> average handle time(talk duration) vs calls answered

# Data Sourcing

The Dataset used for this analysis was provided by [Pwc Switzerland](https://www.pwc.ch/en/careers-with-pwc/students/virtual-case-experience.html) and available here: [Call Center Dataset](https://github.com/calmk/PWC-Virtual-Case-Experience/blob/main/Task%202%3A%20Call%20Center%20Dashboard/01%20Call-Center-Dataset.xlsx)
# Data Preparation

The dataset was loaded into Microsoft Power BI Desktop for transformation in Power Query and modeling.


### Data Cleaning

Data Cleaning for the dataset was done in Power Query as follows:

- added new columns
- Each of the columns in the table was validated to have the correct data type
### Data Transformation
- Number of answered ='Table.AddColumn(#"Changed Type", "Answered", each if [#"Answered (Y/N)"] = "Y" then 1 else 0)'
- Abandoned Rate = 'Table.AddColumn(#"Changed Type1", "Abandoned", each if [#"Answered (Y/N)"] = "N" then 1 else 0)'
- Number of resolved ='Table.AddColumn(#"Added Conditional Column1", "Query Resolved""", each if [#"Answered (Y/N)"] = "Y" and [Resolved] = "Y" then 1 else 0)'
- Number of not resolved 'Table.AddColumn(#"Changed Type2", "Query Not Resolved", each if [#"Answered (Y/N)"] = "Y" and [Resolved] = "N" then 1 else  0)'
- month = 'Table.AddColumn(#"Changed Type3", "Month Name", each Date.MonthName([Date]))'
- minute = 'Table.AddColumn(#"Changed Type4", "Minute", each Time.Minute([AvgTalkDuration]))'


# Data Modeling

After the dataset was cleaned and transformed, it was ready to be modeled, but the dataset just included one table, so the Data Modeling is nothing much to modify

# Data Visualization
![dashboard github](https://github.com/nargesanalytics/pwc_call_center/blob/main/Screenshot%202023-10-28%20204516.png)

### Measures
- Avg_satsifaction = AVERAGE('Call Center'[Satisfaction rating])
- Avg_speed_answer = AVERAGE('Call Center'[Speed of answer in seconds])
- Avg_talk_duration(sec) = AVERAGE('Call Center'[Total Talk Duration])
- call_not_answered = calculate(SUM('Call Center'[Answered] ))
- Calls_abandoned = SUM('Call Center'[Abandoned])
- Calls_answered = sum('Call Center'[Answered])
- Calls_not_answered = Calculate(distinctcount('Call Center'[Call Id]),Filter('Call Center','Call Center'[Answered (Y/N)]="N"))
- Calls_received = COUNT('Call Center'[Call Id])
- Calls_Resolved = sum('Call Center'[Query Resolved])
- Total_call = COUNT('Call Center'[Call Id])
  

