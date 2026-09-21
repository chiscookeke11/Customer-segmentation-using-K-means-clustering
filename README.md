# Customer Segmentation with K-Means Clustering

This project groups mall customers into behavior-based segments with **K-Means clustering**. The analysis uses each customer's annual income and spending score to identify groups that can support targeted marketing, promotions, and customer-engagement strategies.

The complete workflow is provided in a Jupyter notebook, from loading and checking the data through selecting a cluster count with the elbow method and visualizing the resulting customer groups.

## Project highlights

- Loads and inspects the mall customer dataset.
- Checks the dataset shape, column types, and missing values.
- Clusters customers using **Annual Income (k$)** and **Spending Score (1-100)**.
- Uses within-cluster sum of squares (WCSS) and an elbow plot to compare cluster counts from 1 to 10.
- Fits a reproducible five-cluster K-Means model.
- Visualizes customer groups and their centroids in two dimensions.

## Repository structure

```text
.
├── customer_segmentation_using_K-means_clustering.ipynb  # Analysis and visualizations
├── sample_data/
│   ├── Mall_Customers.csv                                # Customer dataset used by the notebook
│   └── fake_or_real_news.csv                             # Additional sample data; not used by this analysis
└── README.md
```

## Dataset

The notebook reads `sample_data/Mall_Customers.csv`, which contains 200 customer records and the following fields:

| Column | Description | Used for clustering? |
| --- | --- | :---: |
| `CustomerID` | Unique customer identifier. | No |
| `Gender` | Customer-reported gender. | No |
| `Age` | Customer age in years. | No |
| `Annual Income (k$)` | Annual income, measured in thousands of dollars. | Yes |
| `Spending Score (1-100)` | A score representing customer spending behavior. | Yes |

> **Note:** `fake_or_real_news.csv` is included in the repository but is not referenced by the customer-segmentation notebook.

## Methodology

1. Load the customer data with pandas and inspect its structure and missing values.
2. Select `Annual Income (k$)` and `Spending Score (1-100)` as the feature matrix.
3. Fit K-Means models for cluster counts 1 through 10 and record WCSS (`inertia_`) for each model.
4. Review the elbow plot to select **five clusters**.
5. Fit the final model with `KMeans(n_clusters=5, init="k-means++", random_state=0)`.
6. Plot the five groups and the learned cluster centroids.

Cluster labels are numeric identifiers assigned by the algorithm; they do not carry an inherent business ranking. Interpret groups by reviewing their position on the income and spending-score chart.

## Getting started

### Prerequisites

- Python 3.9 or later
- Jupyter Notebook or JupyterLab

### Install dependencies

From the repository root, create and activate a virtual environment (recommended), then install the libraries used by the notebook:

```bash
python -m venv .venv
source .venv/bin/activate  # Windows PowerShell: .venv\Scripts\Activate.ps1
python -m pip install --upgrade pip
python -m pip install jupyter matplotlib numpy pandas scikit-learn seaborn
```

### Run the analysis

Start Jupyter from the repository root so the notebook can find `sample_data/Mall_Customers.csv` using its relative path:

```bash
jupyter notebook
```

Then open `customer_segmentation_using_K-means_clustering.ipynb` and run the cells from top to bottom. In JupyterLab, use `jupyter lab` instead.

## Results

The final visualization places each customer on a chart with:

- **x-axis:** annual income (k$)
- **y-axis:** spending score (1-100)
- **color:** assigned K-Means cluster
- **cyan markers:** learned cluster centroids

These segments provide a starting point for business questions such as which high-income customers have high spending scores, or which groups may respond to different offers. The result is exploratory: it should be validated with additional customer attributes and business context before making production decisions.

## Reproducibility notes

- The elbow-method models use `random_state=42`.
- The final five-cluster model uses `random_state=0`.
- The analysis intentionally uses only two features to make the cluster plot directly interpretable. If you add features, scale them before K-Means and evaluate the new segmentation with appropriate validation metrics.

## License

No license has been specified for this repository. Add a license file before redistributing or reusing the project beyond its intended context.
