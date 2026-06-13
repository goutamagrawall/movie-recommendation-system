# 🎬 Movie Recommendation System

A full-stack movie recommendation engine powered by **TF-IDF cosine similarity** and the **TMDB API**, built with **FastAPI** (backend) and **Streamlit** (frontend).

![Python](https://img.shields.io/badge/Python-3.10+-blue?logo=python&logoColor=white)
![FastAPI](https://img.shields.io/badge/FastAPI-0.100+-009688?logo=fastapi&logoColor=white)
![Streamlit](https://img.shields.io/badge/Streamlit-1.30+-FF4B4B?logo=streamlit&logoColor=white)
![scikit-learn](https://img.shields.io/badge/scikit--learn-1.3+-F7931E?logo=scikit-learn&logoColor=white)

---

## ✨ Features

- **Content-Based Recommendations** — TF-IDF vectorization + cosine similarity on movie metadata (overview, genres, keywords)
- **Genre-Based Discovery** — TMDB Discover API finds popular movies in the same genre
- **Live Movie Database** — Real-time posters, ratings, and details from TMDB
- **Keyword Search** — Autocomplete suggestions with word-match filtering
- **Home Feed** — Browse Trending, Popular, Top Rated, Upcoming, and Now Playing movies

## 🏗️ Architecture

```
┌──────────────────┐         HTTP          ┌──────────────────────┐
│   Streamlit UI   │ ◄──────────────────► │   FastAPI Backend    │
│   (app.py)       │    localhost:8501     │   (main.py)          │
└──────────────────┘                      └────────┬─────────────┘
                                                   │
                                    ┌──────────────┼──────────────┐
                                    ▼              ▼              ▼
                              ┌──────────┐  ┌───────────┐  ┌──────────┐
                              │ TMDB API │  │ TF-IDF    │  │ df.pkl   │
                              │ (live)   │  │ Matrix    │  │ (45K     │
                              └──────────┘  └───────────┘  │  movies) │
                                                           └──────────┘
```

## 🚀 Quick Start

### Prerequisites
- Python 3.10+
- [TMDB API Key](https://www.themoviedb.org/settings/api) (free)

### Setup

```bash
# Clone the repo
git clone https://github.com/<your-username>/movie_recommendation_system.git
cd movie_recommendation_system

# Install dependencies
pip install -r requirements.txt

# Add your TMDB API key
echo "TMDB_API_KEY=your_api_key_here" > .env

# Start the FastAPI backend
uvicorn main:app --host 127.0.0.1 --port 8000

# In a new terminal — start the Streamlit frontend
streamlit run app.py
```

Open [http://localhost:8501](http://localhost:8501) in your browser.

## 📡 API Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| `GET` | `/health` | Health check |
| `GET` | `/home?category=popular` | Home feed (trending, popular, top_rated, upcoming, now_playing) |
| `GET` | `/tmdb/search?query=batman` | TMDB keyword search |
| `GET` | `/movie/id/{tmdb_id}` | Movie details by TMDB ID |
| `GET` | `/recommend/tfidf?title=The+Dark+Knight` | TF-IDF content recommendations |
| `GET` | `/recommend/genre?tmdb_id=155` | Genre-based recommendations |
| `GET` | `/movie/search?query=inception` | Bundle: details + TF-IDF + genre recs |

Interactive API docs: [http://localhost:8000/docs](http://localhost:8000/docs)

## 🧠 How It Works

1. **Data Processing** — 45,000+ movies from [The Movies Dataset](https://www.kaggle.com/datasets/rounakbanik/the-movies-dataset) are preprocessed and vectorized
2. **TF-IDF Vectorization** — Movie overviews are converted to TF-IDF vectors using scikit-learn
3. **Cosine Similarity** — Given a movie, cosine similarity finds the most similar movies by content
4. **TMDB Enrichment** — Recommendations are enriched with live posters, ratings, and metadata from TMDB

## 🛠️ Tech Stack

| Layer | Technology |
|-------|-----------|
| Backend | FastAPI, Uvicorn |
| Frontend | Streamlit |
| ML/NLP | scikit-learn (TF-IDF), NumPy, SciPy |
| Data | Pandas, Pickle |
| External API | TMDB API v3 |
| HTTP Client | httpx (async, connection pooling) |

## 📁 Project Structure

```
movie_recommendation_system/
├── main.py                 # FastAPI backend — API routes, TF-IDF engine
├── app.py                  # Streamlit frontend — UI and navigation
├── movies.ipynb            # Jupyter notebook — data exploration & model training
├── df.pkl                  # Preprocessed movie DataFrame (~45K movies)
├── indices.pkl             # Title → index mapping for TF-IDF lookup
├── tfidf_matrix.pkl        # Precomputed TF-IDF sparse matrix
├── tfidf.pkl               # Fitted TfidfVectorizer
├── requirements.txt        # Python dependencies
├── runtime.txt             # Python version for deployment
└── .env                    # TMDB API key (not in repo)
```

## 🌐 Deployment

- **Backend**: Deployed on [Render](https://render.com)
- **Frontend**: Deployed on [Streamlit Community Cloud](https://streamlit.io/cloud)

## 📄 License

This project is open source and available under the [MIT License](LICENSE).

---

<p align="center">
  Built with ❤️ using FastAPI & Streamlit
</p>
