# Wiki-Reliability: A Large Scale Dataset for Content Reliability on Wikipedia
This repo contains the processing code we used to create the Wiki-Reliability dataset.

The processing notebooks should be run in the order of:

## 1. MatchTemplatesUDF.ipynb
* The `MatchTemplatesUDF.ipynb` works on in PySpark and uses an AVRO version of the XLM Wikipedia dumps (dumps.wikipedia.org). The code can be adapted to the XML version  embedding the ""getTemplatesRegexReliability()"" function on the [mwxml package](https://pythonhosted.org/mwxml/). 

* Wikipedia dumps in XML can be downloaded [here](https://dumps.wikimedia.org). To get all the revisions you need to download the "All pages with complete edit history" files.

* If you decide to work in PyPspark, you can use [this repository](https://github.com/wikimedia/analytics-wikihadoop) to transform the XML dump to AVRO.

* A recent version of the  mediawiki_history table can be  downloaded from https://dumps.wikimedia.org/other/mediawiki_history/

## 2. Process_Templates.ipynb
* Processes the full history of revisions returned by `MatchTemplatesUDF` to extract positive and negative template pairs. Positive examples are versions of an article which contain a reliability issue, signalled by the addition of the template, while negative examples are article revisions where the issue has been resolved, signalled by the removal of the template.  

* For each revision example, extracts a set of metadata features.

## 3. Process_Templates_Text.ipynb
* For each revision example in the dataset, parses the article's textual contents to be included as part of a text dataset for NLP tasks.

* For each revision, extracts the:
  - full text of the revision
  - diff'd version of the revision text, containing only the changed sections of text between each revision pair

## 4. Project Information
* Authors: KayYen Wong, [Miriam Redi](http://www.visionresearchwitch.com/) and [Diego Saez-Trumper](https://meta.wikimedia.org/wiki/User:Diego_(WMF)).

* For more details, see the [Research Project Page](https://meta.wikimedia.org/wiki/Research:Wiki-Reliability:_A_Large_Scale_Dataset_for_Content_Reliability_on_Wikipedia) for additional information.
