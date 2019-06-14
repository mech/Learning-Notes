# Search

* [What's Wrong With Taxonomies - The Future is Faceted](http://semanticstudios.com/the_speed_of_information_architecture/)
* [Search at Slack](https://slack.engineering/search-at-slack-431f8c80619e)
* [**What every software engineer should know about search**](https://medium.com/startup-grind/what-every-software-engineer-should-know-about-search-27d1df99f80d)
* [Doug Turnbull](https://medium.com/@softwaredoug/this-is-a-fantastic-post-e9caae910334)
* [Awesome Information Retrieval](https://github.com/harpribot/awesome-information-retrieval)
* [Sourcegraph open sourced!](https://github.com/sourcegraph/sourcegraph)

In Yelp business listing, there is business name, operating hours, images, and some attributes invisible to the users. There are also content components that we don't want to search, such as reviews and tips. These could confuse a user's search results; for example, if a review included the name of a competing restaurant.

As much as we want to index all things, we should know when to leave out content that shouldn't be indexed.

## Diacritic

* [Searching and sorting text with diacritical marks in JavaScript](https://thread.engineering/2018-08-29-searching-and-sorting-text-with-diacritical-marks-in-javascript/)

## Search UI

* [Search interface: 20 things to consider](https://uxplanet.org/search-interface-20-things-to-consider-4b1466e98881)

## Learning to Rank

* [Rank Elasticsearch results using tree based (LambdaMART, Random Forest, MART) and linear models](https://github.com/o19s/elasticsearch-learning-to-rank)

## Personalized and Recent Results

Staff's search need to be personalized and relevance to them. This mean we need to embed staff_id for items relevant to them!

> Imagine searching for "401k matching" and instead of just receiving relevant messages or files, you also get a list of people in HR that can answer your question, or a list of channels for your query where you might be able to find the information you are looking for, or even a list of commonly asked questions relevant to that topic with links to the channel where each one was answered. We still have a lot of work to do to reduce that 20% of information-seeking time, allowing users of Slack to have a more pleasant, productive experience.

## Similar documents

Metadata.

## Collaborative Filtering

Tagging.

## Precision and Recall

* Precision - **Only** the relevant documents. Very precise. Word by word matching.
* Recall - **All** the relevant documents. As broad and wide a net as possible.

## Metadata

* [How Netflix Reverse Engineered Hollywood](https://www.theatlantic.com/technology/archive/2014/01/how-netflix-reverse-engineered-hollywood/282679/)

Metadata tags are used to describe documents, pages, images, software, video and audio files, and other content objects for the purposes of **improved navigation and retrieval**.

Leveraging **CMS** and **controlled vocabularies**, they create dynamic metadata-driven systems that support distributed authoring and powerful navigation.

* Skill sets is a controlled vocabulary in an Authority File.

### Synonym Rings (Unlimited aliasing)

For job posting, have a text file for them to enter synonym reference (i.e. food processor, blender or iTouch vs iPod Touch).

```
(data science) becomes ("hadoop" or "sparks" or "R" or "Cloudera")
```

> Other retailers provide synonyms for "itouch", leading to more useful results even though the user entered a "wrong" search term.

You might use synonym rings by default but order the exact keyword matches at the top of the search results list. Or, you might ignore synonym rings for initial searches but provide the option to "expand your search to include related terms" if there were few or no results.

## Authority File

```
# Singapore university authority file
NUS National University of Singapore
NTU Nanyang Technological University
SMU Singapore Management University
SUTD Singapore University of Technology and Design
SIT Singapore Institute of Technology
SUSS Singapore University of Social Sciences

# USA states
AL AlabamaAK Alaska
AZ ArizonaAR ArkansasCA CaliforniaCO Colorado
```

Synonym management, hierarchical browsing, and associative linking.

## Elasticsearch

* [stretchy - Query builder for ElasticSearch](https://github.com/hired/stretchy)
* [Elasticsearch For Beginners: Indexing your Gmail Inbox](https://github.com/oliver006/elasticsearch-gmail)
* [Building a new search for FT.com](https://www.maketea.co.uk/2017/12/20/building-a-new-search-for-ft-com.html)
* [Elasticsearch bucket aggregations and faceted navigation](https://iridakos.com/tutorials/2018/10/22/elasticsearch-bucket-aggregations.html)

## Blog

* [Semantic Studios](http://semanticstudios.com/writing/)

## Videos

* [We built an Elasticsearch Learning to Rank plugin](https://www.youtube.com/watch?v=JqqtWfZQUTU)

