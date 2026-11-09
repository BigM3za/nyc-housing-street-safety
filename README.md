# Homes on Dangerous Streets?
### Affordable housing and serious traffic crashes in New York City (2022–2025)

**Data Engineering and Visualization, Winter Semester 2026: Project Milestone 1**
German International University, Faculty of Informatics and Computer Science

| | Link |
|---|---|
| Live website | [nyc-housing-street-safety-dun.vercel.app](https://nyc-housing-street-safety-dun.vercel.app) |
| Repository | [github.com/BigM3za/nyc-housing-street-safety](https://github.com/BigM3za/nyc-housing-street-safety) |
| Notebook | [`Milestone1_Housing_x_StreetSafety.ipynb`](Milestone1_Housing_x_StreetSafety.ipynb) |
| Housing dataset | [Affordable Housing Production by Building (HPD)](https://data.cityofnewyork.us/d/hg8x-zxpr), catalog H2 |
| Transportation dataset | [Serious Injury Response, Tracking & Analysis Program, SIRTA (DOT)](https://data.cityofnewyork.us/d/xeqp-qz8h), catalog T4 |

## Team

| Role | Name | ID | GitHub |
|---|---|---|---|
| M1: Lead & Integration | Mohamed Reyad | 16010224 | [MidoReyad](https://github.com/MidoReyad) |
| M2: Housing data | Ziad Mohamed | 16006210 | [ziadMohamed16006210](https://github.com/ziadMohamed16006210) |
| M3: Transport data | Mohamed Said | 16009603 | [mohamedsayed16009603](https://github.com/mohamedsayed16009603) |
| M4: Website logic | Mohamed Nasr | 16003436 | [MohamedAhmedNasr](https://github.com/MohamedAhmedNasr) |
| M5: Website visuals & deployment | Eyad Nada | 16003427 | [EyadNada](https://github.com/EyadNada) |
| M6: Story & documentation | Mazen Osama | 16007545 | [BigM3za](https://github.com/BigM3za) |

## The question and the answer in short

New York City delivers about 25,000 affordable homes a year. **Are they being placed next to the city's most dangerous streets?**

- **Yes, in the same places.** ZIP codes with more new affordable units have more serious crashes (rank correlation 0.61). 26 "double hotspot" ZIPs (14% of ZIPs) received 43% of all new affordable units.
- **The newest and poorest residents are the most exposed.** New-construction buildings sit in ZIPs with 28% more serious crashes than preserved buildings.
- **The danger is on local streets** (96% of serious crashes near new homes), so it can be fixed with tools DOT already uses.
- **The buildings are not making it worse.** Crashes did not rise with completions, and the year after a building opened was slightly safer.

All results are **associations, not causes**. See Section 12 of the notebook for the full story and limitations.

## Repository structure

```
Milestone1_Housing_x_StreetSafety.ipynb   the full analysis (EDA, cleaning, integration, 12 research questions, story)
notebook_src/                             the notebook as plain Python files (easier to review; build_notebook.sh rebuilds it)
data/raw/                                 raw snapshots downloaded from the NYC Open Data API (9 Oct 2026)
data/clean/                               clean tables written by the notebook (Section 11) and read by the website
app.py                                    the Dash website: layout and callbacks
dashboard/data.py                         loading, filtering and aggregating the clean tables
dashboard/figures.py                      the Plotly charts
dashboard/search.py                       the search box: turns text into filters
dashboard/story.py                        text of the Story tab
assets/style.css                          website style (Dash loads it automatically)
reports/                                  automated EDA reports (ydata-profiling, Sweetviz)
tests/                                    unit tests and an end-to-end browser test
docs/prompts_log.md                       every AI prompt we used
requirements.txt                          packages for the website (local run and Render)
requirements-notebook.txt                 packages for running the notebook locally
pyproject.toml, uv.lock, .python-version  packages and Python version for the Vercel deployment
render.yaml                               settings for the alternative Render deployment
```

## How to run the notebook

**Google Colab (recommended):** open the notebook from GitHub in Colab (File → Open notebook → GitHub tab, paste the repository URL), then **Runtime → Run all**. On the first run it downloads both datasets from the API. Colab already has every package we use.

**Locally:**
```bash
pip install -r requirements-notebook.txt
jupyter notebook Milestone1_Housing_x_StreetSafety.ipynb
```
The notebook uses the saved snapshot in `data/raw/`, so the numbers match our text. Set `REFRESH_FROM_API = True` in Section 2 to download fresh data.

## How to run the website locally

```bash
pip install -r requirements.txt
python app.py
```
Then open http://127.0.0.1:8050.

### What the website does
- **Five filters:** borough, years, construction type (housing), crash severity and street type (transportation).
- **Search mode:** type, for example, `Brooklyn 2023 new buildings fatal`, `the bronx 2022-2024 preservation` or a ZIP code like `10453`. The words override the matching filters, and the page shows what the search understood.
- **Generate Report:** charts change **only** when this button is clicked (or Enter is pressed in the search box). The filters are read as Dash `State`, and the button is the only `Input`. Every chart then reads the same stored filters, so they always update together.
- **Charts:** a cross-domain map (crash density + ZIP circles by hotspot group), a ZIP scatter plot (housing vs crashes), yearly trends, a time-of-day heatmap, local vs highway crashes, danger by income band, and a priority ranking.
- **Drill-through:** click a ZIP on the map, the scatter plot or the ranking (or search for it) to open its detail panel.
- **Story tab:** the question, the findings, three recommendations and the limitations.

## How to deploy on Vercel (free, what we used)

1. Push this repository to GitHub.
2. Sign in to [vercel.com](https://vercel.com) with GitHub, click **Add New → Project**, and import this repository.
3. Keep the default settings and click **Deploy**. Vercel finds `app.py`, installs the packages listed in `pyproject.toml` (locked in `uv.lock`) and runs `app`, the Flask server that Dash is built on (`app = server` in `app.py`), as a serverless function.
4. Open the `vercel.app` link and test every filter, the search box and the Generate Report button.
5. Every new commit on `main` is deployed again automatically.

**Notes:**
- `.python-version` and `pyproject.toml` pin Python 3.12.
- The first visit after a quiet period takes a few seconds longer (cold start), because the function loads the clean tables again.
- The website reads only the small clean tables (`data/clean/`), not the raw data, so it fits easily in a serverless function.

### Alternative: Render (free)

1. On [render.com](https://render.com), sign in with GitHub and click **New + → Blueprint**, choose this repository, and confirm. Render reads `render.yaml`.
   *(Or **New + → Web Service**: Build Command `pip install -r requirements.txt`, Start Command `gunicorn app:server --workers 1 --threads 4 --timeout 120`, Instance type **Free**.)*
2. A free Render service sleeps after 15 minutes without visitors; the next visit takes about a minute to load.

## Tests

```bash
pip install pytest playwright
pytest tests/test_search.py tests/test_data.py         # search parser and website numbers
python app.py &                                          # then, in another terminal:
python tests/browser_check.py                            # end-to-end: filters, search, Generate Report, ZIP panel, reset
```

## Team contributions

| Member | Research questions | Cleaning & integration | Website | Documentation |
|---|---|---|---|---|
| M1: Lead & Integration | RQ1, RQ2 | Extract, integration, post-integration cleaning | Data loading (`dashboard/data.py`) | Repository structure |
| M2: Housing data | RQ3, RQ4 | Housing EDA and cleaning | Housing filters | Housing markdown cells |
| M3: Transport data | RQ5, RQ6 | Crash EDA, cleaning and ZIP imputation | Crash filters | Crash markdown cells |
| M4: Website logic | RQ7, RQ8 | Load step | Callbacks, search parser, Generate Report button | Website section of this README, GitHub upload |
| M5: Website visuals & deployment | RQ9, RQ10 | Chart style and colours | Layout, charts, map, Vercel deployment | Deployment guide |
| M6: Story & documentation | RQ11, RQ12 | Cleaning verification | Story tab | Story, README, prompts log, GitHub upload, final check |

## Use of AI

We didn't use AI. نوقطة 

