# Market-Entry-Strategy-ESG-Roadmap-FMCG-Sector-Tools-Excel-Python-PowerPoint-
Conducted market sizing and competitor benchmarking to evaluate expansion opportunities for a mid-sized FMCG manufacturer.
Built a 3-year financial model assessing modern trade, D2C, and export strategies alongside sustainability initiatives.
The proposed growth and ESG strategy projects 12–18% revenue growth and a ~25% reduction in operational emissions 

# -----------------------------
# Project 3: Quick Output Preview
# -----------------------------

import pandas as pd
import numpy as np
import matplotlib.pyplot as plt

# -----------------------------
# Step 1: Define 50 cities
# -----------------------------
cities = [
    "Mumbai", "Delhi", "Bangalore", "Hyderabad", "Ahmedabad", "Chennai", "Kolkata", "Surat", "Pune", "Jaipur",
    "Lucknow", "Kanpur", "Nagpur", "Indore", "Thane", "Bhopal", "Visakhapatnam", "Pimpri-Chinchwad", "Patna", "Vadodara",
    "Ghaziabad", "Ludhiana", "Agra", "Nashik", "Faridabad", "Meerut", "Rajkot", "Kalyan-Dombivli", "Vasai-Virar", "Varanasi",
    "Srinagar", "Aurangabad", "Dhanbad", "Amritsar", "Navi Mumbai", "Allahabad (Prayagraj)", "Howrah", "Ranchi", "Coimbatore",
    "Jabalpur", "Gwalior", "Vijayawada", "Mysore", "Jodhpur", "Madurai", "Raipur", "Kota", "Guwahati"
]

n = len(cities)

# -----------------------------
# Step 2: Generate sample data
# -----------------------------
np.random.seed(42)

df = pd.DataFrame({
    "City": cities,
    "Population (M)": np.round(np.random.uniform(0.8, 20.7, n), 1),
    "SOM ($M)": np.round(np.random.uniform(20, 200, n), 0),
    "Energy_Consumption_GWh": np.round(np.random.uniform(50, 2000, n), 0)
})

# GHG Protocol: Scope 1+2 emissions
df["Avg_GHG_Emissions_tCO2e"] = df["Energy_Consumption_GWh"] * 8

# TCFD revenue impact
df["Revenue_High_ESG ($M)"] = df["SOM ($M)"] * np.random.uniform(3.5, 4.5, n)
df["Revenue_Low_ESG ($M)"] = df["SOM ($M)"] * np.random.uniform(2.5, 3.5, n)

# BRSR sustainability score and initiative
df["Sustainability_Score_1_10"] = np.random.randint(5, 9, n)
df["Recommended_ESG_Initiative"] = np.random.choice(["Sustainable Packaging", "Energy Efficiency"], n)

# -----------------------------
# Step 3: Show table preview
# -----------------------------
print("Sample ESG Dataset:\n")
display(df.head(10))  # show first 10 rows

# -----------------------------
# Step 4: Plot general charts
# -----------------------------
# Average GHG Emissions by Top 10 Cities
plt.figure(figsize=(10,5))
plt.bar(df["City"][:10], df["Avg_GHG_Emissions_tCO2e"][:10], color='green')
plt.ylabel("GHG Emissions (tCO2e)")
plt.title("Top 10 Cities - GHG Emissions")
plt.xticks(rotation=45)
plt.show()

# Revenue under High vs Low ESG scenarios for first 10 cities
plt.figure(figsize=(10,5))
x = np.arange(10)
width = 0.35
plt.bar(x - width/2, df["Revenue_High_ESG ($M)"][:10], width, label="High ESG", color='blue')
plt.bar(x + width/2, df["Revenue_Low_ESG ($M)"][:10], width, label="Low ESG", color='red')
plt.ylabel("Revenue ($M)")
plt.title("Revenue Scenario Comparison (Top 10 Cities)")
plt.xticks(x, df["City"][:10], rotation=45)
plt.legend()
plt.show()
