# Wikipedia AI Concept Network

**Question:** Which AI concepts are most central to Wikipedia's coverage of artificial intelligence, and how do they group into topics?

`wikipedia_ai_network.ipynb` builds a directed network of English Wikipedia articles related to AI and machine learning. A node represents one Wikipedia article, and a directed edge represents a hyperlink from one article's body text to another article in the network.

Links from navigation boxes, infoboxes, references, and other page elements are excluded so that the network focuses on links placed within article content.

Articles are analyzed using:

* **PageRank** as the primary measure of centrality
* **In-degree** as a secondary measure of centrality
* **Betweenness centrality** to identify concepts that connect different parts of the network
* **Louvain community detection** to identify groups of closely connected AI topics

The analysis used for the published findings was collected on **September 23, 2026** and resulted in a network of **310 articles and 2,369 directed edges**.

## Running the notebook

### 1. Clone the repository

```bash
git clone https://github.com/Heinlh/wikipedia-ai-network.git
cd wikipedia-ai-network
```

### 2. Install the required packages

```bash
python -m pip install -r requirements.txt
```

You will also need Jupyter Notebook, JupyterLab, or an editor such as VS Code with Python notebook support.

### 3. Enable data collection before the first run

The repository does **not** include the cached Wikipedia API responses used on my machine.

Before running the notebook for the first time, open `wikipedia_ai_network.ipynb` and change:

```python
REFRESH_DATA = False
```

to:

```python
REFRESH_DATA = True
```

This tells the notebook to collect the required data directly from the MediaWiki API and create a local cache under `data/raw/`.

An internet connection is required for this first run, and collecting the data may take several minutes.

### 4. Run the notebook

Run all cells from top to bottom while using the repository root as the working directory.

After the first successful run, the API responses will be cached locally. You can then change:

```python
REFRESH_DATA = True
```

back to:

```python
REFRESH_DATA = False
```

for future runs. This allows the notebook to reuse your locally cached responses without making new API requests.

## Reproducibility note

The results on a fresh run may differ from the results reported in this repository.

Wikipedia is continuously edited. Articles can be added, removed, renamed, expanded, redirected, or updated with new hyperlinks. Because `REFRESH_DATA = True` collects the current version of Wikipedia, a later run may produce a different number of nodes, edges, PageRank scores, community assignments, or rankings.

The findings in this repository are based on the Wikipedia snapshot I collected on **September 23, 2026**. The published results from that run contained:

* **310 nodes**
* **2,369 directed edges**
* Machine learning as the highest-ranked article by PageRank
* Six substantive topic communities identified using Louvain community detection

A fresh run should therefore be treated as a new snapshot of the Wikipedia AI network rather than an exact reproduction of the September 23, 2026 results.

## Folder layout

| Path                           | Contents                                                                                 |
| ------------------------------ | ---------------------------------------------------------------------------------------- |
| `wikipedia_ai_network.ipynb`   | Main data collection, cleaning, network analysis, validation, and visualization notebook |
| `findings.md`                  | Written summary of the analysis and findings                                             |
| `data/raw/`                    | Locally generated cached MediaWiki API responses                                         |
| `data/nodes.csv`               | Final node-level results, including centrality and community metrics                     |
| `data/edges.csv`               | Final directed hyperlink edges                                                           |
| `figures/network_clusters.png` | Wikipedia AI network visualization grouped by community                                  |
| `figures/top20_pagerank.png`   | Top 20 AI concepts ranked by PageRank                                                    |
| `requirements.txt`             | Required Python packages                                                                 |

## Findings

See [`findings.md`](findings.md) for the complete analysis, interpretation, limitations, and stakeholder recommendations.

## Data source

The data is collected from English Wikipedia using the [MediaWiki Action API](https://www.mediawiki.org/wiki/API:Main_page).

The analysis uses Wikipedia's hyperlink structure as a measure of how AI concepts are connected. These links reflect editorial choices and should not be interpreted as verified learning prerequisites or measures of audience demand.
