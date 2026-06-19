# Medley of Music Analysis

Exploratory analysis and unsupervised clustering of a Spotify dataset spanning
**1900–2021** — looking at how popular music's sound has shifted over a century,
and whether songs group into natural "moods" based on their audio features.

## What's inside

A Python notebook that:

- Explores trends across ~170k tracks — popularity, the most prolific artists,
  and how audio features (energy, acousticness, loudness, danceability, etc.)
  have moved over time.
- Examines correlations between audio features to see which travel together.
- Runs **K-Means clustering** to group songs into audio-feature segments —
  surfacing clusters that read like intuitive "moods" rather than genres.

## A few findings

<!-- Replace these with your actual results — one or two is plenty -->
- Recorded music trended measurably louder and less acoustic over the century.
- [your second finding — e.g. "energy and loudness are tightly correlated; acousticness moves opposite both"]
- K-Means surfaced [N] clusters; the clearest split was [e.g. mellow/acoustic vs. high-energy/danceable].

## Stack

Python · pandas · scikit-learn · matplotlib / seaborn · Jupyter

## Running it

```bash
pip install -r requirements.txt
jupyter notebook   # open the analysis notebook and run top to bottom
```

Dataset: [Spotify Tracks 1921–2020 (Kaggle)](https://www.kaggle.com/datasets/yamaerenay/spotify-dataset-19212020-160k-tracks)

---

More projects at [celinaturner.github.io](https://celinaturner.github.io)
