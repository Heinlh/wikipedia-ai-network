# Wikipedia AI concept network

**Question:** Which concepts are foundational in Wikipedia's coverage of artificial intelligence, and how do the topics group together?

`wikipedia_ai_network.ipynb` builds a directed network of 310 English Wikipedia articles about AI and machine learning, collected on September 23, 2026. A node is one article; an edge is a hyperlink from one article's **body text** to another article in the set. Links from navigation boxes, infoboxes, and reference sections are excluded, because a navigation box links every article it contains to every other one. Articles are ranked by PageRank (primary) and in-degree (secondary), and grouped with Louvain community detection.

## Run the notebook

1. Install the packages with `python -m pip install -r requirements.txt`.
2. Open `wikipedia_ai_network.ipynb` in Jupyter or VS Code with Python notebook support (installed separately).
3. Use this project directory as the working directory and run all cells from top to bottom.

The default setting, `REFRESH_DATA = False`, replays the saved API responses in `data/raw/` and makes no network calls. Set `REFRESH_DATA = True` for a live collection; this needs internet access, takes several minutes, and rewrites the cache. Wikipedia changes daily, so a fresh pull will give different numbers — after refreshing, update the dated Markdown, the findings, the iteration log, and the manual edge review before sharing the analysis.

## Folder layout

| Path | Contents |
|---|---|
| `wikipedia_ai_network.ipynb` | The analysis, with collection and cleaning code |
| `data/raw/` | Every raw MediaWiki API response, gzipped JSON, one file per request |
| `data/iteration_log.csv` | The four collect → clean → check iterations and their metrics |
| `data/nodes.csv` | Final nodes with PageRank, in/out-degree, betweenness, community, primary seed |
| `data/edges.csv` | Final directed edges, with a flag for links from "See also" |
| `figures/network_clusters.png` |  The clustered network |
| `figures/top20_pagerank.png` | The top 20 concepts by PageRank |
| `requirements.txt` | Python packages |

