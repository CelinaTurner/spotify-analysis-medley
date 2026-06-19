# Medley of Music Analysis
<img src="https://raw.githubusercontent.com/CelinaTurner/spotify-analysis-medley/main/images/medley-music-analysis.svg"/>
Exploratory analysis and unsupervised clustering of a Spotify dataset covering
tracks from **1900–2021** (~586k songs, 20 features). The goal: understand what
makes songs popular, which artists are most prolific, and whether songs cluster
into natural groups based on their audio characteristics alone.

**Stack:** Python · pandas · scikit-learn · seaborn / matplotlib · Plotly · Jupyter

---

## 1. Cleaning & cardinality

Started with a full look at the 586,672-row dataset — types, nulls (71 missing
in `Name`, dropped), and cardinality across the categorical columns (`id`,
`name`, `artists`, `artist_id`, `release_date`).

<img src="images/Cardinality.PNG?raw=true"/>

## 2. Most prolific & most popular artists

Counting songs per artist surfaced a quirk worth noting: the top "artist," *Die
Drei*, is a German audiobook series — a reminder that this dataset doesn't
separate spoken-word from music. I tried isolating it via `speechiness` but
couldn't cleanly split audiobooks from wordy genres like rap, so it's flagged
for future work.

<img src="images/Prolific.PNG?raw=true"/>

Ranking by average popularity per artist turned up a few surprises — Bad Bunny
and Rosalía landed in the top three.

## 3. Feature correlation

A heatmap of the audio features showed the strongest relationships are
**loudness ↔ energy (0.77)** and **valence ↔ danceability (0.53)** — both
intuitive: louder songs feel more energetic, and happier-sounding songs are more
danceable.

<img src="images/Heatmap.PNG?raw=true"/>

## 4. K-Means clustering

Standardized the features (z-score), used the **Elbow Method** to settle on
**8 clusters**, then reduced to 2D with PCA to visualize.

```python
features = ['explicit','danceability','energy','key','loudness','mode',
            'speechiness','acousticness','instrumentalness','liveness',
            'valence','tempo','duration_ms']
df = (track_df[features] - track_df[features].mean()) / track_df[features].std()

kmeans = KMeans(n_clusters=8, random_state=1).fit(df)
clusters = kmeans.predict(df)
silhouette_score(df, clusters)   # ~0.15
```

The silhouette score (~0.15) and the scatter plot tell an honest story: the
clusters overlap heavily. Songs don't separate cleanly on audio features alone —
there's more to what makes a track distinct than these 13 dimensions capture.

<img src="images/Scatter.PNG?raw=true"/>

Comparing feature means across clusters did reveal sensible patterns: explicit
tracks trend loud and danceable, low on acousticness; speechiness tracks with
liveness; instrumentalness tracks with acousticness and against loudness.

<img src="images/Cluster.PNG?raw=true"/>

## 5. Takeaways & next steps

Audio features alone don't cleanly classify songs — the weak cluster separation
is itself the finding. Next, I'd like to bring in genre labels, separate
spoken-word content, and try density-based or hierarchical clustering to see if
other algorithms find structure K-Means missed.
