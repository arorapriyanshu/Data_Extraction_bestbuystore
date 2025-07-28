

# Best Buy Store Locator Scraper

This Python script uses Selenium to automate extraction of Best Buy store details for a given ZIP code from the [Best Buy Store Locator](https://www.bestbuy.com/site/store-locator), then saves the results to a CSV file with a single, combined address column.

## Features

- **Automates Best Buy web search by ZIP code**
- Handles initial page reload quirks
- Handles random pop-ups with scroll-into-view and delay logic
- Extracts:
  - Store Name
  - Distance
  - Full Address (single column, combined from all address fields)
  - Store Details URL
  - Hours
- Outputs to `bestbuy_store_results.csv`
- Slow, robust `time.sleep(7)` waits for maximum reliability

## Requirements

- Python 3.7+
- [Selenium](https://pypi.org/project/selenium/)
- Google Chrome browser
- ChromeDriver (version must match your installed Chrome)
    - [Download ChromeDriver](https://chromedriver.chromium.org/downloads)

### Install required Python packages:

```bash
pip install selenium
```

## Usage

1. **Clone or download this script.**

2. Edit the script if you need:
   - A different ZIP code (change the value in `zip_input.send_keys("10001")`)

3. Run the script:
   ```bash
   python bestbuy_store_scraper.py
   ```

4. **Result:**  
   When finished, a file called `bestbuy_store_results.csv` will be created in the same folder with store data.

## Script Logic Overview

1. Opens the Best Buy store locator in Chrome.
2. Refreshes the page to bypass any initial error messages.
3. Waits for and fills in the ZIP code field.
4. Scrolls the "Update" button into view and clicks it.
5. Waits for results, then scrapes all store cards in the results section.
6. Concatenates address fields into a single column ("address").
7. Saves all data as rows in a CSV file.

## CSV Columns

- `name` — Store Name
- `distance` — Approximate distance from the search ZIP code
- `address` — Full, single-column address
- `details_url` — Link to the specific Best Buy store page
- `hours` — Today's hours/open status

## Troubleshooting

- The script uses `time.sleep(7)` between steps for reliability. If your internet is slower or the website delays content, increase the wait times.
- **Pop-ups:** Script is robust with scrolling but some random overlays/popups may still interfere. If scraping fails, try rerunning.
- **Element errors:** Make sure your ChromeDriver and Chrome browser versions are compatible.
- If you need headless mode (no browser UI), add:
  ```python
  options.add_argument('--headless')
  options.add_argument('--window-size=1920,1080')
  ```

## License

MIT License (or your company’s preferred license)

## Author

- Your Name / Company (optional)

## Appendix

### Changing ZIP Code

To change the ZIP code, edit:
```python
zip_input.send_keys("YOUR_ZIP_HERE")
```

### Output Example

| name              | distance   | address                             | details_url                        | hours           |
|-------------------|------------|-------------------------------------|-------------------------------------|-----------------|
| Union Square      | 0.7 miles  | 52 E 14th St, New York, NY 10003    | https://stores.bestbuy.com/2717     | Open until 8 pm |
| Chelsea           | 1.2 miles  | 60 W 23rd St, New York, NY 10010    | https://stores.bestbuy.com/482      | Open until 8 pm |
