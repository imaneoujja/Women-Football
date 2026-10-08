# Project of Data Visualization (COM-480)

| Team members |
|--------------|
| Imane Oujja |
| Shyamala Vasireddy |
| Rim Abkari |

[**Milestone 1**](#milestone-1) • [Milestone 2](#milestone-2) • [Milestone 3](#milestone-3)

## Milestone 1

### Dataset

Our main data comes from a single Kaggle repository: [Women's International Football Results](https://www.kaggle.com/datasets/martj42/womens-international-football-results). It contains three CSV files:

- **results.csv** — 11,177 matches from 1956 to 2025, with date, teams, scores, tournament, and venue. 247 teams, 117 different tournament types. Zero missing values, which is great.
- **goalscorers.csv** — 2,795 individual goal records with scorer name, minute, penalty/own goal flags. 1,055 unique scorers.
- **shootouts.csv** — 134 penalty shootout results.

The data is very clean and needs almost no preprocessing. The only real work is mapping the 247 team names to geographic regions for our spatial analysis — we wrote a lookup table for this but still have ~49 edge cases (historical teams like Czechoslovakia, small territories like Guernsey) that we need to handle.

On top of this, we manually compiled contextual data from FIFA and Wikipedia: World Cup attendance figures, prize money per edition, WSL league attendance, and men's World Cup prize money for comparison. These are small tables we define directly in the notebook.

For later milestones, we plan to integrate [StatsBomb Open Data](https://github.com/statsbomb/open-data) which has event-level data (every pass, shot, tackle) for the 2019 and 2023 Women's World Cups — this will let us build pitch-level tactical visualizations.

### Problematic

We want to tell the story of women's football going from a sport that was literally banned (England 1921–1971, Germany until 1970) to a global phenomenon with 2 billion TV viewers and $110M in World Cup prize money.

Our visualization explores three angles: **(1)** The historical growth — how did we get from 8 teams in the 1960s to 247 today? We want to show this on an interactive world map where nations "light up" as they start playing. **(2)** The economics — prize money went from $0 to $110M, attendance from 510K to nearly 2M, yet the gap with men's football is still enormous. Side-by-side comparisons make this visceral. **(3)** The football itself — who are the legends? When do goals happen? Which teams dominate shootouts? The goalscorer data lets us go beyond aggregates.

We think this topic works well because it has a clear narrative arc, the data supports diverse chart types (maps, timelines, bar races, minute-by-minute plots), and it's a story that hasn't been told much through interactive visualization. Our audience is anyone who follows football — or anyone curious about how a marginalized sport became a global movement.

### Exploratory Data Analysis

We ran a full EDA in our [notebook](eda.ipynb). Here are the highlights:

The dataset spans 1956–2025 with 11,177 matches. The United States leads all-time with 465 wins, followed by Germany and Sweden. Goals per match have barely declined over time (3.78 in the early era vs 3.51 post-2015), but the biggest blowouts have disappeared — the sport is getting more competitive. The craziest match? Cameroon 2–24 South Africa in 2006.

From the goalscorer data: Birgit Prinz (Germany) tops the charts with 34 recorded goals, ahead of Marta (24) and Abby Wambach (23). 53.6% of goals come in the second half vs 44.9% in the first — late drama is real. 7.6% of goals are penalties.

The shootout data shows a first-shooter win rate of 60.5% (n=38 with data), and 134 shootouts total since 1984. Regional analysis reveals Europe and North America dominating historically, but Asia (Japan, South Korea) and Africa (Nigeria, Cameroon) are catching up in recent decades.

The World Cup grew from 12 teams/510K attendance in 1991 to 32 teams/1.98M in 2023. Prize money was $0 until 2015 — now it's $110M, still just 11% of the men's $1B.

### Related work

The main existing work on this data is a [Towards Data Science article](https://towardsdatascience.com/fifa-womens-world-cup-2023-visualized-with-plotly-a7277edf6278/) that visualized the 2023 World Cup with Plotly — static charts focused on a single tournament. [FCrSTATS](https://github.com/FCrSTATS/StatsBomb_WomensData) used StatsBomb data for radar charts of individual players, but again very narrow. [Flourish](https://flourish.studio/blog/world-cup-euros-football-data-visualization/) published World Cup visualization templates, but they're generic and designed for men's tournaments. The [Deloitte Football Money League](https://www.deloitte.com/uk/en/services/consulting-financial/analysis/deloitte-football-money-league-women.html) publishes beautiful infographics on club revenue but as static PDFs.

What's missing is a project that **connects the big picture (global growth, economics) to the details (goalscorers, match-level patterns)** in one interactive experience. That's what we're building.

Our visual inspiration comes from [The Pudding](https://pudding.cool/) for their narrative scrolling + interactivity approach, [FiveThirtyEight's soccer predictions](https://projects.fivethirtyeight.com/soccer-predictions/) for clean sports dashboards, and the famous [Minard map](https://en.wikipedia.org/wiki/Charles_Joseph_Minard) shown in our course as an example of encoding many variables in a single visual. We haven't used this dataset in any other course.

---

## Milestone 2

Website : https://com-480-data-visualization.github.io/DVP/

Report : [Milestone 2 Report](https://github.com/com-480-data-visualization/DVP/blob/master/Milestones/Milestone2.pdf)

## Milestone 3

 **Screencast** : [Video Walkthrough](https://drive.google.com/file/d/1qZGAw3O_oByAsqgX97o9VKDP96bNKhKO/view?usp=sharing)

 
| Deliverable | Link |
|-------------|------|
| 🌐 **Live Website** | [https://com-480-data-visualization.github.io/DVP/](https://com-480-data-visualization.github.io/DVP/) |
| 📄 **Process Book** | [Process Book](https://github.com/com-480-data-visualization/DVP/blob/master/process_book.pdf)         |

 
---
 
## Overview
 
**Beyond the Pitch** is a scrollytelling data visualization website that tells the story of women's international football through 10 interactive D3.js chapters — from the 50-year ban to 2 billion viewers.
 
The site covers **11,177 matches**, **238 nations**, and **70 years of data** (1956–2025).
 
---
 
## Technical Setup
 
### Requirements
 
- A modern browser: **Chrome 90+**, Firefox 88+, Safari 14+, or Edge 90+
- No Node.js, no npm, no build step required
- Internet connection (to load D3.js, TopoJSON, and Google Fonts from CDN)
### Running Locally
 
**Option 1 — Open directly (simplest)**
```bash
open index.html        # macOS
start index.html       # Windows
xdg-open index.html    # Linux
```
All data is bundled in `data/bundle.js` — works offline.
 
**Option 2 — Local server (recommended for development)**
```bash
python3 -m http.server 8080
# then open http://localhost:8080
```
 
**Option 3 — VS Code Live Server**
 
Install the [Live Server extension](https://marketplace.visualstudio.com/items?itemName=ritwickdey.LiveServer), right-click `index.html` → *Open with Live Server*.
 
---
 
## Project Structure
 
```
DVP/
├── index.html              # Main single-page application (10 chapters)
├── css/
│   └── style.css           # Complete design system
├── js/
│   ├── charts.js           # All D3.js visualization functions
│   ├── crossfilter.js      # Cross-chart filter (map click → modal + scatter + race)
│   ├── interactions.js     # Scroll reveal, cursor, loader, nav, counters
│   ├── background.js       # Canvas particle background
│   └── mapfix.js           # Extended country name aliases (150+)
├── data/
│   ├── bundle.js           # All datasets inlined as window.BUNDLE (64KB)
│   └── processed/
│       ├── data.json        # Main dataset: teams, scorers, WC history, timeline
│       ├── race_data.json   # Cumulative wins per team per year
│       ├── chord_data.json  # Head-to-head win matrix (top 10 nations)
│       └── stream_data.json # Regional wins per year
├── img/
│   ├── bg_pitch.jpg        # Football pitch background
│   ├── img_marta.jpg       # Marta (Brazil)
│   ├── img_prinz.webp      # Birgit Prinz (Germany)
│   ├── img_wambach.jpg     # Abby Wambach (United States)
│   ├── img_hero1.jpg       # Hero collage — player 1
│   ├── img_hero2.webp      # Hero collage — player 2
│   ├── img_hero3.avif      # Hero collage — player 3
│   ├── img_hero4.jpg       # Hero collage — player 4
│   └── img_salma.webp      # Salma Paralluelo (Spain)
├── Milestones/             # Milestone 1, 2, 3 deliverables
├── eda.ipynb               # Exploratory data analysis (Milestone 1)
├── requirements.txt        # Python packages for the EDA notebook
├── process_book.pdf        # Full design and development documentation
└── README.md               # This file
```
 
---
 
## Data Sources
 
| Dataset | Source | Records |
|---------|--------|---------|
| Women's International Football Results | [Kaggle](https://www.kaggle.com/datasets/martj42/womens-international-football-results) | 11,177 matches |
| World Cup Prize Money | FIFA official communications | 9 editions |
| World Cup Attendance | FIFA official communications | 9 editions |
 
Data preprocessing done in Python (pandas). All datasets bundled into `data/bundle.js`.

### Re-running the exploratory analysis

The EDA is in [`eda.ipynb`](eda.ipynb). It reads the raw Kaggle files, which are not included in this repo:

1. Download `results.csv`, `goalscorers.csv` and `shootouts.csv` from the [Kaggle dataset](https://www.kaggle.com/datasets/martj42/womens-international-football-results) into `data/`.
2. Run:
   ```bash
   pip install -r requirements.txt
   jupyter notebook eda.ipynb
   ```
 
---
 
## Visualizations
 
| Chapter | Type | Key Insight |
|---------|------|-------------|
| 01 | Annotated area chart | Nations growth — 2 to 238 with historical triggers |
| 02 | Animated bar chart race | USA rise, Germany dominance, new challengers |
| 03 | Animated choropleth map | World expansion post-1991, click for country details |
| 04 | D3 chord / ribbon diagram | Top 10 rivalry matrix — USA leads 16–2 vs Germany |
| 05 | Stacked area streamgraph | Continental power shift, Europe on top |
| 06 | Dual bar chart | Men vs women prize money — $0 for 24 years |
| 07 | Force-directed bubble chart | Top 1,055 scorers by goals |
| 08 | Radial clock + bar chart | Goal timing — 45′ and 85′+ spikes |
| 09 | Scatter plot | Win rate vs experience — dominance quadrant |
| 10 | Radar + head-to-head | Compare any two nations across 5 dimensions |
 
---
 
## Interactive Features
 
- **Country detail modal** — click any nation on the map for full stats + win history chart
- **Cross-filtering** — map click highlights matching team in scatter and race chart
- **Bar chart race** — play/pause/speed controls, 1956 to 2025
- **World map animation** — year slider or auto-play
- **Head-to-head explorer** — select any two nations for radar + H2H record
- **Story Guide** — floating button with 8 pre-scripted data stories
