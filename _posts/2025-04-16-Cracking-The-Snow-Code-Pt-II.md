---
layout: post
title:  "Cracking the Snow Code Pt. II"
description: A deeper dive into snowfall patterns with fresh EDA and an interactive app to explore the storm behind the stats.
image: /assets/img/skislash.png
---

# Cracking the Snow Code Pt. II: The Chill Gets Real

## The Research Question:

Snowstorms in Utah’s mountains might feel random—but is there a method behind the mayhem? This project set out to answer a clear and compelling data science question:

💡 **If given the weather information today, can we predict the amount of snow Alta will receive in 3 days?**

To explore this, I gathered daily weather and snowfall data from December 2023 through February 2025 at Alta Ski Resort and used exploratory data analysis (EDA) to look for patterns. I was hoping to discover clear relationships between daily weather variables and snowfall in the near future. Click [here](https://braydenhumpherys.github.io/Data-Grill-Blog/blog/Cracking-The-Snow-Code/) read part 1 of this project, where I go over the detail of how I gathered the data. You can also visit my github repository to review my scraping code [here](https://github.com/BraydenHumpherys/Snowfall-Prediction).

## 1 Key Finding: February Brings the Most Snow

One of the most reliable takeaways was seasonal. By grouping snowfall totals by month-year and visualizing them in a bar chart, a consistent pattern appeared:

**February had the highest total snowfall across both the 2023–24 and 2024–25 seasons.**

This isn’t groundbreaking meteorology, nor does it really answer our data science question, but it’s a good reminder that February remains a prime month for fresh powder at Alta. December and January also show high totals, while March tends to taper off. ![Snowfall by month]({{site.url}}/{{site.baseurl}}/assets/img/total_snowfall_by_month.png)

## Explore the Data Yourself

To make these insights interactive and accessible, I built a simple [Streamlit app](https://crack-the-snow-code.streamlit.app/) that lets users explore snowfall and weather trends season by season.

### App Features

**Tab 1 – Snowfall by Month-Year**

Select from the “23–24” or “24–25” snow season and view total snowfall broken down by month. This makes it easy to compare snowfall across seasons.

#### **Tab 2 – Weather Time Series**

Choose from four weather variables and visualize their trends throughout the season. This helps users explore how conditions shifted over time.

#### **Tab 3 – Scatter Plots & Correlations**

Explore whether any weather variables show a relationship to snowfall 3 days later. Spoiler: they don’t, but it’s still valuable to visualize that directly.

## Challenges & Next Steps: The Snow Code Isn’t Cracked (Yet)

While this project revealed that February is the snowiest month, it also showed that no single weather variable reliably predicts snowfall three days in advance. Even temperature, which initially looked promising, didn’t hold up under closer inspection—likely due to unit inconsistencies I’m still investigating (I can't figure out why the units for temperature are so whack).

![Cracked Ice](%7B%7Bsite.url%7D%7D/%7B%7Bsite.baseurl%7D%7D/assets/img/total_snowfall_by_month.png)

These findings highlight a key takeaway: simple correlations aren’t enough. Predicting snowfall will likely require more features and machine learning models that can capture complex and nonlinear relationships. A Random Forest is my next step, where I’ll explore feature importance and hopefully find more exciting conclusions.

Though we haven’t cracked the snow code yet, the foundation is here, and the data exploration continues.

[Streamlit-App Github Repo](https://github.com/BraydenHumpherys/SnowFall-App)
