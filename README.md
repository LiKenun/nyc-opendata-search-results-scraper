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

## Sample Output
Here’s the JSON output produced by a sample run of the tool.

    {
        "4k4u-823g": {
            "name": "Water and Sewer Permits",
            "link": "https://data.cityofnewyork.us/Environment/Water-and-Sewer-Permits/4k4u-823g",
            "category": "Environment",
            "type": "Dataset",
            "description": "The DEP Application and Permit data will contain information about the different types of applications approved and permits issued on a regular basis.",
            "tags": [
                "sewer",
                "water",
                "permit"
            ],
            "updated": 1628176338,
            "apiDocLink": "https://dev.socrata.com/foundry/data.cityofnewyork.us/4k4u-823g",
            "dataDownloads": [
                {
                    "contentUrl": "https://data.cityofnewyork.us/api/views/4k4u-823g/rows.csv?accessType=DOWNLOAD",
                    "encodingFormat": "text/csv"
                },
                {
                    "contentUrl": "https://data.cityofnewyork.us/api/views/4k4u-823g/rows.csv?accessType=DOWNLOAD&bom=true&format=true",
                    "encodingFormat": "text/csv"
                },
                {
                    "contentUrl": "https://data.cityofnewyork.us/api/views/4k4u-823g/rows.csv?accessType=DOWNLOAD&bom=true&delimiter=%3B&format=true",
                    "encodingFormat": "text/csv"
                },
                {
                    "contentUrl": "https://data.cityofnewyork.us/api/views/4k4u-823g/rows.json?accessType=DOWNLOAD",
                    "encodingFormat": "application/json"
                },
                {
                    "contentUrl": "https://data.cityofnewyork.us/api/views/4k4u-823g/rows.rdf?accessType=DOWNLOAD",
                    "encodingFormat": "application/rdfxml"
                },
                {
                    "contentUrl": "https://data.cityofnewyork.us/api/views/4k4u-823g/rows.rss?accessType=DOWNLOAD",
                    "encodingFormat": "application/rssxml"
                },
                {
                    "contentUrl": "https://data.cityofnewyork.us/api/views/4k4u-823g/rows.tsv?accessType=DOWNLOAD&bom=true",
                    "encodingFormat": "text/tab-separated-values"
                },
                {
                    "contentUrl": "https://data.cityofnewyork.us/api/views/4k4u-823g/rows.xml?accessType=DOWNLOAD",
                    "encodingFormat": "application/xml"
                }
            ],
            "attachments": {
                "Data_Dictionary-DEP Water and Sewer Permits.xlsx": "https://data.cityofnewyork.us/api/views/4k4u-823g/files/360b70a9-8cd4-4bed-a25d-1987fdc6ba8b?download=true&filename=Data_Dictionary-DEP Water and Sewer Permits.xlsx"
            },
            "columns": [
                {
                    "name": "borough",
                    "type": "number",
                    "humanName": "BOROUGH"
                },
                {
                    "name": "borough_name",
                    "type": "text",
                    "humanName": "Borough Name"
                },
                {
                    "name": "block",
                    "type": "number",
                    "humanName": "BLOCK"
                },
                {
                    "name": "lot",
                    "type": "number",
                    "humanName": "LOT"
                },
                {
                    "name": "zip",
                    "type": "number",
                    "humanName": "ZIP"
                },
                {
                    "name": "serv_order_type",
                    "type": "text",
                    "humanName": "SERV_ORDER_TYPE"
                },
                {
                    "name": "permit_description",
                    "type": "text",
                    "humanName": "Permit Description"
                },
                {
                    "name": "permit_no",
                    "type": "number",
                    "humanName": "PERMIT_NO"
                },
                {
                    "name": "dateissued",
                    "type": "calendar_date",
                    "humanName": "DATEISSUED"
                }
            ]
        },
        "bvug-v3mm": {
            "name": "Clergy Parking Permits",
            "link": "https://data.cityofnewyork.us/Transportation/Clergy-Parking-Permits/bvug-v3mm",
            "category": "Transportation",
            "type": "Dataset",
            "description": "Issued to members of the clergy for parking their personal passenger vehicles when conducting ministerial duties at their houses of worship, funeral establishments or hospitals. Allows parking for up to five hours in No Parking Zones adjacent to their houses of worship, four hours adjacent to a funeral home and up to three hours adjacent to hospitals.",
            "tags": [
                "permit",
                "parking",
                "clergy",
                "application"
            ],
            "updated": 1630667413,
            "apiDocLink": "https://dev.socrata.com/foundry/data.cityofnewyork.us/bvug-v3mm",
            "dataDownloads": [
                {
                    "contentUrl": "https://data.cityofnewyork.us/api/views/bvug-v3mm/rows.csv?accessType=DOWNLOAD",
                    "encodingFormat": "text/csv"
                },
                {
                    "contentUrl": "https://data.cityofnewyork.us/api/views/bvug-v3mm/rows.csv?accessType=DOWNLOAD&bom=true&format=true",
                    "encodingFormat": "text/csv"
                },
                {
                    "contentUrl": "https://data.cityofnewyork.us/api/views/bvug-v3mm/rows.csv?accessType=DOWNLOAD&bom=true&delimiter=%3B&format=true",
                    "encodingFormat": "text/csv"
                },
                {
                    "contentUrl": "https://data.cityofnewyork.us/api/geospatial/bvug-v3mm?method=export&format=GeoJSON",
                    "encodingFormat": "text/csv"
                },
                {
                    "contentUrl": "https://data.cityofnewyork.us/api/geospatial/bvug-v3mm?method=export&format=KML",
                    "encodingFormat": "text/csv"
                },
                {
                    "contentUrl": "https://data.cityofnewyork.us/api/geospatial/bvug-v3mm?method=export&format=KMZ",
                    "encodingFormat": "text/csv"
                },
                {
                    "contentUrl": "https://data.cityofnewyork.us/api/views/bvug-v3mm/rows.rdf?accessType=DOWNLOAD",
                    "encodingFormat": "application/rdfxml"
                },
                {
                    "contentUrl": "https://data.cityofnewyork.us/api/views/bvug-v3mm/rows.rss?accessType=DOWNLOAD",
                    "encodingFormat": "application/rssxml"
                },
                {
                    "contentUrl": "https://data.cityofnewyork.us/api/geospatial/bvug-v3mm?method=export&format=Shapefile",
                    "encodingFormat": "text/csv"
                },
                {
                    "contentUrl": "https://data.cityofnewyork.us/api/views/bvug-v3mm/rows.tsv?accessType=DOWNLOAD&bom=true",
                    "encodingFormat": "text/tab-separated-values"
                },
                {
                    "contentUrl": "https://data.cityofnewyork.us/api/views/bvug-v3mm/rows.xml?accessType=DOWNLOAD",
                    "encodingFormat": "application/xml"
                }
            ],
            "attachments": {
                "Clergy_Parking_Permits_Open_Data_Dictionary.xlsx": "https://data.cityofnewyork.us/api/views/bvug-v3mm/files/99c419c0-9f3c-4403-bd0b-1ad7b5bab9ed?download=true&filename=Clergy_Parking_Permits_Open_Data_Dictionary.xlsx"
            },
            "columns": [
                {
                    "name": "houseofworship",
                    "type": "text",
                    "humanName": "HouseOfWorship"
                },
                {
                    "name": "streetaddress",
                    "type": "text",
                    "humanName": "StreetAddress"
                },
                {
                    "name": "city",
                    "type": "text",
                    "humanName": "City"
                },
                {
                    "name": "state",
                    "type": "text",
                    "humanName": "State"
                },
                {
                    "name": "postcode",
                    "type": "text",
                    "humanName": "Postcode"
                },
                {
                    "name": "entrydate",
                    "type": "calendar_date",
                    "humanName": "EntryDate"
                },
                {
                    "name": "permitnumber",
                    "type": "text",
                    "humanName": "PermitNumber"
                },
                {
                    "name": "dateissue",
                    "type": "calendar_date",
                    "humanName": "DateIssue"
                },
                {
                    "name": "dateexpiry",
                    "type": "calendar_date",
                    "humanName": "DateExpiry"
                },
                {
                    "name": "permitstatus",
                    "type": "text",
                    "humanName": "PermitStatus"
                },
                {
                    "name": "permittype",
                    "type": "text",
                    "humanName": "PermitType"
                },
                {
                    "name": "borough",
                    "type": "text",
                    "humanName": "Borough"
                },
                {
                    "name": "latitude",
                    "type": "number",
                    "humanName": "Latitude"
                },
                {
                    "name": "longitude",
                    "type": "number",
                    "humanName": "Longitude"
                },
                {
                    "name": "community_board",
                    "type": "number",
                    "humanName": "Community Board"
                },
                {
                    "name": "council_district",
                    "type": "number",
                    "humanName": "Council District"
                },
                {
                    "name": "census_tract",
                    "type": "number",
                    "humanName": "Census Tract"
                },
                {
                    "name": "bin",
                    "type": "number",
                    "humanName": "BIN"
                },
                {
                    "name": "bbl",
                    "type": "number",
                    "humanName": "BBL"
                },
                {
                    "name": "nta",
                    "type": "text",
                    "humanName": "NTA"
                },
                {
                    "name": "geocoded_column",
                    "type": "point",
                    "humanName": "Location"
                }
            ]
        }
    }