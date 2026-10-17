# Let's Fill the Cart! (Instacart Orders Analysis)

An exploratory analysis of grocery orders from **Instacart**, a grocery delivery platform. The project covers the full workflow of a data analysis: reading five related tables, cleaning them and answering business questions about when, how often and what customers buy.

## Main findings

* **When people order:** the peak is at 10 a.m. and the volume stays high until 3 p.m. Sunday is the busiest day and Thursday the quietest.
* **How often they come back:** there are two clear peaks, at 7 days (weekly shoppers) and at 30 days (monthly shoppers, and likely a system cap at 30 days).
* **Wednesday vs. Saturday:** both days have a similar shape, but Saturday has more orders in 16 of the 24 hours (its peak is at 2 p.m., against 3 p.m. on Wednesday).
* **Customers:** most of them placed only one order, and the typical order has between 4 and 7 items.
* **Products:** the most popular and the most reordered items are fresh produce (bananas, strawberries, avocados, spinach), which suggests a healthy shopping profile.
* **A warning about percentages:** reorder rates are close to 100% for niche products and for customers with very few items, but they reflect low volume and not real loyalty.

## Data cleaning

* 15 duplicated orders removed (all of them placed on Wednesday at 2 a.m.), leaving 478,952 orders.
* 1,258 products without a name (all in the aisle and department called `missing`) filled with `'unknown'`.
* Missing values in `add_to_cart_order` (836 rows, all from orders with more than 64 products, which the system cannot position) filled with the flag value 999 and converted to integer.
* Missing values in `days_since_prior_order` kept, because they are the first order of each customer.
* Products registered under more than one ID (104 repeated names) identified and documented.

## Repository structure

```
instacart_project/
├── dataframes/
│   ├── aisles.csv
│   ├── departments.csv
│   ├── instacart_orders.csv
│   ├── order_products.zip
│   └── products.csv
├── instacart_analysis.ipynb
├── README.md
└── requirements.txt
```

## Run locally

```
git clone https://github.com/<your-username>/instacart_project.git
cd instacart_project
python -m venv .venv
.venv\Scripts\activate          # Windows
source .venv/bin/activate       # macOS / Linux
pip install -r requirements.txt
pip install ipykernel           # to run the notebook in VS Code or Jupyter
```

Then open `instacart_analysis.ipynb` and run all cells. The notebook reads the data from the `dataframes/` folder, so it must be opened from the project root. The largest table, `order_products`, is stored zipped (`order_products.zip`, with `order_products.csv` inside, about 90 MB unzipped) to keep the repository light. pandas reads it directly, so there is no need to unzip it. The notebook needs a reasonable amount of free memory to run.

## Tech stack

Python, pandas, Matplotlib, Jupyter Notebook.
