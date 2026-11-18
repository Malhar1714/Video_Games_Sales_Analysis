# Video_Games_Sales_Analysis

# Video Game Sales Analysis

This is a data analysis project on worldwide video game sales. I wanted to find out which genres, platforms, publishers and games sell the most, how sales have changed over the years, and how different regions compare. I used Python (pandas, Matplotlib and Seaborn) and did everything in a Jupyter Notebook.

## Why I made this

I wanted to practice the full flow of a data project: loading a raw dataset, checking and cleaning it, and then exploring it with charts to find insights. The dataset is large enough (over 16,000 games) to show real patterns, but still simple enough to follow.

## Key questions this project answers

1. Which genres sell the most?
2. Which gaming platforms are the most successful?
3. How have global video game sales changed over the years?
4. Which games are the all-time best sellers?
5. Which region buys the most games?
6. Do most games sell a lot, or only a few?
7. Which publishers lead the market?
8. How are the regional sales related to global sales?

## About the dataset

The data is in a CSV file called `vgsales.csv`. It has **16,598 rows** (one per game and platform) and **11 columns**, covering games released from **1980 to 2020**. All sales figures are in **millions of units**.

| Column | What it means |
|---|---|
| Rank | Rank of the game by global sales |
| Name | Name of the game |
| Platform | Platform the game was released on (e.g. Wii, PS2, X360) |
| Year | Year the game was released |
| Genre | Genre of the game (12 genres, e.g. Action, Sports, Shooter) |
| Publisher | Company that published the game |
| NA_Sales | Sales in North America |
| EU_Sales | Sales in Europe |
| JP_Sales | Sales in Japan |
| Other_Sales | Sales in the rest of the world |
| Global_Sales | Total worldwide sales |

**Good to know:** each row is a game on one platform, so the same game released on several platforms appears in several rows.

## Steps I followed

### 1. Loading and checking the data
- Read the CSV file with pandas
- Looked at the first rows, the shape, the data types, the column names and a statistical summary
- Checked for missing values and duplicate rows

**What I found:** the dataset has 16,598 rows and 11 columns. There were **no duplicate rows**. The only missing values were in the `Year` column: **271 rows (about 1.6%)**.

### 2. Cleaning the data
- Filled any missing `Publisher` values with `Unknown`
- Converted `Year` to an integer type
- Removed extra spaces from all the text columns
- Checked the unique platforms (31) and genres (12)
- Checked that there were no negative sales values
- Checked the release year range (1980 to 2020)
- Checked that the regional sales add up to the global sales
- Saved the cleaned data as `vgsales_cleaned.csv`

**Why:** Extra spaces make the same value look different (for example `"Sega "` and `"Sega"`), which breaks grouping. The negative sales and year range checks make sure there are no impossible values. The sales check showed that NA + EU + JP + Other differs from Global Sales by at most 0.02 million, which is only rounding, so the sales columns are consistent.

**Note:** I kept the 271 rows with a missing `Year` instead of deleting them, because they still have valid sales data. They are only left out of the year-based chart.

### 3. Exploring the data
I loaded the cleaned CSV and made these charts. For each one, here is what it shows and what I found.

#### 1. Total global sales by genre
- **What it shows:** Total sales of every genre, from highest to lowest.
- **Insight:** **Action** is the best-selling genre by far, at about 1,750 million units. **Sports** (about 1,330 million) and **Shooter** (about 1,040 million) follow. **Strategy**, **Adventure** and **Puzzle** sell the least. Genres with a broad audience and many releases dominate the market.

#### 2. Top 10 platforms by global sales
- **What it shows:** The ten platforms with the highest total sales.
- **Insight:** The **PS2** leads with about 1,250 million units sold. The **Xbox 360**, **PS3**, **Wii** and **DS** are close behind, each between about 820 and 980 million. The list is dominated by consoles from the 2000s, with the original **PS** also in the top six.

#### 3. Global video game sales by release year
- **What it shows:** Total sales of games grouped by the year they were released.
- **Insight:** Sales grew slowly through the 1980s and 1990s and rose sharply after 2000. They **peaked around 2008 to 2009 at about 680 million units**, then declined. The sudden drop to almost zero after 2016 is most likely because the dataset is **incomplete for the most recent years**, not because people stopped buying games.

