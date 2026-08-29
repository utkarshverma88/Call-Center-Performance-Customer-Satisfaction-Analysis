# Call Center Performance & Customer Satisfaction Analysis

## Project Overview
This project presents an interactive Power BI dashboard designed to monitor and analyze Call Center operations, key service level metrics, agent performance, and customer satisfaction (CSAT) scores. Using transactional call logs, the dashboard tracks critical call center KPIs, identifies operational bottlenecks across support topics, and ranks agent effectiveness to enable data-driven workforce management.

## Objectives
* **Operational Monitoring:** Track overall call volume, answer rates, and Service Level Agreement (SLA) compliance over time.
* **Agent Performance Management:** Evaluate agent effectiveness through CSAT rankings, call volumes, and resolution success rates.
* **Topic & Issue Breakdown:** Identify service friction across support categories (e.g., Streaming, Admin, Technical Support) by measuring average speed of answer and customer satisfaction.

---

## Dashboard Structure & Pages

### 1. Executive Summary & SLA Tracking

<img width="1399" height="793" alt="Screenshot 2026-08-29 011825" src="https://github.com/user-attachments/assets/fa031d9c-41e4-458f-b00e-bfd97f9cb602" />

Focuses on macro-level operational metrics and time-series performance:
* **KPI Cards:**
  * **Total Calls:** 5K
  * **Answer Rate:** 81.1%
  * **SLA % within 20sec:** 32.6%
  * **Resolution Rate:** 89.9%
  * **Average CSAT:** 3.40 / 5.00
* **Trend Analysis Chart:** Dual-axis line chart tracking `Total Calls` against `SLA % (Rolling 7-day)` across timeline filters (Jan 2021 – Mar 2021).

### 2. Agent Performance Analytics
<img width="1401" height="794" alt="Screenshot 2026-08-29 011849" src="https://github.com/user-attachments/assets/4003a2eb-bd34-4641-ab43-d093c6805fb3" />

Evaluates individual call center staff against volume, resolution quality, and customer satisfaction:
* **Agent Performance Table:** Ranks agents based on `Average_CSAT`, displaying `Total_Calls`, `Resolution_Rate`, and `Agent_CSAT_Rank` (e.g., Martha ranking #1 with 3.47 CSAT, Dan #2 at 3.45, through Joe #8 at 3.33).
* **CSAT Breakdown Bar Chart:** Horizontal bar chart comparing CSAT scores across all active agents.
* **Resolution Rate Gauge:** Target gauge visualizing total resolution rate (89.9%).
* **Topic Slicers:** Quick-filter buttons for Admin Support, Payment Related, Technical Support, Contract Related, and Streaming.

### 3. Topic & Speed of Answer Analysis
<img width="1402" height="798" alt="Screenshot 2026-08-29 011907" src="https://github.com/user-attachments/assets/8431ba18-426d-4726-89b3-26549072a7b3" />

Drills down into specific support categories and operational efficiency:
* **Topic Summary Matrix:** Detailed view of call volume, average speed of answer (seconds), resolution rate, and CSAT per topic.
  * *Technical Support:* Highest CSAT (3.62) with lowest speed of answer (~66.83s).
  * *Streaming:* Lowest CSAT (3.16) with highest speed of answer (~70.43s).
* **Interactive Slicers:** Dynamic toggles for `Answered (Y/N)` and `Resolved (Y/N)`.

---

## Data Model & Key DAX Measures

### Primary Measures
```dax
// Total Calls Count
Total_Calls = COUNT('Call_Center_Data'[Call_ID])

// Answer Rate Percentage
Answer_Rate = 
DIVIDE(
    CALCULATE(COUNT('Call_Center_Data'[Call_ID]), 'Call_Center_Data'[Answered] = "Y"),
    [Total_Calls],
    0
)

// Resolution Rate Percentage
Resolution_Rate = 
DIVIDE(
    CALCULATE(COUNT('Call_Center_Data'[Call_ID]), 'Call_Center_Data'[Resolved] = "Y"),
    CALCULATE(COUNT('Call_Center_Data'[Call_ID]), 'Call_Center_Data'[Answered] = "Y"),
    0
)

// Average CSAT Rating
Average_CSAT = AVERAGE('Call_Center_Data'[Satisfaction_Rating])

// Agent CSAT Ranking
Agent_CSAT_Rank = 
RANKX(
    ALL('Call_Center_Data'[Agent]), 
    [Average_CSAT], 
    , 
    DESC, 
    Dense
)
```

## Key Findings & Insights
* **Service Level Bottleneck:** While overall resolution rate remains high (89.9%), only 32.6% of calls are answered within the target 20-second SLA, indicating potential staffing shortages during peak hours.
* **Topic Performance Variance:** Technical Support queries yield the highest customer satisfaction (3.62 CSAT), whereas Streaming queries receive the lowest satisfaction (3.16 CSAT) alongside higher wait times.
* **Balanced Agent Output:** Call distribution among agents is evenly split (~582 to 666 calls per agent), with top CSAT performers maintaining high overall resolution rates above 89%.

---

## Reports
* **Operational Dashboard:** Live interactive reporting detailing key metrics across volume, response rates, and customer satisfaction.
* **Performance Breakdown:** Comprehensive dynamic summaries dissecting service levels by both agent roster and individual inquiry categories.

---

## Conclusion
This project demonstrates the application of Power BI and DAX to address operational metrics in a customer support environment. By integrating service level metrics, issue breakdown, and agent evaluation into a single report, the dashboard provides the actionable clarity needed to streamline agent allocation and improve overall customer satisfaction.

---

## How to Use
1. **Clone the Repository:** Clone this project repository from GitHub.
2. **Open the Report:** Open the `.pbix` file using **Power BI Desktop**.
3. **Interact with Visuals:** Use date sliders, topic buttons, and status filters (Answered/Resolved) to drill down into specific call center segments.

---

**Author - utkarshutkarshverma88**  
*This project is part of my portfolio, showcasing the Power BI, DAX modeling, and dashboarding skills essential for data analyst roles. If you have any questions, feedback, or would like to collaborate, feel free to get in touch!*
