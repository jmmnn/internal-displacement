
### Raw Data
We already have certain datasets containing URLs.

__Activities:__
- *Do we want to obtain more urls for our own dev / testing?*

### Scraping
To be moved to `info-sources` repo. Interested parties can contribute there.

Also covers the following two points from Filtering:
- Identify language of a document (English vs. not English)
- Broken URLs

__Activities:__
- Maintain some sort of link to `info-sources` to understand how these tools can be used / fit into the `internal-displacement` pipeline,  
i.e., function arguments, what they return, API type stuff.

### Pipeline
Controls the input and output of data with respect to scraping and interpreting articles.

__Activities__
- Define how to export / store articles (discussion):
    + CSVs for now, but likely some sort of database will be necessary to facilitate the online / interactive tool for modeling and analysis
- Take new data and extract only URLs, converting them into list
- Checks and keeps a log of all previously scraped URLs
- Checks whether a URL is from a domain on an RSS whitelist (future)
- Manages output from scraper and either appends to original database or creates new database

(please see [#86](https://github.com/Data4Democracy/internal-displacement/issues/86))

### Filtering (Interpreter)
The third filtering requirement is more specific to the `internal-displacement` domain:

- Filtering out documents not reporting on human mobility (binary classification)

__Activities:__
- Implement filtering out of documents not reporting on human mobility (modeling)

> @milanoleonardo: *'this can be done by looking at the dependency trees of the sentences in the text to make sure there is a link between a “reporting term” and a “reporting unit” (see challenge for details). This would definitely remove all documents reporting on “hip displacement” or sentences like “displaced the body of people” etc.'*

*How to test this functionality? Build some hand-crafted examples of things that shouldn't be included?*

### Tagging (Interpreter)

- Classification of documents into 3 classes (Disasters, Conflict & Violence, Other)

__Activities:__
- Select approach / model that will allow for online learning or re-training in the future with new datasets. (discussion)
- Build and train classifier for classifiying into the 3 required classes. (modeling)

> @milanoleonardo: *'the best would be to set a fixed threshold on the probability distribution and assign a tag based on the content of the document.'*

### NLP

"Fact extraction" from documents:
- Publication date, locaction (ISO 3166 country codes) , reporting term, reporting units etc.

__Activities:__
- Select NLP tool or framework (discussion)
- Build and test working tool for extracting facts (modeling)

### Article Class

__Activities:__
- Define the properties each Article needs to have and fill out code for instantiating new Articles (beginner friendly)
- Create / fill-out functions for update articles properties by calling and using return values from Scraper and Interpreter functions (beginner friendly)
- Fill out function for saving articles along with relevant properties (beginner friendly)

### Visualization

Including but not limited to Interactive Map, Histograms

__Activities:__
- Design of visualizations (data-viz)
- Selection of tool for online visualizations (i.e. D3) (discussion)
- Create visualization functions that take in data in standard format and produce desired and interactive visualizations (data-viz)

### Quantitative Analysis

Online tool that allows analysts to interact directly with data, choose what they visualize and how etc.

__Activities:__
- Design / build front-end page(s) for analysts
- Create back-end functionality for connecting to database and returning necessary data, facts etc.


### Data Engineering

We will need to construct a data pipeline / workflow to manage the end-to-end process, both for batch processing of files as well as (potentially) real-time processing of individual urls:

+ Data collection from various sources, i.e. existing csv files, new file provided by analysts etc.
+ Data pre-processing - applying the filtering tools created to exclude broken, irrelevant and non-English articles
+ Article classification - applying the pre-trained classifier, or training a new classifier
+ Fact Extraction - using NLP tools for extracting the key facts from the articles
+ Data storage - saving the article along with relevenat tags and extracted facts
+ API for enabling data analysts to interact with the data


### All Deliverables:

- URL to working version of the tool
- Source code repo
- Analysis of the test dataset
- User guide
- Admin guide

__Activities:__
- Create, maintain and update user guide (documentation)
- Create, maintain and update admin guide (documentation)


### Possible Libraries

___NLP:___
- nltk
- Tensor Flow
- Spacy

___Text parsing and fact extraction:___
- mordecai - Geoparsing (extracting relevant country)
- Newspaper module (python 3)
- goose-extractor - Text + meta-data extraction (only python 2)


