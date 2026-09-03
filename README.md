# Amazon Product Scraper

A simple Python scraper that crawls an Amazon search results page, follows every product link, and extracts key product details into a CSV file.

## Features

- Scrapes product **title**, **price**, **rating**, and **image URL**
- Walks paginated search results automatically (follows the "Next" button)
- Avoids re-scraping duplicate product URLs
- Exports all collected data to `laptops.csv` via pandas

## Requirements

- Python 3.8+
- Dependencies:
  ```bash
  pip install requests beautifulsoup4 lxml pandas
  ```

## Usage

1. Open `scraper.py` and set the `search_url` variable in `main()` to the Amazon search/listing page you want to scrape:
   ```python
   search_url = "https://www.amazon.com/s?k=laptops"
   ```
2. Run the script:
   ```bash
   python scraper.py
   ```
3. Results are saved to `laptops.csv` in the same directory.

## Output Columns

| Column | Description                          |
|--------|---------------------------------------|
| title  | Product name                          |
| price  | Product price (float, or "No price listed") |
| rating | Star rating (e.g. "4.5")              |
| image  | Main product image URL                |
| url    | Product page URL                      |


## Legal Note

Scraping Amazon may violate its Terms of Service. Use responsibly, respect `robots.txt`, and consider using the [Amazon Product Advertising API](https://webservices.amazon.com/paapi5/documentation/) for production use cases.
