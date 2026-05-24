# Movie & TV Show Recommender System

> **PSTAT 134 — Statistical Data Science | Spring 2026**
> UC Santa Barbara

---

## 🚧 Project Status: IN PROGRESS

| Task | Status |
|------|--------|
| Data collection via TMDB API | ✅ Done |
| Data cleaning & feature engineering | ✅ Done |
| TF-IDF vectorization | ✅ Done |
| Cosine similarity matrix | ✅ Done |
| `recomend()` function — complete implementation | ✅ Done |
| EDA visualizations (need ≥ 4 plots/tables) | ✅ Done |
| Introduction section (markdown) | ⬜ TODO |
| Results section with sample outputs | ⬜ TODO |
| Discussion & Conclusion section | ⬜ TODO |
| Render notebook (Kernel → Restart & Run All) | ⬜ TODO |
| Export as `.html` and commit to repo | ⬜ TODO |

---

## 👥 Team Members

- Sid Revanuru
- Jayden Gould
- Jason Kim
- Clark Enge

---

## 📖 Description

This project builds a **content-based movie and TV show recommender system** using metadata from the [TMDB API](https://developer.themoviedb.org/reference/intro/getting-started). Given a title as input, the system ranks similar titles by analyzing content features — genres, cast, keywords, and plot overview text — using TF-IDF vectorization and cosine similarity, with popularity and vote average as secondary weighting factors.

---

## 📁 Repository Structure

```
Movie-TV-Show-Recommender/
├── PSTAT 134 FINAL PROJECT.ipynb   ← Main project notebook
├── PSTAT 134 FINAL PROJECT.html    ← Rendered report (TO BE ADDED before submission)
├── Project_Memo.ipynb              ← Initial project proposal
├── Project_Memo.html               ← Rendered project memo
├── testing.ipynb                   ← Development/scratch notebook
├── all_movie_data                  ← Cached TMDB dataset (pickle)
└── README.md                       ← This file
```

---

## ⚙️ Setup & Installation

**Requirements:** Python 3.9+, Jupyter Lab or Jupyter Notebook

```bash
pip install pandas numpy scikit-learn requests jupyter wordcloud matplotlib seaborn
```

**TMDB API Key** (only needed if regenerating data from scratch):
```python
API_TOKEN = "YOUR_TOKEN_HERE"  # Set in notebook before running data pull
```
> If `all_movie_data` is present in the repo root, the notebook loads it directly and skips the API call.

---

## 🚀 Usage

1. Clone the repo and open `PSTAT 134 FINAL PROJECT.ipynb` in Jupyter.
2. Run **Kernel → Restart & Run All** to execute all cells in order.
3. Call the recommender (once the function is complete):
```python
recomend("Inception", text_weight=0.7, pop_weight=0.2, vote_weight=0.1)
```

---

## ✅ Pre-Submission Checklist

- [ ] `recomend()` function is fully implemented and tested
- [ ] At least **4 visualizations** are present in the notebook
- [ ] **Introduction** section written at the top of the notebook
- [ ] **Results** section shows sample recommender outputs and discusses findings
- [ ] **Discussion/Conclusion** section reflects on limitations and takeaways
- [ ] All cells run top-to-bottom with sequential execution counters
- [ ] Notebook exported as `PSTAT 134 FINAL PROJECT.html` and committed
- [ ] README updated with final results summary

---

## 📄 Rubric Reference (Written Report — 50 pts)

| Criterion | Pts | Requirement |
|-----------|-----|-------------|
| Content | 15 | Thorough understanding of DS concepts; clear methodology, analysis, and results |
| Organization | 15 | Clear intro, methods, results, and conclusion sections |
| Clarity & Style | 10 | Concise writing, appropriate terminology, complete sentences |
| Visualizations | 5 | At least 4 effective, relevant plots or tables |
| Formatting | 5 | All code evaluated/rendered; report readable as `.html` or `.pdf` |

---

## 🙏 Acknowledgements

Data sourced from [The Movie Database (TMDB)](https://www.themoviedb.org/). Project completed for PSTAT 134 at UC Santa Barbara.
