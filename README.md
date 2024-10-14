# UFO Sightings Analysis - Power BI Project

🛸 **UFO Sightings Analysis**: This project focuses on analyzing reported UFO sightings from various regions, years, and environmental conditions. Using Power BI, this analysis provides key insights into the trends of UFO sightings and helps uncover potential patterns based on geography, time, and weather conditions.

🔍 **Explore interactive visuals, advanced DAX measures, and data transformation techniques** to understand how different variables, such as location, weather, and year, influence UFO sightings data.

# Background

The **UFO Sightings Analysis** was created to explore trends in UFO sighting data. This project aims to identify regions with frequent sightings, seasonal trends, and analyze environmental conditions that correlate with sightings. The Power BI dashboard delivers a comprehensive view of how UFO sightings have been reported across time and space, providing insight into this mysterious phenomenon.

### Key Questions Addressed:
1. **Which regions report the most UFO sightings?**
2. **What time of year and day are UFO sightings most commonly reported?**
3. **Are there any environmental or geographic factors that correlate with UFO sightings?**
4. **How have the number of sightings changed over time?**
5. **Which regions have seen the most growth in sightings over recent years?**

# Tools and Techniques I Used

For this analysis, I leveraged the following tools and techniques:
- **Power BI**: The primary tool used for creating dynamic and interactive visualizations, making it easy to explore the UFO sightings data.
- **Advanced DAX (Data Analysis Expressions)**: Implemented for calculating trends, year-over-year growth, and identifying high-sighting regions.
- **Data Cleaning and Transformation**: Power Query was used to clean and reshape the data for analysis.
- **Conditional Formatting**: Applied to highlight high-sighting periods and regions in visuals for quick insights.
- **Advanced Power BI Features**: Drillthrough, custom tooltips, and report page tooltips were utilized to provide users with detailed contextual insights.

# The Dashboard

### Key Visuals and Insights:

1. **Sightings Over Time**:
   - The **line chart** visualizes the number of UFO sightings over time, revealing trends and potential spikes in specific years. This allows for analysis of periods where sightings dramatically increased or decreased.

2. **Geographical Distribution of Sightings**:
   - The **map visual** pinpoints the geographical location of UFO sightings, highlighting hotspots in the data. Users can drill down into specific regions to uncover where the most sightings have occurred, such as the **United States**, which historically reports the most UFO sightings.

3. **Sightings by Month**:
   - This **bar chart** displays sightings broken down by month, revealing potential seasonal trends. Users can spot which months see higher numbers of reports (e.g., increased sightings during summer months).

4. **Environmental and Time-based Analysis**:
   - A visual exploring the correlation between **weather conditions** (e.g., cloudy, clear) and sightings. It provides insights into whether environmental conditions play a role in the frequency of sightings.
   - Additionally, there’s an analysis of **time of day**, examining whether certain times (e.g., night vs. day) have a higher concentration of sightings.

5. **Top States for UFO Sightings**:
   - A **bar chart** lists the top states or regions for UFO sightings, showcasing the most active areas in terms of sighting reports.

# The Analysis

### 1. Geographical Hotspots for Sightings

By mapping the sightings, users can easily identify **geographical hotspots** for UFO sightings, particularly across regions like the **United States** and **Canada**. This visual is key for understanding where UFO activity is most concentrated.

**DAX for Sightings Count by Region**:
```dax
Sightings Count by Region = 
CALCULATE(
    COUNT('Sightings'[SightingID]),
    'Sightings'[Country] = "United States"
)
```

This DAX formula calculates the number of sightings in a specific country or region, providing a clear view of hotspots for sightings.

### 2. Temporal Analysis of Sightings

Tracking sightings over time, I used line and bar charts to help visualize how sightings fluctuate over months and years. This insight allows researchers to investigate potential reasons behind spikes in reports.

