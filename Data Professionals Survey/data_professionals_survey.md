# Data Professionals Survey Dashboard

## Overview

This project analyzes [survey data](data_professionals_survey.xlsx) from 630 data professionals across various roles, countries, and experience levels. The dashboard provides insights into:
- Demographics (gender, country of residence, age)
- Job roles and salaries
- Programming language preferences
- Work satisfaction metrics (work/life balance, salary happiness)
- Perceived difficulty of breaking into the data field

## Data Transformation Process

### Preprocessing Steps

1. **Job Role Column Refinement**
   - Split entries containing "Others" into a separate column
   - Standardized job role classifications for consistent analysis

2. **Salary Data Transformation**
   - Converted salary ranges into usable numerical values
   - Split salary ranges into minimum and maximum values
   - Calculated average salary for each respondent

3. **Gender Data Processing**
   - Split gender data into two distinct columns (Male count & Female count)
   - Used binary encoding: 1 for presence, 0 for absence in each column
   - This enabled separate gender-based analyses

## Measures
### Quadrant Analysis Measures

#### Quadrant Line Assignment
This create colors for each quadrant in the plot where Quadrant 1 - Low Pay/High Satisfaction, Quadrant 2 - High Pay/High Satisfaction, Quadrant 3 - Low Pay/Low Satisfaction and Quadrant 4 - High Pay/Low Satisfaction.

```dax
CF Quadrants =
VAR TargetSalary = [Average Salary]<=[Salary Range Value]
VAR TargetHappiness = [Q6 - How Happy are you in your Current Position with the following? (Salary)]>=[Happiness with Salary Value]
VAR Result =
SWITCH(
    TRUE(),
    TargetSalary && TargetHappiness = FALSE(),1,
    TargetSalary && TargetHappiness, 2,
    TargetSalary = FALSE() && TargetHappiness = FALSE(), 3,
    TargetSalary = FALSE() && TargetHappiness, 4,
)
RETURN
    Result
```

#### Top Quadrant Specification on Plot

```dax
CF TopQuadrant =
VAR TargetSalary = [Average Salary]<=[Salary Range Value]
VAR TargetHappiness = [Q6 - How Happy are you in your Current Position with the following? (Salary)]>=[Happiness with Salary Value]
VAR Result =
    TRUE(),
       TargetSalary && TargetHappiness, 1,
0
)
RETURN
    Result

```

#### Male & Female Count

```dax
Male Count = SUM(data_professionals_survey[male count])
```

```dax
Female Count = SUM(data_professionals_survey[female count])
```

## Visualization 
The first visualization is pretty basic as there was not a lot of data transformation done but in the second visualization, measures was created to create some visualizations.



