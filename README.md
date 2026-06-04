# Movie Recommender System

> **PSTAT 134 — Statistical Data Science | Spring 2026**
> UC Santa Barbara

---

## Project Status: ANALYSIS COMPLETE

The notebook is finished and runs top to bottom with sequential execution counts. The only steps left are exporting the rendered report and submitting it.

| Task | Status |
|------|--------|
| Data collection via TMDB API | Done |
| Data cleaning & feature engineering | Done |
| Tag construction & weighting (genres x3, cast x2, keywords x2) | Done |
| TF-IDF vectorization | Done |
| Cosine similarity matrix | Done |
| `recommend()` function — complete implementation | Done |
| Score-weight and tag-weight tuning | Done |
| EDA visualizations (4 plots) | Done |
| Introduction section | Done |
| Results section with live recommender outputs | Done |
| Discussion & Conclusion section | Done |
| Notebook executed end to end (Restart & Run All) | Done |
| Export as `.html` and commit to repo | Pending |
| Submit written report and oral slides | Pending |

---

## Team Members

- Sid Revanuru
- Jayden Gould
- Jason Kim
- Clark Enge

---

## Description

This project builds a **content-based movie recommender system** using metadata from the [TMDB API](https://developer.themoviedb.org/reference/intro/getting-started). Given a movie title, the system ranks similar titles by analyzing content features (plot overview, genres, cast, and keywords) with TF-IDF vectorization and cosine similarity. Popularity and vote average enter as low-weight tiebreakers. The dataset is roughly 9,925 movies pulled from the TMDB discovery endpoint, sorted by popularity.

---

## Methods

1. **Data collection.** Pull movies from the TMDB `discover/movie` endpoint, then fetch details, credits, and keywords for each title.
2. **Feature engineering.** Combine each movie's overview, genres, cast, and keywords into a single `tags` field. Multi-word tokens are collapsed (for example `Science Fiction` becomes `ScienceFiction`) so TF-IDF treats them as one term. Overview words are stemmed; genres, cast, and keywords are up-weighted (3x, 2x, 2x) so they carry more signal than a single shared overview word.
3. **Vectorization.** Apply TF-IDF over the `tags` field with a 5,000-term vocabulary and English stop words removed.
4. **Similarity.** Compute the pairwise cosine similarity matrix across all titles.
5. **Ranking.** For a queried title, take the 100 most text-similar candidates and re-rank them with a weighted final score:

   `final_score = 0.95 * text_similarity + 0.03 * popularity + 0.02 * vote_average`

---

## Key Findings

The recommender was tested on three titles:

- **The Dark Knight** — strongest results. The top eight recommendations are all Batman-franchise films, with scores of 0.23 to 0.43. Named franchises share explicit proper-noun tokens, which produces tight clusters in TF-IDF space.
- **Interstellar** — moderate results. All recommendations are Sci-Fi or space-themed, with strong matches such as Gravity, The Martian, and Apollo 13 (scores 0.22 to 0.28).
- **Inception** — weakest results. Its short, generic overview overlaps broadly with many films, so the list is a mixed bag (scores 0.18 to 0.27).

Raising the genre, cast, and keyword weights and lowering the popularity weight (from 0.20 to 0.03) removed popular but unrelated films from the top ranks, such as a musical comedy that previously surfaced first for Inception.

---

## Repository Structure

```
Movie-TV-Show-Recommender/
├── PSTAT 134 FINAL PROJECT.ipynb   <- Main project notebook (executed)
├── PSTAT 134 FINAL PROJECT.html    <- Rendered report (to be added before submission)
├── Project_Memo.ipynb              <- Initial project proposal
├── Project_Memo.html               <- Rendered project memo
├── testing.ipynb                   <- Development/scratch notebook
├── all_movie_data                  <- Cached TMDB dataset (pickle)
├── .gitignore                      <- Ignores local-only files
└── README.md                       <- This file
```

> `Project Information Pages/` (course rubric and instructions) is kept locally and excluded from the repo via `.gitignore`.

---

## Setup & Installation

**Requirements:** Python 3.9+, Jupyter Lab or Jupyter Notebook

```bash
pip install pandas numpy scikit-learn nltk requests jupyter wordcloud matplotlib seaborn
```

**TMDB API Key** (only needed if regenerating data from scratch):
```python
API_TOKEN = "YOUR_TOKEN_HERE"  # Set in notebook before running data pull
```
> If `all_movie_data` is present in the repo root, the notebook loads it directly and skips the API call.

---

## Usage

1. Clone the repo and open `PSTAT 134 FINAL PROJECT.ipynb` in Jupyter.
2. Run **Kernel -> Restart & Run All** to execute all cells in order.
3. Call the recommender:
```python
recommend("Inception")
# or with custom weights:
recommend("Inception", text_weight=0.95, pop_weight=0.03, vote_weight=0.02)
```

---

## Pre-Submission Checklist

- [x] `recommend()` function is fully implemented and tested
- [x] At least **4 visualizations** are present in the notebook
- [x] **Introduction** section written at the top of the notebook
- [x] **Results** section shows live recommender outputs and discusses findings
- [x] **Discussion/Conclusion** section reflects on limitations and takeaways
- [x] All cells run top to bottom with sequential execution counters
- [x] README updated with final results summary
- [ ] Notebook exported as `PSTAT 134 FINAL PROJECT.html` and committed
- [ ] Written report and oral slides submitted

---

## Rubric Reference (Written Report — 50 pts)

| Criterion | Pts | Requirement |
|-----------|-----|-------------|
| Content | 15 | Thorough understanding of DS concepts; clear methodology, analysis, and results |
| Organization | 15 | Clear intro, methods, results, and conclusion sections |
| Clarity & Style | 10 | Concise writing, appropriate terminology, complete sentences |
| Visualizations | 5 | At least 4 effective, relevant plots or tables |
| Formatting | 5 | All code evaluated/rendered; report readable as `.html` or `.pdf` |

---

## Acknowledgements

Data sourced from [The Movie Database (TMDB)](https://www.themoviedb.org/). Project completed for PSTAT 134 at UC Santa Barbara.
