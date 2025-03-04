# Service Operations Analytics Dashboard

## Overview
This dashboard provides a view of service operations data for the period of January 1 - December 31, 2024. It visualizes service operations key performance indicators (KPIs) and trends from multiple datasets.

## Data Sources
[Service Operations Sample Dataset.xlsx](https://github.com/user-attachments/files/19060319/Service.Operations.Sample.Dataset.xlsx)

![Service Operations Analytics Dashboard](https://github.com/user-attachments/assets/dd8b774b-69ea-4eea-a1e1-0d1f8f5fe444)

The live dashboard can be viewed using PowerBI [on](./Service Analytics Dashboard.pbix)

The dashboard is built using the following datasets:

1. **Ticket Data**: Service ticket entries from January 1 - December 31, 2024
2. **Agent Scheduling Information**: Daily scheduling data for 6 agents over January - December, 2024
3. **Customer Information**: Data for 15 customers (C001-C015)
4. **Historical Ticket Trends**: Monthly aggregated data for all of 2024
5. **SLA Targets by Priority**: Service Level Agreement (SLA) targets for each priority level (Critical, High, Medium, Low)

## Dashboard Components
### Key Metrics (Top Row)
- **Tickets**: Total number of tickets (112)
- **Average Resolution Time**: Average time to resolve tickets in hours (6.50)
- **SLA Compliance**: Percentage of tickets resolved within SLA targets (85.29%)
- **Average CSAT Score**: Customer Satisfaction (CSAT) rating (3.80 out of 5)

## Charts and Visualizations
### Monthly Ticket Volume by Team
- Line chart showing ticket volume trends across the year
- Segmented by three teams: Account Management, Customer Service, and Technical Support
- Reveals seasonality with high volumes in January and December
- Shows relatively consistent volumes throughout the rest of the year

### SLA Compliance by Priority
- Horizontal bar chart showing SLA compliance rates for each priority level
- Medium priority tickets have the highest compliance rate
- Critical and High priority tickets show good compliance
- Low priority tickets have lower compliance rates, suggesting potential resource allocation issues

### Agent Performance
- Scatter plot showing the relationship between resolution time and CSAT scores
- Chart shows some performance variations in resolution time but CSAT score is the same among the 6 agents (David Wilson, Emily Davis, Jennifer Lee, John Smith, Michael Brown, Sarah Johnson)
- Helps identify agents who need additional training or who demonstrate best practices

### Tickets Distribution by Team and Communication Channel
- Stacked bar chart showing distribution of tickets across teams and communication channels
- Teams: Technical Support, Account Management, Customer Service
- Channels: Chat, Email, Phone
- Shows channel preferences for different teams


## Data Transformation
### Data Preprocessing
- Created a column named month in "Agent scheduling Information"
- Created two columns named "month" and "year" which extracted the respective month and year from "date" in from "Service Operations"

### Table Modelling Steps
- Ticket Data to Customer Data: Connect using customer_id
- Ticket Data to Agent Schedule: Connect using agent_id and month
- Ticket Data to Monthly Metrics: Connect using month field
- Ticket Data to SLA Targets: Connect using priority field

## Applicability
1. **Monthly Planning**: Review agent performance and SLA compliance
2. **Quarterly Review**: Assess team performance and identify improvement areas
