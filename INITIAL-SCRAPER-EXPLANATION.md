# INITIAL SCRAPER EXPLANATION

**Date Accessed:** 2025-05-12

## 📌 Purpose of the Script

The `script.py` file is responsible for scraping the main front-page headline from the Daily Pennsylvanian (https://www.thedp.com). It runs automatically once per day via GitHub Actions and stores results in a JSON file.

---

## 🔍 Code Functionality Summary

```python
def scrape_data_point():
    req = requests.get("https://www.thedp.com")
    loguru.logger.info(f"Request URL: {req.url}")
    loguru.logger.info(f"Request status code: {req.status_code}")

    if req.ok:
        soup = bs4.BeautifulSoup(req.text, "html.parser")
        target_element = soup.find("a", class_="frontpage-link")
        data_point = "" if target_element is None else target_element.text
        loguru.logger.info(f"Data point: {data_point}")
        return data_point
```

### 🔧 How It Works
- **Requests**: Connects to the DP homepage using the `requests` library.
- **Status Check**: Verifies that the request was successful (`req.ok`).
- **Parsing**: Uses BeautifulSoup to parse the page’s HTML.
- **Extraction**: Searches for a tag `<a class="frontpage-link">` and returns its `.text` if found.
- **Logging**: Logs useful debugging information using the `loguru` library.

---

## 📁 Output

If successful, the headline is inserted into a JSON file (`data/daily_pennsylvanian_headlines.json`) under today’s date and timestamp, e.g.:

```json
{
  "2025-05-12": [
    [
      "2025-05-12 13:15PM",
      "Penn women's basketball wins Ivy Madness"
    ]
  ]
}
```

---

## ✅ Verified Outcome

- GitHub Actions triggered successfully ✅  
- Headline extracted and logged ✅  
- Data committed to JSON and pushed by GitHub bot ✅  