![Data Professionals Dashboard 1](https://github.com/user-attachments/assets/f3c7fe28-96c6-4961-82d5-5cb61bf141ac)



![Data Professionals Dashboard 2](https://github.com/user-attachments/assets/9129ce31-07c3-41b2-9823-6ac4faee60dc)

### Key Visualizations

1. **Salary vs. Happiness Analysis**
   - Created a scatter plot comparing salary with salary satisfaction
   - Inverted y-axis for more intuitive visualization
   - Developed a measure to divide the plot into meaningful quadrants
   - Added interactive slicers to allow adjustment of quadrant lines

2. **Difficulty to Break into Data Field**
   - Used color-coding to represent different difficulty levels
   - Applied a consistent color palette for visual clarity
   - Created both bar chart and donut chart representations

3. **Demographics Representation**
   - Displayed gender distribution using multi-row cards
   - Visualized total respondents (630), with breakdown of male (468) and female (162) participants

4. **Programming Language Preferences**
   - Used tree map and bar charts to show language popularity
   - Highlighted Python as the dominant language preference

5. **Geographic Distribution**
   - Visualized respondent distribution across countries
   - Used color-coded stacked bars to show job role distribution by country

### Quadrant Analysis Implementation

The scatter plot quadrant analysis in the second dashboard was a key feature that required specific technical implementation:

1. **Creating Reference Lines:**
   - Created two DAX measures to establish horizontal and vertical reference lines
   - The horizontal line represents the threshold for "high" vs "low" salary
   - The vertical line represents the threshold for "high" vs "low" happiness

2. **Interactive Threshold Control:**
   - Implemented slicers that allow users to dynamically adjust these thresholds
   - The salary threshold slicer defaults to 112 (visible in the dashboard)
   - The happiness threshold slicer defaults to 5

3. **Quadrant Calculation:**
   - Created a calculated field to categorize each data point into one of four quadrants:
     * Q1: High Salary, High Happiness (ideal scenario)
     * Q2: Low Salary, High Happiness (good value)
     * Q3: Low Salary, Low Happiness (concerning)
     * Q4: High Salary, Low Happiness (compensation not translating to satisfaction)

4. **Visual Enhancements:**
   - Used conditional formatting to color-code points based on their quadrant assignment
   - Added quadrant labels for clarity
   - Implemented tooltips that display the quadrant information along with detailed data point information

5. **Analysis Benefits:**
   - This approach enables identification of outliers and patterns
   - Helps discover roles that offer good salary-to-satisfaction ratio
   - Reveals potential areas where compensation structures could be improved
   - Provides a foundation for segmentation analysis by job role, country, or other factors

## Interactive Features

- Work/Life Balance and Salary Happiness gauge visualizations
- Slicers for filtering data by various dimensions
- Interactive quadrant analysis for salary vs. happiness
- Drill-down capabilities for deeper analysis

## Dashboard Components

The dashboard consists of multiple interconnected visualizations that provide a comprehensive view of the data professionals landscape, allowing users to:
- Compare salary variations across roles and countries
- Understand the relationship between salary and satisfaction
- Analyze the perceived barriers to entry in the field
- Explore programming language preferences by job role

## Key Insights Gained from Analysis

1. **Gender Disparity in the Field**
   - Significant imbalance with 468 male respondents (74.3%) versus 162 female respondents (25.7%)
   - Gender distribution varies across job roles and countries

2. **Salary Hierarchy and Job Roles**
   - Data Scientists command the highest average salaries in the field
   - Data Engineers rank second in compensation
   - Entry-level positions (Students/Looking) and Database Developers show the lowest average compensation

3. **Geographic Distribution and Compensation**
   - United States has the highest concentration of data professionals among respondents
   - Salary levels vary significantly by country, with US-based professionals typically earning more

4. **Work Satisfaction Metrics**
   - Average Work/Life Balance satisfaction is moderately positive at 5.74/10
   - Salary satisfaction is lower at 4.27/10, suggesting compensation may not meet expectations
   - Higher salaries don't always correlate with higher satisfaction levels

5. **Barriers to Entry**
   - 42.7% of respondents (269 people) found breaking into data neither easy nor difficult
   - 24.6% (156 people) found it difficult
   - 21.3% (134 people) found it easy
   - Only 7% (44 people) found it very difficult
   - This suggests moderate accessibility to the field with some challenges

6. **Programming Language Preferences**
   - Python dominates as the preferred programming language across all job roles
   - R and Other languages follow as distant second and third choices
   - Clear language specialization patterns emerge across different job roles
   - Language preference tends to align with specific job functions

7. **Age Demographics**
   - The average age of respondents is 30 years
   - This suggests a relatively young professional community

8. **Role Distribution**
   - Data Analysts represent the largest group among respondents
   - Student/Looking cohort represents significant interest in entering the field

9. **Quadrant Analysis Insights**
   - The scatter plot quadrant analysis revealed distinct patterns across job roles:
     * Data Scientists often appear in the "High Salary, High Happiness" quadrant
     * Many Data Analysts fall in the "Low Salary, Low Happiness" quadrant
     * The adjustable thresholds help identify roles that offer exceptional value (high happiness despite moderate salary)
     * Some high-salary positions show surprisingly low satisfaction, suggesting factors beyond compensation affect happiness

These insights provide valuable market intelligence for career planning, hiring strategies, educational curriculum development, and understanding the current state of the data profession landscape and these dashboards can be used by:
- Data professionals seeking industry benchmarks
- HR and recruitment teams analyzing compensation trends
- Career changers researching the data field
- Educational institutions developing data science curricula


