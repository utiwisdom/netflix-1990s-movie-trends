# Netflix 1990s Movies: Exploratory Data Analysis

![Red Popcorn](redpopcorn.jpg)

## Project Overview

This project explores Netflix's catalogue to understand movies released in the **1990s**, using Python and Pandas. The goal is to uncover what a "typical" 90s movie looked like and how much of the decade's action catalogue was built around short, fast-paced storytelling.

Two questions drive the analysis:
- **What was the most frequent movie duration in the 1990s?**
- **How many short action movies (under 90 minutes) were released in the 1990s?**

### Business Scenario
> You work for a production company that specializes in nostalgic styles. Before greenlighting a 90s-inspired project, the team wants data on how long these movies ran and how common short action films were.

### Why This Matters
Runtime is a real production decision. It drives shooting schedules, budget, editing, cinema scheduling, and viewer retention on streaming platforms. Knowing the typical length of 90s movies gives a production company a data-backed target for a nostalgia-style film instead of guessing. Knowing how common short action films were shows whether a lean, high-energy format is true to the era.

---

## Dataset

- **File:** `netflix_data.csv`
- **Source:** DataCamp project dataset (Netflix titles)
- **Key columns used:**

  | Column | Description |
  |---|---|
  | `type` | Type of show (`Movie` or `TV Show`) |
  | `release_year` | Year of release |
  | `duration` | Duration of the movie in minutes |
  | `genre` | Show genre (e.g. Action, Comedy, Drama) |

Other columns include `show_id`, `title`, `director`, `cast`, `country`, `date_added`, and `description`.

---

## Tools Used

- **Python 3**
- **Pandas** for filtering and aggregation
- **Matplotlib** for visualizing the duration distribution
- **Jupyter Notebook**

---

## Approach

1. Load `netflix_data.csv` into a Pandas DataFrame.
2. Filter to **movies** released between **1990 and 1999**.
3. Find the **mode** of `duration` to get the most frequent runtime.
4. Plot a histogram of durations to sanity-check the answer visually.
5. Filter the 1990s movies to **Action** with `duration < 90` and count them.

```python
import pandas as pd
import matplotlib.pyplot as plt

netflix_df = pd.read_csv("netflix_data.csv")

# 1990s movies only
movies_90s = netflix_df[
    (netflix_df["type"] == "Movie")
    & (netflix_df["release_year"] >= 1990)
    & (netflix_df["release_year"] < 2000)
]

# Most frequent duration
duration = int(movies_90s["duration"].mode()[0])

# Histogram of durations
plt.hist(movies_90s["duration"], bins=20)
plt.title("Distribution of 1990s Movie Durations")
plt.xlabel("Duration (minutes)")
plt.ylabel("Number of movies")
plt.show()

# Short action movies (< 90 minutes)
short_action = movies_90s[
    (movies_90s["genre"] == "Action") & (movies_90s["duration"] < 90)
]
short_movie_count = int(short_action.shape[0])
```

---

## Results

| Metric | Variable | Value |
|---|---|---|
| Most frequent movie duration in the 1990s | `duration` | **94 minutes** |
| Short action movies (< 90 min) in the 1990s | `short_movie_count` | **7** |

*(Confirm these against your notebook's exact output before publishing.)*

---

## Key Insights

- **The "typical" 90s movie ran about 94 minutes.** That is just over an hour and a half, which gives a clear runtime target for a nostalgia-style production.
- **Short action movies were rare.** Only a handful of action titles in the 1990s came in under 90 minutes, which suggests action films of the era leaned toward fuller runtimes rather than ultra-short formats.
- **Runtimes cluster tightly around the mode.** The histogram shows most 1990s movies fall in a narrow band, meaning the decade had a fairly consistent standard length.
- **Limitation:** this analysis covers only titles available on Netflix, not every film released in the 1990s, so results describe the Netflix catalogue rather than the whole decade.

### What This Means for a Production Company
A nostalgia-focused film should aim for roughly 90 to 100 minutes to feel authentic to the era. A sub-90-minute action film would be a deliberate stylistic choice, not the norm, so if the team wants that lean format it should be justified by pacing or budget, not by period accuracy.

### Next Steps
- Compare 1990s runtimes with the 2010s to test whether movies have gotten longer.
- Break down average duration by genre to see which genres ran longest.
- Look at which countries produced the most 1990s titles on Netflix.

---

## How to Run This Project

1. Clone the repository
2. Make sure `netflix_data.csv` is in the same folder as `notebook.ipynb`
3. Install dependencies: `pip install pandas matplotlib jupyter`
4. Open `notebook.ipynb` in Jupyter
5. Run all cells top to bottom

---

## Repository Structure

```
netflix-1990s-movies-eda/
├── notebook.ipynb
├── netflix_data.csv
├── redpopcorn.jpg
├── README.md
└── screenshots/
    ├── 01-setup.png
    ├── 02-duration-result.png
    └── 03-short-action-result.png
```

---

## Screenshots

### Project Setup
![Setup](screenshots/01-setup.png)

### Duration Result
![Duration Result](screenshots/02-duration-result.png)

### Short Action Movies Result
![Short Action Result](screenshots/03-short-action-result.png)

---

## Author

**Wisdom Uti**
ALX Data Engineering Graduate | Data Science Volunteer Mentor
[LinkedIn](https://linkedin.com/in/uti-wisdom-286602228/) · [GitHub](https://github.com/utiwisdom) · [Portfolio](https://datascienceportfol.io/wisdomuti8)