#### 4. Top 10 best-selling video games
- **What it shows:** The ten games with the highest global sales.
- **Insight:** **Wii Sports** is far ahead of everything else at about 82.7 million units, more than double the second place, **Super Mario Bros.** (about 40.2 million). Nintendo titles fill most of the list, including Mario Kart Wii, Wii Sports Resort and Pokemon Red/Blue. Part of Wii Sports' lead comes from the fact that it was bundled with the Wii console.

#### 5. Total sales by region
- **What it shows:** Total sales in North America, Europe, Japan and the rest of the world.
- **Insight:** **North America is the biggest market** at roughly 4,400 million units, followed by Europe at about 2,400 million. Japan (about 1,300 million) and the rest of the world (about 800 million) are much smaller.

#### 6. Distribution of global sales (histogram)
- **What it shows:** How many games fall into each sales range.
- **Insight:** The distribution is **extremely skewed**. Most games sell very little: the median game sold only **0.17 million units**, while the average is **0.54 million**, pulled up by a few huge hits. The most extreme game sold 82.74 million. A small number of blockbusters account for a large share of total sales.

#### 7. Global sales by genre (box plot)
- **What it shows:** The spread of sales inside each genre.
- **Insight:** In every genre, the typical game sells a small amount and the boxes sit close to zero. The dots above them are **outliers**, which are the hit games. Sports has the single biggest outlier (Wii Sports), while Platform, Racing and Role-Playing also have strong hits. This shows that a genre's total sales depend heavily on a few big titles.

#### 8. Top 10 publishers by global sales
- **What it shows:** The publishers with the highest total sales, excluding the `Unknown` group.
- **Insight:** **Nintendo** leads at about 1,780 million units, followed by **Electronic Arts** (about 1,110 million) and **Activision** (about 730 million). Sony Computer Entertainment, Ubisoft, Take-Two, THQ, Konami, Sega and Namco Bandai complete the top 10. Nintendo's lead is large, which fits its many best-selling games.

#### 9. Correlation heatmap
- **What it shows:** How strongly the numeric columns move together (from -1 to +1).
- **Insight:**
  - **Global sales** is most strongly related to **NA sales (0.94)** and **EU sales (0.90)**, then Other (0.75) and Japan (0.61). So a game that sells well in North America and Europe usually sells well worldwide.
  - **Japan** has the weakest links to the other regions (0.29 to 0.45), which suggests Japanese tastes are different from the rest of the world.
  - **Rank** has a negative correlation with sales (about -0.4), which makes sense because rank 1 is the highest seller.
  - **Year** has almost no relationship with sales (-0.07).
  - Correlation does not mean one variable causes the other.

## Summary of findings

- **Genres:** Action, Sports and Shooter are the top three genres by total sales.
- **Platforms:** The PS2 is the best-selling platform, followed by the Xbox 360, PS3, Wii and DS.
- **Timeline:** Sales peaked around 2008 to 2009 and then declined. The drop after 2016 is probably because of missing data.
- **Best sellers:** Wii Sports is the top game by a large margin, and Nintendo dominates the top 10 games and the publisher ranking.
- **Regions:** North America is the biggest market, followed by Europe, Japan and the rest of the world.
- **Distribution:** Most games sell fewer than 1 million copies. A few hits drive the market.
- **Relationships:** Global sales follow North American and European sales most closely.

## Limitations

- The data looks incomplete for games released after about 2016, so the yearly trend at the end should not be trusted.
- Each row is a game on one platform, so a game released on many platforms is counted several times, and best sellers are per platform.
- Sales are physical sales figures in millions and do not include digital downloads.
- The 271 games with a missing release year are left out of the yearly chart.

## Project files

```
video_games.ipynb        the main notebook with all the code and charts
vgsales.csv              the original dataset
vgsales_cleaned.csv      the cleaned dataset (created by the notebook)
README.md                this file
```

## Tools used

- Python 3
- pandas and NumPy for data handling
- Matplotlib and Seaborn for charts
- Jupyter Notebook

## How to run it

1. Download or clone this project.
2. Install the libraries:
   ```
   pip install numpy pandas matplotlib seaborn jupyter
   ```
3. Make sure `vgsales.csv` is in the same folder as the notebook.
4. Start Jupyter:
   ```
   jupyter notebook
   ```
5. Open `video_games.ipynb` and run all the cells from top to bottom.

The first part of the notebook creates `vgsales_cleaned.csv`, and the second part reads it for the charts, so run the cells in order.

## Notes

- The numbers in the insights are read from the charts in the notebook, so they are approximate.
- The results describe this dataset and may not match the whole video game market.
