# EXPERIMENTAL SETUP

To reproduce the recommendation models presented in the paper — namely six state-of-the-art Collaborative Filtering algorithms (**ItemKNN**[1], **UserKNN**[2], **BPR**[3], **SVD**[4], **VAECF**[5], and **NeuMF**[6]) — we used the **Cornac** framework [7]. Cornac was employed to generate per-user top-*n* recommendation lists with a consistent output format compatible with the **CONFIGRE** re-ranking algorithm.

Each dataset was randomly divided into a **train set (80%)** and a **test set (20%)**. For each algorithm, the *top-1000* recommendations (top-*n*) were generated and later re-ranked into *top-10* lists (top-*k*) using **CONFIGRE**, which enforces provider fairness across **continents** and **countries**. Recommendation performance was evaluated using **Normalized Discounted Cumulative Gain (NDCG)**.

---

# DATASETS OVERVIEW

This repository contains four enriched datasets with **geographical metadata** for research and analysis across multiple domains. Each dataset is provided as a CSV file with attributes relevant to its specific context.

## 1. Movies Dataset (`movies.csv`)
- **Description**: Items from MovieLens-1M, enriched with country/continent of production.  
- **Contents**: 3,600 movies.  
- **Geographical Data**: 62 countries, 6 continents.  
- **Special Attributes**: IMDB ID linked to country data via the OMDb API (http://www.omdbapi.com/).  
- **Notes**: Multi-country productions are included; continent derivation provided.

## 2. Books Dataset (`books.csv`)
- **Description**: Items from Book-Crossing with geographical metadata.  
- **Contents**: 12,314 books.  
- **Geographical Data**: 11 countries, 4 continents.  
- **Special Attributes**: ISBNs linked to country/continent using the Global Register of Publishers (https://grp.isbn-international.org/search/piid_cineca_solr).

## 3. Courses Dataset (`courses.csv`)
- **Description**: Courses with geographic provenance of providers and users.  
- **Contents**: 11,454 courses.  
- **Geographical Data**: 71 countries, 6 continents.  
- **Special Attributes**: Instructor time zones and inferred continental affiliations.

## 4. Songs Dataset (`songs.csv`)
- **Description**: The DataSongs dataset, including song ratings and artist origin.  
- **Contents**: 1,777,981 ratings (1–5) by 30,759 users for 16,380 songs.  
- **Geographical Data**: 54 countries, 6 continents.  
- **Special Attributes**: Artist’s country and continent of origin for each song.

> **General notes**: CSV files include headers aligned with the descriptions above. Please handle data responsibly, especially when linking to external APIs or third-party resources.

---

# EXECUTION GUIDE (NOTEBOOK)

The fairness post-processing is implemented in the notebook **`CONFIGRE_VF_final.ipynb`**. Run each cell **sequentially** from top to bottom. The notebook generates all intermediate and final CSV files automatically.

## Inputs required in the working directory
- `train.csv` — training data used to compute global proportions.  
- `<algorithm>.csv` — Cornac-generated top-*n* recommendation lists for each model (`BPR.csv`, `SVD.csv`, `UserKNN.csv`, `ItemKNN.csv`, `VAECF.csv`, `NeuMF.csv`).  
  Required columns: `id, user, item, rating, position, continent, country`.

## Notebook sections and outputs

| # | Section (cell group) | What it does | Output |
|---|-----------------------|--------------|--------|
| 1 | **Compute continental proportions** | Aggregates `train.csv` by `continent` and allocates the number of items per continent for the final *top-k*. | `porc-cont.csv` (`continent, percent_continent, new_continents`) |
| 2 | **Compute country proportions** | Aggregates `train.csv` by `country` and allocates the number of items per country. | `porc-country.csv` (`country, percent_country, new_countries`) |
| 3 | **Compute loss per algorithm** | For `algorithm = '<ModelName>'`, normalizes `rating` (min-max), computes a per-record loss relative to the base at position *k*, and zeroes loss for positions `< k`. | `<algorithm>-loss.csv` |
| 4 | **Merge proportional metadata** | Joins `*-loss.csv` with `porc-cont.csv` and `porc-country.csv`. Sorts by priority keys for re-ranking. | `<algorithm>-join.csv` |
| 5 | **Run CONFIGRE (3 phases)** | Three-phase assignment to build fair *top-k* per user: **Phase 1:** meet country & continent targets; **Phase 2:** fill remaining continent targets; **Phase 3:** complete user lists. | `<algorithm>-<tol*100>.csv` (e.g., `ItemKNN-100.csv` when `tolerance = 1`) |

### Parameters inside the notebook
```python
algorithm = 'ItemKNN'   # 'BPR' | 'SVD' | 'UserKNN' | 'ItemKNN' | 'VAECF' | 'NeuMF'
topk = 10               # final list length per user after re-ranking
topn = 1000             # length of the initial list per user (from Cornac)
tolerance = 1           # used in the final filename as <tolerance*100>
```
# EXECUTION GUIDE (NOTEBOOK)

# (optional) create a virtual environment
python -m venv .venv
source .venv/bin/activate  # Windows: .venv\Scripts\activate

# dependencies for the notebook
pip install pandas numpy scikit-learn jupyter

# (optional) if you need to generate <algorithm>.csv files with Cornac:
pip install cornac

# CITATION
If you use the datasets, the CONFIGRE implementation, or the experimental setup in your research, please cite:


# CONTACT

For inquiries or collaborations, please contact:

- david.contreras@salle.url.edu
- egomezy109@gmail.com

# REFERENCES

1. **Cornac** — Truong, S., Nguyen, T., Nguyen, A., et al. *Cornac: A Comparative Framework for Multimodal Recommender Systems.* **JMLR**, 21(95):1–5, 2020.  
2. **ItemKNN** — Sarwar, B., Karypis, G., Konstan, J., & Riedl, J. *Item-Based Collaborative Filtering Recommendation Algorithms.* **WWW**, 2001.  
3. **UserKNN** — Resnick, P., Iacovou, N., Suchak, M., Bergstrom, P., & Riedl, J. *GroupLens: An Open Architecture for Collaborative Filtering of Netnews.* **CSCW**, 1994.  
4. **BPR** — Rendle, S., Freudenthaler, C., Gantner, Z., & Schmidt-Thieme, L. *BPR: Bayesian Personalized Ranking from Implicit Feedback.* **UAI**, 2009.  
5. **SVD / Matrix Factorization** — Koren, Y., Bell, R., & Volinsky, C. *Matrix Factorization Techniques for Recommender Systems.* **IEEE Computer**, 42(8):30–37, 2009.  
6. **VAECF** — Liang, D., Krishnan, R., Hoffman, M., & Jebara, T. *Variational Autoencoders for Collaborative Filtering.* **WWW**, 2018.  
7. **NeuMF** — He, X., Liao, L., Zhang, H., Nie, L., Hu, X., & Chua, T.-S. *Neural Collaborative Filtering.* **WWW**, 2017.
