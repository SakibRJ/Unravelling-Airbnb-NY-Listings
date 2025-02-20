# Unravelling Airbnb-NY Listings: A Python Based EDA Approach


## Project Description
This project applies Python-based Exploratory Data Analysis (EDA) to examine Airbnb listings in New York, leveraging libraries such as Pandas, Numpy, Seaborn, and Matplotlib. The objective is to uncover key insights into pricing trends, location dynamics, property types, and customer ratings, helping both hosts and stakeholders make informed, data-driven decisions. The analysis includes data cleaning, handling missing values, summary statistics, and correlation analysis, followed by visualizations using histograms, scatter plots, bar charts etc. Additionally, it explores room type distribution, availability patterns, outlier detection, and advanced filtering to refine insights.

By identifying patterns and correlations, this study provides strategic recommendations for location-based targeting, and property management, ultimately enhancing profitability and guest satisfaction. The findings highlight operational trends that can guide hosts in maximizing revenue while ensuring competitive, value-driven accommodations. Future enhancements could incorporate predictive modeling and advanced analytics to deepen market insights, optimize decision-making, and improve Airbnb’s overall competitiveness.



###  Objectives
- Univariate: Examine the key individual variables, such as the distribution of pricing across listings, the frequency of availability, and the count of bedrooms, which can help identify patterns and trends that can provide a clearer understanding of the dataset's characteristics & thereby gaining insights into market trends, demand patterns, and listing characteristics, helping hosts and stakeholders make informed decisions.
- Provide insights into regional pricing patterns and help identify trends in property value across various areas, which is distribution of listings across different neighbourhoods, along with the corresponding mean price.
- Bivariate: Explore the relationships between major attributes and shedd light on potential dependencies and trends within the dataset to uncover key insights into how location, guest feedback, and accommodation type influence pricing patterns.
- Identify the top correlations between different attributes within the dataset, revealing key relationships and valuable insights into how various factors interact and influence each other.
- Any more insights that can add value into the characteristics of this report are welcome.


### Dataset Overview
The dataset consists of 20,765 entries with 22 features, capturing key details about Airbnb listings, including:

- ID & Host Information: Unique listing ID and host name.
- Location Details: Neighborhood group (borough), latitude, and longitude.
- Pricing & Availability: Nightly rental price and the number of available days per year.
- Property Features: Room type (e.g., entire home/apt, private room, hotel room, shared room).
Engagement Metrics: reviews, ratings etc.

Refer to the 'Business_Req_Document_Airbnb.docx' for a detailed breakdown of the dataset.


### Methodology
- Importing all dependencies (lib) #Pandas, Numpy, Seaborn for graphs/charts, matplotlib.pyplot for plotting aspects.
- loading and understanding the dataset.
- Data Cleaning to ensure data consistency for accurate analysis.
- Data Analysis to extract meaningful insights.
- Visualization to enhance interpretability and decision-making.

### Approach
1. ### Data Cleaning
Handle missing data: price, neighborhood, and minimum_nights, room_type columns had null values.
Removal of Duplicated rows: 12 rows were detected and removed.
    
    data.duplicated().sum() #View duplicates
    data.drop_duplicates(inplace=True) ##Deleting duplicated rows

Fix data types: Converted last_review to a datetime object.

    data['last_review']=data['last_review'].astype('datetime64[ns]')

Remove outliers: Listings with prices > $2,000 were capped to avoid skewed visualizations.

BEFORE:

