# Googleplaystoredata
Google Play Store Apps Analysis: An end-to-end Python data science project exploring 10,000+ apps to identify market trends. Features data cleaning, sentiment analysis, and visualization of correlations between ratings, installs, pricing, and app categories to drive mobile product strategy.
Mean Rating: Calculates the average value of the Rating column.
Unique Categories: Identifies and lists all distinct app categories available in the dataset.
Frequency Counts: Counts occurrences of each value in the Type column (e.g., Free vs. Paid).
Mode Identification: Determines the most frequent value in the Content Rating column
Size Normalization: Converts app sizes from string formats (like 'M' for megabytes and 'k' for kilobytes) into numeric byte values for mathematical analysis.
Install Count Cleaning: Transforms the Installs column by removing "+" and "," characters to convert them into integers.
Review Formatting: Converts Reviews data into numeric format, including handling "M" (million) suffixes.
Anomaly Detection: Specifically filters for rows where the Category is '1.9' to investigate data entry errors or outliers.
Performance Filtering: Creates a subset of the data containing only apps with a Rating of 4.0 or higher.
Top Performers: Sorts the dataset to identify the top 5 apps based on the number of installs
App Size Distribution: Includes code to generate a histogram showing the distribution of app sizes across the store.
Grouped Means: Calculates the mean number of reviews categorized by the app Type (Free vs. Paid).
