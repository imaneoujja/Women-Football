# Project of Data Visualization (COM-480)

| Team members |
|--------------|
| Imane Oujja |

[**Milestone 1**](#milestone-1) • [Milestone 2](#milestone-2) • [Milestone 3](#milestone-3)

## Milestone 1 (20th March, 5pm)

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

We ran a full EDA in our [notebook](../eda.ipynb). Here are the highlights:

The dataset spans 1956–2025 with 11,177 matches. The United States leads all-time with 465 wins, followed by Germany and Sweden. Goals per match have barely declined over time (3.78 in the early era vs 3.51 post-2015), but the biggest blowouts have disappeared — the sport is getting more competitive. The craziest match? Cameroon 2–24 South Africa in 2006.

From the goalscorer data: Birgit Prinz (Germany) tops the charts with 34 recorded goals, ahead of Marta (24) and Abby Wambach (23). 53.6% of goals come in the second half vs 44.9% in the first — late drama is real. 7.6% of goals are penalties.

The shootout data shows a first-shooter win rate of 60.5% (n=38 with data), and 134 shootouts total since 1984. Regional analysis reveals Europe and North America dominating historically, but Asia (Japan, South Korea) and Africa (Nigeria, Cameroon) are catching up in recent decades.

The World Cup grew from 12 teams/510K attendance in 1991 to 32 teams/1.98M in 2023. Prize money was $0 until 2015 — now it's $110M, still just 11% of the men's $1B.

### Related work

The main existing work on this data is a [Towards Data Science article](https://towardsdatascience.com/fifa-womens-world-cup-2023-visualized-with-plotly-a7277edf6278/) that visualized the 2023 World Cup with Plotly — static charts focused on a single tournament. [FCrSTATS](https://github.com/FCrSTATS/StatsBomb_WomensData) used StatsBomb data for radar charts of individual players, but again very narrow. [Flourish](https://flourish.studio/blog/world-cup-euros-football-data-visualization/) published World Cup visualization templates, but they're generic and designed for men's tournaments. The [Deloitte Football Money League](https://www.deloitte.com/uk/en/services/consulting-financial/analysis/deloitte-football-money-league-women.html) publishes beautiful infographics on club revenue but as static PDFs.

What's missing is a project that **connects the big picture (global growth, economics) to the details (goalscorers, match-level patterns)** in one interactive experience. That's what we're building.

Our visual inspiration comes from [The Pudding](https://pudding.cool/) for their narrative scrolling + interactivity approach, [FiveThirtyEight's soccer predictions](https://projects.fivethirtyeight.com/soccer-predictions/) for clean sports dashboards, and the famous [Minard map](https://en.wikipedia.org/wiki/Charles_Joseph_Minard) shown in our course as an example of encoding many variables in a single visual. We haven't used this dataset in any other course.

---

## Milestone 2 (17th April, 5pm)

*10% of the final grade*

## Milestone 3 (29th May, 5pm)

*80% of the final grade*

### Late policy

- < 24h: 80% of the grade for the milestone
- < 48h: 70% of the grade for the milestone
