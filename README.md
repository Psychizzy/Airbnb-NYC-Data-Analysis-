# Airbnb-NYC-Data-Analysis-
This project provides an in-depth analysis of the Airbnb market in New York City (NYC), examining pricing trends, host performance, availability, guest engagement, and revenue insights. The goal is to identify key patterns, detect anomalies, and provide data-driven recommendations for both Airbnb hosts and business strategists.
# Tools
Power BI, DAX, Excel, Python (for preprocessing)

# Objectives:
✅ Understand market trends across different boroughs and neighborhoods.
✅ Analyze pricing distribution and identify key factors influencing price variations.
✅ Evaluate host performance based on revenue, availability, and superhost status.
✅ Detect anomalies & outliers that impact data accuracy and decision-making.
✅ Provide business recommendations for Airbnb hosts and stakeholders.

📂 Dataset Overview
📌 Dataset Name: Airbnb_NYC_2019
📌 Source: Inside Airbnb (Public Dataset)
📌 Total Rows: 38,843
📌 Total Columns: 16

🔑 Key Columns:
id → Unique listing ID
name → Name of the Airbnb listing
host_id → Unique ID of the host
neighbourhood_group → Borough (Manhattan, Brooklyn, etc.)
neighbourhood → Specific area within the borough
room_type → Entire home/apartment, private room, shared room
price → Listing price per night
minimum_nights → Minimum nights required for booking
number_of_reviews → Number of guest reviews
availability_365 → Number of available days per year

# Data Cleaning & Processing
1️⃣ Handling Missing Data & Errors
* Listings with missing prices or 0 prices were excluded from pricing analysis.
* host_name and name column errors were replaced with "Unknown" where necessary.
* last_review was converted to a proper date format.

2️⃣ Identifying & Flagging Outliers
🔹 Price Outliers: Listings with prices above $1,000/night were flagged.
🔹 Minimum Nights Outliers: Listings with minimum_nights > 365 were flagged.

# Created New Calculated Columns
✅ Adjusted Minimum Nights:
Adjusted Minimum Nights =  
IF(AirBnb_NYC_2019[minimum_nights] > 365, 365, AirBnb_NYC_2019[minimum_nights])

✅ Average Price per Night:
Avg Price per Night =  
VAR AdjustedNights = ADDCOLUMNS(
    AirBnb_NYC_2019, "Adjusted Nights", 
    IF(AirBnb_NYC_2019[minimum_nights] > 365, 365, AirBnb_NYC_2019[minimum_nights])
)
RETURN
DIVIDE(
    SUMX(AdjustedNights, AirBnb_NYC_2019[price] * [Adjusted Nights]),
    SUMX(AdjustedNights, [Adjusted Nights]), 0
)

✅ Availability Category:
Availability Category =  
VAR DaysAvailable = MAX('AirBnb_NYC_2019'[availability_365]) 
RETURN
SWITCH(TRUE(),
     DaysAvailable = 0, "Not Available",
     DaysAvailable < 90, "Low Availability",
     DaysAvailable >= 90 && DaysAvailable < 180, "Medium Availability",
     DaysAvailable >= 180, "High Availability"
)  
✅ Superhost Identification: Based on availability & listing count.

# Dashboard Breakdown & Visualizations
📌 The dashboard is structured into 3 pages, each telling a unique story about Airbnb NYC.

📌 Page 1: General Overview
🔹 Objective: Provides a high-level summary of listings, pricing, and availability.
🔹 Key Visuals:
✔️ Top 5 Neighbourhoods by Total Listings (Williamsburg leads)
✔️ Average Price by Borough (Hell’s Kitchen & Williamsburg highest)
✔️ Availability of Listings (Donut Chart)
✔️ Price Distribution Histogram
✔️ Total Listings by Room Type (Pie Chart)
✔️ Listings Density by Borough (Map)

📌 Page 2: Market Insights & Pricing
🔹 Objective: Explores price distribution, availability, and review impact.
🔹 Key Visuals:
✔️ Price Distribution by Neighbourhood Group (Manhattan leads)
✔️ Total Listings vs. Availability Category
✔️ Reviews Impact on Pricing
✔️ Average Price by Room Type
✔️ Price Variation Over Time (Line Chart)
✔️ Listing Distribution Map

📌 Page 3: Host & Business Performance Insights
🔹 Objective: Examines host revenue, listing activity, and business performance.
🔹 Key Visuals:
✔️ Top 5 Hosts by Total Revenue (Michael & David lead)
✔️ Average Availability by Room Type
✔️ Booking Availability by Host Activity
✔️ Top 5 Hosts by Listings
✔️ Superhosts vs. Regular Hosts
✔️ Revenue Distribution Histogram

# Key Findings & Business Recommendations
🏙️ Market & Pricing Trends
✅ Williamsburg & Hell’s Kitchen have highest Airbnb activity.
✅ Bronx & Staten Island are more budget-friendly alternatives.

💰 Host Performance & Revenue
✅ Few hosts dominate most revenue, earning over $40K+ annually.
✅ Superhosts have higher occupancy & revenue but are only 7.7% of total hosts.
✅ Many hosts underprice listings, leading to lost revenue.

🏠 Availability & Booking Insights
✅ Over 50% of listings are not available year-round.
✅ Shared rooms have higher availability but lower demand.
✅ More reviews correlate with higher bookings.

📊 Outliers & Market Anomalies
✅ $10,000/night listings exist but are extreme outliers.
✅ Some hosts list properties with unrealistic availability.
✅ Many listings have underpriced rates, reducing potential revenue.

# Business Recommendations
✔️ Optimize pricing based on market trends.
✔️ Increase availability to maximize earnings.
✔️ Encourage guests to leave reviews for better visibility.
✔️ Detect pricing anomalies & flag unrealistic listings.
✔️ Promote underutilized boroughs like Bronx & Staten Island.
✔️ Educate hosts on pricing & availability strategies.

# Interactive Features & Enhancements
✅ Filters & Slicers:
Neighborhood
Room Type
Price Outliers (Filtered Out)

✅ Custom Bookmarks & Navigation:
Airbnb Logo as a clickable bookmark to see Brooklyn Analysis alone.

✅ Final Design & Aesthetics:
✔️ Professional color scheme & layout.
✔️ Consistent fonts & clear storytelling.
✔️ Airbnb branding for a polished look.

