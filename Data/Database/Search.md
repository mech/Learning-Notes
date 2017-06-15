# Search

* [What's Wrong With Taxonomies - The Future is Faceted](http://semanticstudios.com/the_speed_of_information_architecture/)

In Yelp business listing, there is business name, operating hours, images, and some attributes invisible to the users. There are also content components that we don't want to search, such as reviews and tips. These could confuse a user's search results; for example, if a review included the name of a competing restaurant.

As much as we want to index all things, we should know when to leave out content that shouldn't be indexed.

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

## ElasticSearch

* [stretchy - Query builder for ElasticSearch](https://github.com/hired/stretchy)

## Blog

* [Semantic Studios](http://semanticstudios.com/writing/)