![Image](https://github.com/user-attachments/assets/9334c980-33f2-4918-b41e-91fdcda98b49)


AFTER:

    #Removing outliers and storing the dataset in new df
    df = data[data['price'] < 2000]

![Image](https://github.com/user-attachments/assets/f9bb6bd2-3734-4877-88c2-0418db4cfdc3)

2. ### EDA (Exploratory Data Analysis)
#### Checking the price distribution; Exploration of price across the dataset:

    plt.figure(figsize=(10, 7))
    sns.lineplot(data=df, x='neighbourhood_group', y='price', hue='room_type')
    plt.xlabel('Neighbourhood in NY   fig(a)')
    plt.ylabel('Price ($)')
    plt.title("Price Distribution across Neighbourhood in the dataset")
    plt.show()

![Image](https://github.com/user-attachments/assets/f7db44cb-e58a-40db-9f78-dcb10a8d8a7a)

#The Graph above indicates price distribution across the neighbourhood in newyork for AirBnb listing in the dataset.

#Almost all room-types bags the most expensive spots in 'Manhatta' of which hotel room having the most expensive listings where as 'Bronx' indicating the chepest listings in almost all kinds of room-types.

#### Room type distribution:

Price Distribution of rooms analysed with histogram.
![Image](https://github.com/user-attachments/assets/f49fdb74-d6af-4527-962f-8b5e4045fe3d)
#The data is right skewed where majority of the listing are priced between 0-500 USD

#### Availability distribution
![Image](https://github.com/user-attachments/assets/87762f6a-53b9-4760-8ca7-bfbe691278cf)
#The distribution is bimodal, with major peaks at 0 and 365.The spikes at round numbers (90, 160) could indicate hosts setting availability in structured time blocks.

#### Visualized the count listings per neighborhood using bar plots:

    viz = sns.barplot(data=df, x='neighbourhood_group', y='price', hue='room_type')
    plt.title("Mean price/bed & Dependency on Neighbourhood")
    plt.xlabel("Neighbourhood Group   fig(d)")
    plt.ylabel("Avg Listing price")
    for labels in viz.containers:
        viz.bar_label(labels, fontsize=7, padding=3)
    plt.show()

![Image](https://github.com/user-attachments/assets/e9eaa533-78b6-49ca-99c0-7e45e60ac27c)


#### Neighborhood group insights:

Analyzed price variations by boroughs.
Manhattan had the highest average prices.

#### Availability trends:

Used heatmaps to show correlations among price, availability_365, number_of_reviews, and beds.

#### Price distribution:

Used histograms to show the distribution of prices.
Majority of the listings were priced between $50 - $300.
Host listings:

#### Relationship of Price with Reviews:
![Image](https://github.com/user-attachments/assets/32ed84cc-b1f9-468a-b86a-92671e2769b6)
#The scatter chart "Relationship of Price with Reviews" shows an inverse relationship between price and the number of reviews i.e., higher-priced listings tend to receive fewer reviews. This suggests that expensive properties attract a smaller, more selective group of guests. 

#### Review behavior:

Used pair plots to show relationships between number of reviews, price, and availability.

3. ### Data Visualization
Pairplot: To see correlations among price, availability, and number of reviews.
Heatmap: Showing correlations among numerical features.
Histograms and Boxplots: To detect outliers in price.
Bar Charts: Displaying room types and neighborhood group distributions.
Key Findings and Insights

Price Trends:
Manhattan has the most expensive listings, followed by Brooklyn.
Entire homes/apartments cost significantly more than private or shared rooms.

Room Type Distribution:
Entire homes/apartments are the most common, but private rooms offer budget-friendly options.

Outliers in Price:
Few listings priced at $10,000+ were detected, indicating the need to filter such extreme values.

Availability Patterns:
Listings with high availability tend to have lower prices and more reviews, likely due to better guest experience.


### Conclusion/Insights:

#### The insights derived align with the business objectives, along with additional findings. For a comprehensive analysis and deeper understanding of the outcomes, please run 'MAIN_Airbnb_data_Analysis.ipynb'. This README serves only as a high-level overview of the project.

- Price distribution across NYC shows that Manhattan has the most expensive Airbnb listings across all room types, while the Bronx offers the cheapest options.

- A significant number of listings are available for 350+ days, followed by those available for 0-20 days. The distribution is bimodal, with peaks at `0 and 365`, while spikes at `90 and 160` days suggest structured hosting availability.

- Manhattan has the highest mean listing price per bed at `$140`, followed by Brooklyn at `$100` and Queens at `$77`.

- Hotel listings are the most expensive in Manhattan, while shared and private rooms listings are more affordable. Bronx has the lowest-cost private rooms listings, followed by Queens, while Staten Island offers the cheapest apartment/home listings.

- The scatter plot shows an inverse relationship between price and reviews—higher-priced listings receive fewer reviews, suggesting they attract a smaller, selective audience. Listings priced between `$1-$750` have the most reviews, reflecting higher booking frequency.

- Entire homes/apartments have the highest review count at `11,483`, followed by private rooms with `8,766`. Manhattan leads in total reviews due to high footfall, followed by Brooklyn.

- The majority of NYC Airbnb listings are Entire Homes/Apartments and Private Rooms, while Shared Rooms are scarce. Airbnb could boost shared room and hotel listings through incentives, while hosts can capitalize on this market gap.

- Price and bed count show a strong positive correlation, with prices increasing as bed count rises. Price has a weak negative correlation with minimum nights and a slight positive correlation with availability_365, suggesting higher-priced listings have lower demand but more availability.
