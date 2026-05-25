# ⚽ Premier League Analytics Dashboard — Power BI

> Power BI · Power Query · DAX · Data Modelling · Kaggle Dataset

An end-to-end Business Intelligence project built in Power BI, analysing **32 seasons of Premier League match data (1993–2025)** sourced from Kaggle. The dashboard surfaces performance trends, discipline patterns, and match-level insights across teams and eras — delivered as a 4-page interactive report designed for football analysts, sports strategists, and data enthusiasts.

---

## 🎯 Project Objectives

**Goal 1** — Clean and transform raw match data across 3 CSV files using Power Query, building a reliable and analysis-ready data model.

**Goal 2** — Design a star-schema data model with proper table relationships to support cross-filtering and drill-through navigation.

**Goal 3** — Develop DAX measures for key football metrics including points, win rates, goal differences, clean sheets, and disciplinary statistics.

**Goal 4** — Build a 4-page interactive Power BI dashboard covering League Overview, Team Performance, Discipline Analysis, and Match Insights.

**Goal 5** — Extract 3–5 actionable business insights from the data to communicate findings to non-technical stakeholders.

---

## 📂 Dataset

| File | Description |
|------|-------------|
| `matches.csv` | Match-level results: teams, scores, referee, venue |
| `teams.csv` | Club metadata: team names, short codes |
| `seasons.csv` | Season-level context: year, division, matchweek |

- **Source:** Kaggle — Premier League Match Data (1993–2025)
- **Coverage:** 32 seasons · 12,000+ matches · 50+ clubs
- **Format:** 3 CSV files loaded via Power Query

---

## 🛠️ Tech Stack

| Tool | Purpose |
|------|---------|
| Power BI Desktop | Dashboard development and report design |
| Power Query (M Language) | Data ingestion, cleaning, and transformation |
| DAX | Calculated columns, measures, and KPIs |
| Data Modelling | Star schema with fact and dimension tables |
| Kaggle | Public dataset source |

---

## 🗂️ Dashboard Pages

### Page 1 — League Overview
A high-level season summary showing total matches played, goals scored, average goals per game, and top-performing teams per season. Includes a season slicer for year-on-year comparison.

### Page 2 — Team Performance
Deep-dive into individual club statistics — wins, losses, draws, points accumulated, goal difference, home vs. away record, and win rate over selected seasons. Supports drill-through to match-level detail.

### Page 3 — Discipline Analysis
Visual breakdown of yellow cards, red cards, and fouls by team and referee. Highlights the most disciplined and most penalised clubs across seasons with trend analysis.

### Page 4 — Match Insights
Match-level explorer showing scorelines, half-time vs. full-time result comparison, comeback wins, and high-scoring games. Enables filtering by home team, away team, referee, and season.

---

## 📐 Data Model

Built on a **star schema** with the following structure:

- **Fact Table:** `Fact_Matches` — one row per match containing scores, cards, result codes, and foreign keys
- **Dimension Tables:**
  - `Dim_Teams` — club names and identifiers
  - `Dim_Seasons` — season year, matchweek, and era grouping
  - `Dim_Date` — full date table for time intelligence functions
- **Relationships:** All dimensions connected to the fact table via one-to-many relationships; cross-filter direction set to single for performance

---

## 📊 Key DAX Measures

```DAX
-- Total Goals Scored
Total Goals = SUM(Fact_Matches[HomeGoals]) + SUM(Fact_Matches[AwayGoals])

-- Win Rate %
Win Rate % = 
DIVIDE(
    CALCULATE(COUNTROWS(Fact_Matches), Fact_Matches[Result] = "W"),
    COUNTROWS(Fact_Matches)
) * 100

-- Points Accumulated
Points = 
CALCULATE(
    SUMX(Fact_Matches, 
        IF(Fact_Matches[Result] = "W", 3,
        IF(Fact_Matches[Result] = "D", 1, 0))
    )
)

-- Clean Sheets
Clean Sheets = 
CALCULATE(
    COUNTROWS(Fact_Matches),
    Fact_Matches[GoalsConceded] = 0
)

-- Average Goals Per Game
Avg Goals Per Game = DIVIDE([Total Goals], COUNTROWS(Fact_Matches))
```

---

## 🔧 Data Cleaning & Transformation (Power Query)

- Removed duplicate match records and null-value rows across all 3 CSV files
- Standardised team name formats (e.g. `Man Utd` → `Manchester United`) for consistent merging
- Split date columns and derived `Season_Year`, `Month`, and `Matchweek` fields
- Created a `Result` column (W / D / L) from the perspective of the home team
- Merged `matches.csv` with `teams.csv` on team ID to resolve home and away club names
- Appended season metadata from `seasons.csv` using a left join on season key
- Replaced coded referee names with full names where available

---

## 💡 Key Business Insights

- **Home advantage is significant but declining** — home win rate across all seasons sits at ~46%, down from ~52% in the mid-1990s, suggesting greater tactical parity in the modern game
- **Manchester United and Arsenal dominated the pre-2010 era** — combining for over 35% of all title-winning seasons between 1993 and 2010
- **Goals per game have increased steadily since 2015** — rising from an average of 2.5 to 2.9 by the 2024/25 season, reflecting a shift towards higher-tempo, attacking football
- **Disciplinary records correlate with league position** — bottom-half clubs average 18% more yellow cards per game than top-6 sides, indicating aggressive pressing under pressure
- **High-scoring matches (4+ goals) are 23% more likely in December** — fixture congestion and fatigue appear to be a measurable factor in defensive performance

---

## 📚 Skills Demonstrated

- End-to-end Power BI project development from raw data to polished dashboard
- Data cleaning and feature engineering using Power Query (M Language)
- Star schema data modelling with relationship management in Power BI
- DAX measure authoring including time intelligence, conditional aggregations, and KPIs
- Interactive report design with slicers, drill-through, bookmarks, and cross-filtering
- Translating 32 seasons of football data into clear, stakeholder-ready business insights

---

## 👨‍💻 Author

**Kaviraj Desai**

- LinkedIn: [linkedin.com/in/kavirajdesai](https://linkedin.com/in/kavirajdesai)
- GitHub: [github.com/kavirajdesai](https://github.com/kavirajdesai)
