# NYC OpenData Search Results Scraper
This tool scrapes the search results page(s) of NYC OpenData’s website and then visits each item’s page to retrieve additional details such as the download links for the data set or any attachments related to it.

## How to Use
The notebook is divided into several cells, the first of which provides the functions used by the rest of the notebook. Set the URL to the results page you want to scrape. Then run the cells in order. The second cell extracts search results, the third one extracts additional details about each result, and the fourth saves the scraped data into a pickle file.

### Getting the Search Results
It extracts the data from the first results page and all subsequent pages until it cannot find a link to the following page. For each page, it looks for the result elements and maps each one to a dictionary. The dictionary schema is as follows:
* **name** (string): the name of the item
* **link** (string): the link to the page with more information about the item
* **category** (string): the category of the item (e.g., *Education*)
* **type** (string): the type of the item (e.g., *Dataset*)
* **description** (string): a description of the item
* **tags** (set of strings): a set of tags associated with the item
* **updated** (integer): the UNIX timestamp which this item was last updated
* **apiDocLink** (string): a link to the API documentation (which might possibly be used to extract more metadata about the item)

## Getting the Data Set Details
It extracts additional information about the items using the links to the items’ pages. It adds the following keys if the information is available:
* **attachments** (dict of strings): key-value pairs of file names and their corresponding links to download them
* **columns** (list of dicts): an ordered list of dicts representing column metadata
* **dataDownloads** (list of dicts of strings): a list of key-value pairs where the key is the file name and the value is the link to its URL

In the case where download of data set details is interrupted, run the cell again and the code will attempt to resume progress. Simply, it checks each item for the existence of the additional dictionary keys. If they don’t exist, the code tries to retrieve them again and amends the dictionary with any additional information it finds.

## Missing Libraries?
This notebook was developed on Google’s Colaboratory platform. Your environment may not have the same libraries preinstalled. If any of the `import` statements fail, you are probably missing some libraries.

### BeautifulSoup
This library is for parsing HTML code, obiviating the need for unwiedly/fragile regular expressions. Much of the information can be gleaned from the HTML alone.

If you get an error at the `import bs4` line, then you will need to grab the BeautifulSoup library for your Python environment. You can install that using `pip install beautifulsoup4`. Detailed instructions here: https://beautiful-soup-4.readthedocs.io/en/latest/#installing-beautiful-soup

### Esprima
This library is for parsing JavaScript code.

If you get an error at the `import esprima` line, then you will need to grab the Esprima library for your Python environment. You can install that using `pip install esprima`.
