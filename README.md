# arXiv Paper Scraper - Lab 1

## Description
This project scrapes arXiv papers programmatically, downloading full-text source files (TeX), metadata, and references for a specified range of paper IDs.

## Installation

### Requirements
- Python 3.8 or higher
- pip package manager

### Install Dependencies

```bash
pip install arxiv requests pandas tqdm psutil
```

**Note:** `psutil` is required for memory and disk usage tracking in enhanced metrics.

## Usage

### Standard Mode (Basic Statistics)

1. Open `lab1.ipynb` in Jupyter Notebook or JupyterLab
2. Configure the scraping range in Cell 1:
   - `START_MONTH`: Start month (e.g., "2023-09")
   - `START_ID`: Start paper ID (e.g., "2848")
   - `END_MONTH`: End month (e.g., "2023-09")
   - `END_ID`: End paper ID (e.g., "7847")
3. Run all cells in order (Cell 0 → Cell 6)

### Enhanced Metrics Mode (Detailed Performance Analysis)

For comprehensive performance metrics including memory usage, disk storage, and per-paper timing:

1. Run Cells 0-5 as usual
2. In Cell 7, uncomment the last line:
   ```python
   enhanced_report = scrape_with_enhanced_metrics()
   ```
3. Run Cell 7

This will generate `23127388_detailed_report.json` with all performance metrics.

### Resuming After Interruption

If scraping is interrupted (network loss, system shutdown):

1. Check the last successfully scraped paper ID in the `data/23127388/` folder
2. Update `START_ID` in Cell 1 to the next paper ID
3. Re-run from Cell 1 onwards

**Note:** Network connection is **required** throughout the scraping process as the code uses:
- arXiv API for downloading papers
- Semantic Scholar API for extracting references

If network is lost, the script will fail and must be resumed manually.

## Output Structure

### Data Files

```
data/
├── 23127388/                              # Student ID folder
│   ├── 2309-02848/                        # Paper folder (yyyymm-id)
│   │   ├── metadata.json                  # Paper metadata
│   │   ├── references.json                # References (arXiv IDs only)
│   │   └── tex/                           # TeX source files
│   │       ├── 2309-02848v1/              # Version 1
│   │       │   ├── *.tex files            # Only .tex files
│   │       │   └── Figures/ (empty)       # Empty folders preserved
│   │       └── 2309-02848v2/              # Version 2
│   ├── 2309-02849/
│   └── ...
└── 23127388_detailed_report.json          # Performance metrics (if using enhanced mode)
```

### Report Files

**23127388_detailed_report.json** (Enhanced metrics mode only):
- **Scraping Summary**: Total papers, success rate, failed IDs
- **Timing Metrics**: 
  - Total duration
  - Entry discovery time
  - Average/min/max time per paper
- **Storage Metrics**:
  - Paper sizes before/after cleanup
  - Storage saved percentage
  - Final output size
- **Memory Metrics**:
  - Initial/final/max/average RAM usage
  - Memory increase during scraping
- **Reference Metrics**:
  - Total references collected
  - Average references per paper
  - Min/max references

## Features

- Downloads all versions of each paper (v1, v2, v3, etc.)
- Extracts metadata from arXiv API
- Crawls references from Semantic Scholar API (only papers with arXiv IDs)
- Keeps only .tex files and empty folders
- Removes images and auxiliary files to save space
- Rate limiting to avoid API bans

## Student Information

- Student ID: 23127388
- Course: Introduction to Data Science

