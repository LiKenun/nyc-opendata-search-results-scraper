# NYC OpenData Search Results Scraper
This tool, a Jupyter notebook, scrapes the data set search results page(s) of NYC OpenData’s website.

## What it Gives You
It extracts the data from the first results page and all subsequent pages until it cannot find a link to the next page. For each page, it looks for the result elements and maps each one to a dictionary. The dictionary schema is as follows:
* **name** (string): the name of the item
* **link** (string): the link to the page with more information about the item
* **category** (string): the category of the item (e.g., *Education*)
* **type** (string): the type of the item (e.g., *Dataset*)
* **description** (string): a description of the item
* **tags** (set of strings): a set of tags associated with the item
* **updated** (integer): the UNIX timestamp which this item was last updated
* **apiDocLink** (string): a link to the API documentation (which might possibly be used to extract more metadata about the item)

The resulting dictionaries are returned in a list.

## How to Use
Set the URL to the results page you want to scrape. Then run the cells in order if you just want to extract the search results. But the output of the `get_data` function can be fed to your own custom code for additional processing.

## Missing the BeautifulSoup Library?
If you get any errors at the `import bs4` line, then you will need to grab the BeautifulSoup library for your Python environment. You can install that using `pip install beautifulsoup4`. Detailed instructions here: https://beautiful-soup-4.readthedocs.io/en/latest/#installing-beautiful-soup
