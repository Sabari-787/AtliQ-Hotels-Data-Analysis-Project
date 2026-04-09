# 🏨 AtliQ Hotels Data Analysis Project (End-to-End Data Analytics)

![Python](https://img.shields.io/badge/Python-3.x-blue?logo=python)
![Pandas](https://img.shields.io/badge/Library-Pandas-yellow)
![Matplotlib](https://img.shields.io/badge/Visualization-Matplotlib-green)
![Status](https://img.shields.io/badge/Status-Completed-success)

---

## 📌 Project Overview

This is an **end-to-end data analysis project** on hotel booking data.

The objective is to:
- 📊 Analyze hotel performance
- 🧹 Clean real-world data
- 📈 Generate business insights
- 📉 Visualize key metrics

---

## 🧩 Problem Statement

A hotel chain wants to:
- Understand booking trends  
- Analyze revenue performance  
- Identify occupancy patterns  
- Improve business decisions  

---

## 📂 Datasets Used

- `fact_bookings.csv`
- `fact_aggregated_bookings.csv`
- `dim_hotels.csv`
- `dim_rooms.csv`
- `dim_date.csv`

---

# 🔹 1. Data Exploration

```python
import pandas as pd

df_bookings = pd.read_csv('datasets/fact_bookings.csv')

print(df_bookings.shape)
print(df_bookings.head())
```

### 📊 Booking Platform Distribution

```python
df_bookings.booking_platform.value_counts().plot(kind="bar")
```

---

# 🔹 2. Data Cleaning

## ✅ Remove Invalid Guests

```python
df_bookings = df_bookings[df_bookings.no_guests > 0]
```

---

## ✅ Remove Revenue Outliers

```python
avg = df_bookings.revenue_generated.mean()
std = df_bookings.revenue_generated.std()

upper_limit = avg + 3 * std

df_bookings = df_bookings[df_bookings.revenue_generated <= upper_limit]
```

---

## ✅ Handle Missing Values

```python
df_agg_book = pd.read_csv('datasets/fact_aggregated_bookings.csv')

cap_mean = round(
    df_agg_book[df_agg_book['room_category'] == 'RT1']['capacity'].mean()
)

df_agg_book.fillna({'capacity': cap_mean}, inplace=True)
```

---

# 🔹 3. Data Transformation

## ✅ Create Occupancy %

```python
df_agg_book['occ_pct'] = (
    df_agg_book['successful_bookings'] / df_agg_book['capacity']
) * 100
```

---

# 🔹 4. Data Analysis & Insights

---

## 📊 1. Average Occupancy by Room Type

```python
df.groupby("room_class")["occ_pct"].mean()
```

---

## 📊 2. Average Occupancy by City

```python
df.groupby("city")["occ_pct"].mean()
```

---

## 📊 3. Weekday vs Weekend Occupancy

```python
df.groupby("day_type")["occ_pct"].mean()
```

---

## 📊 4. June Month Occupancy

```python
df_june = df[df["mmm yy"] == "Jun 22"]

df_june.groupby("city")["occ_pct"].mean().plot(kind="bar")
```

---

## 📊 5. Revenue by City

```python
df_bookings_all.groupby("city")["revenue_realized"].sum()
```

---

## 📊 6. Monthly Revenue

```python
df_bookings_all.groupby("mmm yy")["revenue_realized"].sum()
```

---

## 📊 7. Revenue by Hotel

```python
df_bookings_all.groupby('property_name')['revenue_realized'].sum().sort_values(ascending=False)
```

---

## 📊 8. Average Rating per City

```python
df_bookings_all.groupby('city')['ratings_given'].mean().round(1)
```

---

## 📊 9. Revenue Share by Booking Platform (Pie Chart)

```python
import matplotlib.pyplot as plt

df_bookings_all.groupby('booking_platform')['revenue_realized'].sum().plot(
    kind='pie',
    figsize=(8,8),
    autopct='%1.1f%%',
    shadow=True
)

plt.show()
```

---

# 📈 Key Insights

- 🏆 **Weekend occupancy is higher than weekdays**
- 🏙️ **Delhi has highest occupancy rate**
- 💰 **Mumbai generates highest revenue**
- 🏨 **Luxury rooms (RT4) have higher revenue**
- 📊 **Booking platforms contribute differently to revenue**

---

# 📁 Project Structure

```
atliq-hotels-analysis/
│── datasets/
│   ├── fact_bookings.csv
│   ├── dim_hotels.csv
│   ├── dim_rooms.csv
│   ├── dim_date.csv
│── main.py
│── README.md
```

---

# 🚀 How to Run

```bash
python main.py
```

---

# 💡 Future Improvements

- 📊 Build Power BI Dashboard  
- 🌐 Create Streamlit Web App  
- 🤖 Add ML model for revenue prediction  
- 📈 Advanced visualizations  

---

# 📈 Resume Value

> Performed end-to-end hotel data analysis using Python and Pandas, including data cleaning, transformation, and visualization to generate actionable business insights.

---

# ⭐ If you like this project

Give it a ⭐ and keep building 🚀
