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

## Known Issues / TODO

This script has a few bugs that need fixing before it will run:

- **`sum`/`counter` not tracked properly** — `get_product_info` references `sum` and `counter` but never declares them `global`, so it will raise an `UnboundLocalError`. Consider computing the average from the returned DataFrame in `main()` instead.
- **Invalid syntax in `parse_listing`** — the line `Recursively check the next page` is a stray comment missing its `#`, which will cause a `SyntaxError`.
- **Commented-out description field** — the `description` key is left in the returned dict as a triple-quoted string literal, which will break the dictionary. Either implement the description scrape or remove the line entirely.
- **No rate limiting** — the scraper sends requests back-to-back with no delay, which risks triggering Amazon's bot detection or getting your IP blocked. Consider adding `time.sleep()` between requests.
- **No error handling around `requests.get`** — network failures or timeouts will crash the script.
- **Empty `search_url`** — must be set before running.

## Legal Note

Scraping Amazon may violate its Terms of Service. Use responsibly, respect `robots.txt`, and consider using the [Amazon Product Advertising API](https://webservices.amazon.com/paapi5/documentation/) for production use cases.