**DAX for Year-over-Year Sightings Growth**:
```dax
YoY Sightings Growth = 
DIVIDE(
    [Total Sightings] - CALCULATE([Total Sightings], PREVIOUSYEAR('Date'[Year])),
    CALCULATE([Total Sightings], PREVIOUSYEAR('Date'[Year]))
)
```

This DAX measure calculates the **year-over-year growth** in sightings, highlighting trends in how UFO sighting reports have changed over time.

### 3. Seasonal and Time of Day Trends

I explored the UFO sighting data by **month** and **time of day** to identify patterns. Seasonal fluctuations could suggest external factors influencing reports (e.g., more outdoor activity in summer).

**DAX for Sightings by Month**:
```dax
Sightings by Month = 
CALCULATE(
    COUNT('Sightings'[SightingID]),
    MONTH('Sightings'[Date]) = MONTH(TODAY())
)
```

This DAX function calculates the number of sightings for each month, allowing us to determine which months see the most reports.

### 4. Environmental Analysis

An essential part of this analysis was to investigate whether certain **weather conditions** or **time of day** correlate with increased UFO sightings. By visualizing data across variables like **weather patterns** and **cloud coverage**, we can speculate on possible environmental influences on sightings.

**DAX for Sightings by Weather Condition**:
```dax
Sightings by Weather = 
CALCULATE(
    COUNT('Sightings'[SightingID]),
    'Sightings'[Weather] = "Clear"
)
```

This formula calculates sightings that occur during **clear weather conditions**, helping identify potential environmental correlations.

# Advanced SQL Query for UFO Sightings Analysis

In addition to using DAX measures in Power BI, SQL was used for data cleaning and aggregation before importing the data into Power BI. Here's an advanced SQL query used to calculate sightings based on environmental and geographical factors:

```sql
WITH WeatherImpact AS (
    SELECT 
        State,
        COUNT(SightingID) AS TotalSightings,
        AVG(CASE WHEN Weather = 'Clear' THEN 1 ELSE 0 END) AS ClearWeatherRatio,
        AVG(CASE WHEN TimeOfDay = 'Night' THEN 1 ELSE 0 END) AS NightTimeSightingsRatio
    FROM 
        dbo.UFOSightings
    GROUP BY 
        State
)

SELECT 
    State,
    TotalSightings,
    ClearWeatherRatio,
    NightTimeSightingsRatio
FROM 
    WeatherImpact
ORDER BY 
    TotalSightings DESC;
```

This query provides insights into how different environmental factors (e.g., weather conditions or time of day) affect the likelihood of UFO sightings in specific states.

# Key Insights

1. **Geographical Hotspots**: The analysis revealed that the **United States** remains the leader in UFO sightings, with certain states like **California** reporting the highest number of cases.
   
2. **Seasonal and Monthly Trends**: The data suggests that UFO sightings are more frequent during the **summer months**, potentially due to increased outdoor activity.
   
3. **Environmental Correlations**: Clear weather conditions and nighttime sightings showed a notable increase in UFO reports, providing insight into the potential impact of environmental factors on sighting reports.

# What I Learned

🧩 **Advanced DAX for Temporal and Geographical Analysis**: This project allowed me to dive deep into advanced DAX calculations for analyzing **time-based trends** and **geographical hotspots**, providing significant insights into when and where sightings occur.

📊 **SQL for Data Aggregation**: Using SQL, I was able to clean and aggregate data based on multiple factors, ensuring that the dataset was ready for insightful visualizations in Power BI.

💡 **Environmental Impact on Sightings**: Through this project, I learned how to correlate environmental factors, such as weather and time of day, with increases in UFO sighting reports.

# Conclusions

### Key Takeaways:
- **Regional UFO Hotspots**: The United States, especially states like California and Texas, continues to dominate the number of UFO sightings reported.
- **Time of Year and Day Impact**: UFO sightings are more frequent during summer months and at night, suggesting external factors influencing reports.
- **Environmental Influence**: Clear weather conditions correlate with higher UFO sighting reports, offering an interesting dimension to the analysis.
