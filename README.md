# LAGT: Lemmatized Ancient Greek Texts
---

## Purpose
This repository serves for extraction, merging, cleaning and morphological analysis of publicly available ancient Greek texts accessible via two GitHub repositories:
* [Perseus Digital Library](https://github.com/PerseusDL/canonical-greekLit)
* [First 1000 Years of Greek](https://github.com/OpenGreekAndLatin/First1KGreek)

The morphological analysis has been implemented using [spaCy](https://spacy.io) and consists of (1) a **coarse-grained POS-tagging** and (2) a dictionary-based **lemmatization**.

The POS-tagger has been trained using two universal dependencies treebank data:
* [Perseus](https://github.com/UniversalDependencies/UD_Ancient_Greek-Perseus/tree/master) (11,476 train sentences, 1,137 test sentences)
* [PROIEL](https://github.com/UniversalDependencies/UD_Ancient_Greek-PROIEL/tree/master) (15,014 train sentences; 1,019 test sentences) 
The lemmatizer relies on a stable version of the Greek part of Morpheus dictionary [link](https://github.com/gcelano/LemmatizedAncientGreekXML/tree/master/Morpheus). The dictionary is simplified, transformed into Python dictionary and reorganized with items arranged by postags:
```python
{"POSTAG1" : 
	{"wordform1" : "lemma1",
	 "wordform2" : "lemma1",
	 ...},	 
{"POSTAG2: : 
	{...}}
```
The dictionary is further extended 




---
## Authors
* Vojtěch Kaše [![](https://orcid.org/sites/default/files/images/orcid_16x16.png)]([0000-0002-6601-1605](https://www.google.com/url?q=http://orcid.org/0000-0002-6601-1605&sa=D&ust=1588773325679000)), SDAM project, vojtech.kase@gmail.com


## License
CC-BY-SA 4.0, see attached License.md

## DOI
[Here will be DOI or some other identifier once we have it]

### References
[Here will go related articles or other sources we will publish/create]

---
# How to use this repository

## Sources and prerequisites
This repository contains scripts in Python 3. These scripts are mainly in  Jupyter Notebook file format and it should be possible to run them with any local or cloud-bysed Python and Jupyter Notebook/Lab environment. 

### Data
The raw data are from two GitHub repositories:
* **Perseus Digital Library**:  https://github.com/PerseusDL/canonical-greekLit - XML Canonical resources for Greek Literature
* **Open Greek and Latin**: https://github.com/OpenGreekAndLatin/First1KGreek - XML files for the works in the First Thousand Years of Greek Project

### Software
1. Jupyter Lab (Jupyter notebooks files)
1. Sciencedata.dk web interface

### Registered account
1. Google account - to work with metadata
2. Github account (to extract the raw data straightforward from Github)
3. Sciencedata.dk account (to work with preprocessed data to which point the script.
4. S

## Instructions 

You can either (1) clone the repo into your Google Drive and then open the scripts directly in Google Colab (2) clone the repo into your local hard drive and run the scripts with your local Jupyter, (3) open Google Colab and choose an option to open a file from Github.

* `1_DATA-EXTRACTION.ipynb` 
	* **description**: It extracts the data from public GitHub repositories (hundreds of tei-xml files), merges them into one Pandas dataframe and export this dataframe into a json file at sciencedata.dk. It also checks for duplicates in tlg codes in filesnames.  (e.g. `tlg0086.tlg010` is a tlg code  code for Aristotle's *Ethica Nicomachea*).
	* **input**:  xml files located on GitHub, scrapped directly from there
	* **output**: `AGT_raw_[yyyymmdd].json`
    

* `2_DATING&PROVENIENCE.ipynb` 
	* **description**:  This scripts enriches the raw data in various ways, especially by dating and cultural provenience. It also removes duplicates. In splits collective works (e.g. New Testament and Homeric Hymns) as produced by individual authors.
	* **input**: `AGT_raw_[yyyymmdd].json`
	* **output**:  `AGT_dated_[yyyymmdd].json`
  
  
  
* `3_LEMMATIZATION.ipynb` 
	* **description**: It produces lemmatized text as a list of words and a list of lemmatized sentences as a list of lists of words.
    * **input**: `AGT_dated_[yyyymmdd].json
    * **output**: `AGT_[yyyymmdd].json`
    
* `3_OVERVIEW.ipynb` 
	* **description**: It produces various overview figures and tables
    * **input**: `AGT_[yyyymmdd].json`
    * **output**: various figures and tables
 
* `VARIOUS.ipynb` 
	* **description**:  various scripts, mainly for testing


Using [TLG metadata for dating](https://raw.githubusercontent.com/cltk/cltk/master/cltk/corpus/greek/tlg/author_date.py), we were able to get some sort of dating for 1,374 documents.

Next to it, we were able to classify 876 as either "christian" or "pagan" provenience. 
