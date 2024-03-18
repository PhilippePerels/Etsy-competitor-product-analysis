# Etsy-competitor-product-analysis
Analysing Etsy competitor's products to drive business growth through data driven insights

### Project Overview
1. Download data on competitor product in my niche, gathered with Everbee (Etsy analytics tool).
2. Use Python (pandas, matplotlib and seaborn) for data exploration, assessment, and manipulation.

### Tools 
- Jupyther Notebook
- Excel

### Data exploration
```python
# Look at first few rows
data.head()
```
```python
# Understand data structure
data.info()
```
```python
# Understand exactly how many values are missing from each feature
data.isnull().sum()
```
```python
# Basic statistics on data
data.describe()
```
```python
# Correlation between features, helps understand which variables moves together
correlation_matrix = data.corr()
plt.figure(figsize=(10, 8))
sns.heatmap(correlation_matrix, annot=True)
plt.title('Correlation Matrix')
plt.show()
```
![Capture d'écran 2024-03-18 152638](https://github.com/PhilippePerels/Etsy-competitor-product-analysis/assets/118985006/7df1a45c-6774-4474-a584-39e1a8f76398)
```python
# Sort the shops by mean revenue in descending order
shop_stats = data.groupby('Shop Name')['Est. Monthly Revenue'].agg(['count', 'mean'])
shop_stats = shop_stats.sort_values(by='mean', ascending=False)
# Plot the bar chart
plt.figure(figsize=(10, 6))
plt.bar(shop_stats.index, shop_stats['mean'])
plt.xticks(rotation=90)
plt.xlabel('Shop Name')
plt.ylabel('Mean Est. Monthly Revenue')
plt.title('Mean Est. Monthly Revenue by Shop')
plt.show()
```
![Capture d'écran 2024-03-18 152751](https://github.com/PhilippePerels/Etsy-competitor-product-analysis/assets/118985006/bd51f09e-3985-4840-9a1a-7886b3f60a0d)
```python
# boxplot to see relationship between product title character count and estimated monthly revenue
data['Title Character Count'] = data['Product Name'].apply(len)
sns.boxplot(x='Title Character Count', y='Est. Monthly Revenue', data=data)
plt.xticks(rotation=90)
plt.title('Title Character Count vs. Monthly Revenue')
plt.show()
```
![Capture d'écran 2024-03-18 161140](https://github.com/PhilippePerels/Etsy-competitor-product-analysis/assets/118985006/f9bb0297-9f9a-4be8-a17f-60d24541fe7c)
```python
# Scatter plot to visualize the relationship between listing age and estimated monthly revenue
plt.scatter(data['Listing Age'], data['Est. Monthly Revenue'])
plt.xlabel('Listing Age (Months)')
plt.ylabel('Est. Monthly Revenue')
plt.title('Listing Age vs. Monthly Revenue')
plt.show()
```
```python
# Scatter plot to visualize the relationship between the number of tags used and monthly revenue
plt.scatter(data['Tags Used'], data['Est. Monthly Revenue'])
plt.xlabel('Number of Tags Used')
plt.ylabel('Est. Monthly Revenue')
plt.title('Number of Tags Used vs. Monthly Revenue')
plt.show()
```
```python
# Histogram of prices for high-revenue listings
plt.hist(data[data['Est. Monthly Revenue'] > 500]['Price'], bins=10)
plt.xlabel('Price')
plt.ylabel('Frequency')
plt.title('Price Distribution for High-Revenue Listings')
plt.show()
```
![Capture d'écran 2024-03-18 161301](https://github.com/PhilippePerels/Etsy-competitor-product-analysis/assets/118985006/010a2261-1000-44f0-a379-fc525835a1de)
```python
# Create a list of all tag columns (Tag 1 to Tag 13)
tag_columns = ['Tag 1', 'Tag 2', 'Tag 3', 'Tag 4', 'Tag 5', 'Tag 6', 'Tag 7', 'Tag 8', 'Tag 9', 'Tag 10', 'Tag 11', 'Tag 12', 'Tag 13']

# Create an empty dictionary to store tag frequencies
tag_frequencies = {}

# Calculate tag frequencies
for col in tag_columns:
    tags = data[col].str.strip()  # Remove leading/trailing whitespaces
    for tag in tags:
        if tag not in tag_frequencies:
            tag_frequencies[tag] = 1
        else:
            tag_frequencies[tag] += 1

# Sort the dictionary by frequency in descending order
sorted_tag_frequencies = {k: v for k, v in sorted(tag_frequencies.items(), key=lambda item: item[1], reverse=True)}

# Show the top N most frequently used tags
N = 10
top_tags = list(sorted_tag_frequencies.keys())[:N]
```
```python
# Convert tags to string type
top_tags = [str(tag) for tag in top_tags]

# Ensure 'tag_frequencies' is of numeric type (float)
tag_frequencies = [float(frequency) for frequency in tag_frequencies]

#plot top 10 most frequently used tags

plt.bar(top_tags, tag_frequencies)
plt.xlabel('Tags')
plt.ylabel('Frequency')
plt.title(f'Top {N} Most Frequently Used Tags')
plt.xticks(rotation=45)
plt.show()
```
```python
# Create a DataFrame with tag data (replace 'data' with your DataFrame)
tag_data = data[['Tag 1', 'Tag 2', 'Tag 3']]  # Include all tag columns you want to analyze

# Replace missing values (NaN) with an empty string
tag_data = tag_data.fillna('')

# Calculate the length of each tag (e.g., number of words)
tag_data['Tag Length'] = tag_data.apply(lambda row: sum(len(tag.split()) for tag in row), axis=1)

# Create a scatter plot to analyze the relationship
plt.scatter(tag_data['Tag Length'], data['Est. Monthly Revenue'], alpha=0.5)
plt.xlabel('Tag Length')
plt.ylabel('Est. Monthly Revenue')
plt.title('Tag Length vs. Monthly Revenue')
plt.show()
```
![Capture d'écran 2024-03-18 161406](https://github.com/PhilippePerels/Etsy-competitor-product-analysis/assets/118985006/dfb81bf9-6e10-4722-b5c8-aad96d74f040)

### Recommandations
1. Use at least 139 title characters for your products on Etsy.
2. Regularly post new product on your shop.
3. Use all 13 tags available.
