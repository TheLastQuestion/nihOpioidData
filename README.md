# Opioid crisis -- what's the government doing about it?
#### Analysis performed in connection with a data science [Medium post](https://medium.com/@bryant.d.renaud/opioid-crisis-whats-the-government-doing-about-it-42f5f50fe6e4)
#### _Not an official position of the US Govt._

### Table of Contents

1. [Installation](#installation)
2. [Project Motivation](#motivation)
3. [File Descriptions](#files)
4. [Results](#results)
5. [Licensing, Authors, and Acknowledgements](#licensing)
6. [A note on Text Analysis](#text)

## Installation <a name="installation"></a>

There should be no necessary libraries to run the code here beyond the Anaconda distribution of Python.  The code should run with no issues using Python versions 3.*. The libraries used, however, are:
* downloading data
    * urlib
    * zipfile
    * io
* wrangling data
    * pandas
    * numpy
* cleaning data
    * re
* modeling
    * nltk
    * sklearn
    * statsmodels
* visualizing
    * pyplot

## Project Motivation<a name="motivation"></a>

I am currently making my wy through an intensive data science certification course. I developed this code and the associated blog post as my first large assignment in the course. It is, of course, also inspired by current events.

## File Descriptions <a name="files"></a>

You will need to run the downloadData notebook in order to pull the open data from Federal Reporter and assemble it into one csv.

The opioidResearchData notebook will then read in that csv and perform all the analysis and plot-generation. The other files in this repo include a washington post image for the medium post and the plots generated from this notebook.

## Results<a name="results"></a>

Please read the [Medium post](https://medium.com/@bryant.d.renaud/opioid-crisis-whats-the-government-doing-about-it-42f5f50fe6e4) for details, but a summary of findings is:
1. Research lags current events — despite the fact that the opioids crisis, in terms of mortality, was well underway in the late ’00s, NIH’s opioid-related research portfolio did not see a spike in funding until much later, starting around 2016. This spike took the form of both an increase in the number of opioids projects awarded as well as dollars awarded for opioids projects.
2. Using NLP and topic modeling, we observed that studies involving particular patient subgroups are rising in importance. Taken as a whole, however, the plurality of opioids projects over the last 11 fiscal years have tended to involve conditions opioids are prescribed for, HIV and other infections, and dependence and recovery.
3. While total project costs tend not to vary much by topic area, those projects associated with the road to recovery do seem to be funded at a level around $100,000 more than projects in most other topics. Organizations in certain states tend to have larger project costs, but this may be an artifact of those organizations receiving relatively few opioid project grants.

## Licensing, Authors, Acknowledgements<a name="licensing"></a>

I've included the MIT license here to be as permissive as makes sense. If you find anything here useful, go for it! Of course, if you use the WaPo picture, make sure to attribute properly, as it is not mine to circulate freely.

## A note on Text Analysis (Topic Modeling)<a name="text"></a>

LDA (Latent Dirichlet Allocation) is a model used for discovering abstract topics from a collection of documents. These 'latent' topics can be discovered based on observed data -- words in the documents, in this case.

To surface these topics, we create a matrix where each document is a row and each column is a word in the corpus vocabulary. The corpus vocabulary is the universe of words present in any one or more documents in the corpus (minus chosen 'stopwords' that we consider to provide little information).

Each cell of the matrix would be a count of that word in that document. A variant increases the level of sophistication by using a normalized version of these counts known as TF-IDF. TF stands for term-frequency and TF-IDF is term-frequency times inverse document-frequency. In other words, we are not only looking for how often a word appears in a given document, but also whether this particular word is distinct across all the collections of documents (corpus). For example, intuitively we understand that words like "often" or "use" are more frequently encountered, but they are less informative (more semantically-vacuous) if we want to discern a particular topic of a document, as they might be frequently encounter across all text documents in a corpus. On the other hand, words which we will see less frequently across a collection of document might indicate that those words are specific to a particular document, and, therefore, constitute a basis for a topic.

We provide the model with this matrix and how many topics we want it to use. Think of it like a k-means clustering analog. The model will then iterate a specified number of times considering two distributions; 1) which words in the vocabulary are more or less probable to belong in a given topic and 2) which topic is more or less probable for a given document.

The main assumptions, if this all went over your head:
* each document consists of a mixture of topics, and
* each topic consists of a collection of words.
