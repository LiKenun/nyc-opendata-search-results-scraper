# NYC OpenData Scraper and Clusterer
This project consists of two Jupyter notebook tools: the data set metadata scraper which scrapes the search results page(s) of NYC OpenData’s website and then visits each item’s page to retrieve additional metadata; and the clusterer which analyzes the output of the scraper to group similar data sets.

This is an ongoing project, and one while the metadata scraper is practically final the clusterer is still being developed. Currently, it’s limited to clustering by name, although there is a lot of additional metadata to consider for the clustering process.

## How to Use
Each of the notebooks are divided into several cells with embedded instructions. In general they are run from top to bottom in sequential order.

Use the scraper to get the data sets’ metadata and feed the output of that tool to the clusterer. Both tools work with a common JSON format.

### Metadata Collected

* name (string): the name of the item
* link (string): the link to the page with more information about the item
* category (string): the category of the item (e.g., Education)
* type (string): the type of the item (e.g., Dataset)
* description (string): a description of the item
* tags (list of strings): a set of tags associated with the item
* updated (string): the timestamp which this item was last updated
* updateFrequency (string): the frequency the data set is updated if not Historical Data
* apiDocLink (string): a link to the API documentation
* columns: a list of columns and their properties
    * name (string): the name of the column
    * humanName (string): a human-friendly name for the column
    * type (string): the column type (one of: calendar_date, checkbox, location, number, point, text, or url)
    * nullCount (number): the count of null values for the column
    * nonNullCount (number): the count of non-null values for the column
    * largest: the largest value for the column
    * smallest: the smallest value for the column
    * top (list): a list of the top values for the column
* attachments: a list of downloadable files—most often spreadsheets or PDFs—that describe the data in more detail
* dataDownloads: a list of downloadable files containing all of the data in different formats

## Library Requirements
This notebook was developed on Google’s Colaboratory platform. Your environment may not have the same libraries preinstalled. If any of the `import` statements fail, you are probably missing some libraries. You can grab the necessary libraries using `!pip install ` within the notebook *before* running any other cells.

* `beautifulsoup4` for parsing HTML code, obiviating the need for unwiedly/fragile regular expressions
* `esprima` for parsing JavaScript code
* `nltk` for the part of speech (POS) tagger and lemmatizer which are needed to simplify the words in the data set names to their most basic forms as well as an edit distance function
* `numpy` for `pandas` and `scikit-learn`
* `pandas` for HTML table output instead of `print`ing
* `scikit-learn` for the clustering algorithm
* `scipy` for `scikit-learn`
