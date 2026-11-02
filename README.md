# Video-Game-Sales
🎮 Video Game Sales Analytics Dashboard (Power BI). I created an interactive Power BI dashboard that analyses 16,000+ video game releases to show which genres, platforms and publishers drive sales, and how tastes differ across North America, Europe, Japan and the rest of the world.


---

## 1.Project Overview

The video game industry is hit-driven and highly regional. A genre that dominates in North America can underperform in Japan, and a handful of blockbusters can account for a large share of total sales. This project turns raw sales data into a decision-support tool for a game company, answering questions such as:

1. Which genres, platforms and publishers generate the most sales, and how has that changed over time?
2. How do regional preferences differ, and where should a title launch first?
3. Which publishers are efficient (high sales per title) rather than just large?
4. How concentrated are sales in a few top-selling games?
5. How long does a platform's sales life last, and when does it peak?

---

## 2.Dataset

- **Source:** [Kaggle: Video Game Sales]([https://www.kaggle.com/](https://www.kaggle.com/datasets/rush4ratio/video-game-sales-with-ratings/data)) 
- **Size:** 16,000+ rows, one row per game per platform
- **Unit:** all sales figures are **millions of copies sold** (units, not revenue)

| Field | Description |
|---|---|
| Name | Game title |
| Platform | Release platform (PC, PS4, Wii, etc.) |
| Year_of_Release | Year the game was released |
| Genre | Game genre |
| Publisher | Publisher of the game |
| Developer | Developer of the game |
| NA_Sales | North America sales (millions) |
| EU_Sales | Europe sales (millions) |
| JP_Sales | Japan sales (millions) |
| Other_Sales | Rest of world sales (millions) |
| Global_Sales | Total worldwide sales (millions) |


## 🧱 Data Model

Built in Power Query and the Power BI model view as a star schema.

```
dimPlatform ──┐
dimGenre ─────┼──► factSales ──► factRegionSales ◄── dimRegion
dimPublisher ─┤     (SalesID)      (SalesID, Region, Sales)
dimDeveloper ─┘
```

- **factSales:** one row per game per platform, with foreign keys to each dimension and a `SalesID` index.
- **dimPlatform / dimGenre / dimPublisher / dimDeveloper:** distinct values with IDs.
- **factRegionSales:** `NA_Sales`, `EU_Sales`, `JP_Sales` and `Other_Sales` unpivoted into `Region | Sales`, so a single region slicer filters every regional visual.
- **dimRegion:** the four regions with a sort order, used for the region slicer.


