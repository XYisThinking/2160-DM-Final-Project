# Steam Genre Co-Occurrence Network Analysis

This project analyzes how game genres connect in the Steam ecosystem using network science techniques, and explores whether network structure can predict a game's price tier.

## Dataset

Steam Dataset 2025 from Kaggle:
https://www.kaggle.com/datasets/crainbramp/steam-dataset-2025-multi-modal-gaming-analytics

The full dataset contains multiple files, this project uses the following three:

| File | Description |
|------|-------------|
| applications.csv | 239,664 Steam applications with metadata such as price, platform support, release date, and supported languages |
| application_genres.csv | 587,515 app-genre tag pairs linking applications to genre IDs |
| genres.csv | 154 genre entries with multi-language labels |

## Project Structure

```
steam-genre-network/
  README.md
  steam_genre_network_analysis.ipynb
  steam_genre_network_report.pdf
  data/
    applications.csv
    application_genres.csv
    genres.csv
```

## How to Run

1. Install dependencies: pandas, numpy, matplotlib, networkx, scikit-learn
2. Download the three CSV files from the Kaggle link above and place them in `data/`
3. Update `DATA_DIR` in the notebook to point to your `data/` folder
4. Run all cells in order

## Methods

The analysis consists of four parts:

1. A genre-level co-occurrence network where nodes are genres and edge weights represent the number of games tagged with both genres. Centrality metrics including weighted degree, betweenness, closeness, and PageRank are computed for each genre. Community structure is detected using greedy modularity optimization.

2. A game-level network visualization built via snowball sampling. A pool of 3,000 multi-genre games is randomly sampled, edges are created between games sharing at least 2 genre tags, and 500 connected games are selected through snowball sampling from the highest-degree seed.

3. A temporal trend analysis of genre popularity from 2010 to 2025.

4. A price tier prediction task that classifies 88,529 paid games into three tiers using network-derived features and game metadata. Three classifiers are compared: Logistic Regression, Random Forest, and Gradient Boosting.

## Results

The genre network contains 18 nodes and 125 edges. Indie has the highest PageRank at 0.197 and covers over 101,000 games. Community detection identified 5 genre clusters. The Random Forest classifier achieved 59.8% accuracy for 3-tier price classification, with achievement count, language count, and mean PageRank as the top predictive features.


