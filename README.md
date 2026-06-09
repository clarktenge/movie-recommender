# Movie Recommender System

A content-based recommender system that suggests movies and TV shows using TF-IDF vectorization, cosine similarity, and weighted feature engineering on TMDB metadata. Given a title, it returns the most similar films ranked by a blend of text similarity, popularity, and vote average.

---

## How It Works

1. **Data collection** — ~9,925 movies pulled from the TMDB `discover/movie` endpoint, with per-title details, credits, and keywords fetched via separate API calls.

2. **Feature engineering** — Overview, genres, cast, and keywords are combined into a single `tags` field. Multi-word tokens are collapsed (`Science Fiction` → `ScienceFiction`) so TF-IDF treats them as atomic terms. Overview words are stemmed; genres, cast, and keywords are up-weighted (3×, 2×, 2×) to carry more signal than raw overview text.

3. **Vectorization** — TF-IDF over `tags` with a 5,000-term vocabulary; English stop words removed.

4. **Similarity** — Pairwise cosine similarity matrix across all titles.

5. **Ranking** — For a query, take the 100 most text-similar candidates and re-rank with a weighted final score:

   ```
   final_score = 0.95 × text_similarity + 0.03 × popularity + 0.02 × vote_average
   ```

---

## Key Findings

- **The Dark Knight** — top 8 recommendations are all Batman-franchise films (scores 0.23–0.43). Named franchises share proper-noun tokens, producing tight clusters in TF-IDF space.
- **Interstellar** — all recommendations are Sci-Fi or space-themed; strong matches include *Gravity*, *The Martian*, and *Apollo 13* (scores 0.22–0.28).
- **Inception** — weakest results (scores 0.18–0.27). Its short, generic overview overlaps broadly with many films across genres.

Raising genre/cast/keyword weights and reducing the popularity weight (0.20 → 0.03) removed high-popularity but thematically unrelated films from top results.

---

## Setup

**Requirements:** Python 3.9+, Jupyter Lab or Jupyter Notebook

```bash
pip install -r requirements.txt
```

**TMDB API key** — only needed to regenerate data from scratch:

```python
API_TOKEN = "YOUR_TOKEN_HERE"  # Set at top of notebook before running the data pull
```

> If `all_movie_data.pkl` is present in the repo root, the notebook loads it directly and skips the API call.

---

## Usage

```bash
git clone https://github.com/clarktenge/movie-recommender.git
cd movie-recommender
jupyter notebook movie_recommender.ipynb
```

Run **Kernel → Restart & Run All**, then call the recommender:

```python
recommend("Inception")

# With custom weights:
recommend("Inception", text_weight=0.95, pop_weight=0.03, vote_weight=0.02)
```

---

## Repository Structure

```
movie-recommender/
├── movie_recommender.ipynb    ← Main analysis notebook (executed)
├── all_movie_data.pkl         ← Cached TMDB dataset (pickle)
├── requirements.txt
├── .gitignore
└── README.md
```

---

## Contributors

Built collaboratively by [Clark Enge](https://github.com/clarktenge), Sid Revanuru, Jayden Gould, and Jason Kim.

---

## Acknowledgements

Data sourced from [The Movie Database (TMDB)](https://www.themoviedb.org/).
