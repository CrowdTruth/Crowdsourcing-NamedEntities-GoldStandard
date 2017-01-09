# Harnessing diversity in crowds and machines for better NER performance


This repository contains the experimental results of identifying and typing named entities in English Wikipedia sentences. Even though current named entity recognition tools achieve nearly human-like performance or particular data types or domains, they are still highly dependent on the gold standard used for training and testing. The mainstream approach of gathering ground truth or gold standard for training and evaluating named entity recognition tools is still by means of experts, who are typically expensive and hard to find. Furthermore, for each new input type, or each new domain, new gold standards need to be created. Overall, the experts follow over-generalized annotation guidelines, meant to increase the <b>inter-annotator agreement</b> between experts. Such guidelines are thus prone to denying the intrinsic language ambiguity, multitude of perspectives and interpretations. Thus, ground truth datasets might not always be 'gold' or 'true' in terms of capturing the real text meaning and interpretation diversity. In the last decade crowdsourcing has also proven to be a suitable method for gathering such ground truth, but data ambiguity is still not handled.

However, in our work we focus on capturing the <b>inter-annotator disagreement</b> to provide a new type of ground truth, i.e., crowd truth - by applying the CrowdTruth metrics and methodology, where language features are taken into consideration. All the crowdsourcing experiments were performed through the CrowdTruth platform, while the results were processed and analyzed using the CrowdTruth methodology and metrics. For more information, check the <b><a href="http://crowdtruth.org/">CrowdTruth</a></b> website. For gathering the annotated data, we used the <b><a href="http://corwdflower.com/">CrowdFlower</a></b> marketplace.

We propose a novel approach for extracting and typing named entities in texts, i.e.m a hybrid multi-machine-crowd approach where state-of-the-art NER tools are combined and their aggregated output is validated and improved through crowdsourcing. We report here results of:
1. Five state-of-the-art named entity recognition tools (SingleNER)
2. The combined output of the five state-of-the-art named entity recognition tools (MultiNER)
3. Crowdsourcing experiments for correcting and improving the Multi-NER output and also for improving the expert-based gold standard (MultiNER+Crowd). 


## Check the Results & Download the Data: <a href="https://github.com/CrowdTruth/Crowdsourcing-NamedEntities-GoldStandard">Crowdsourcing-Improved-NE-Gold-Standard</a>


## Table of Contents:

* [Experimental Data](#experimentaldata)
* [Dataset Files](#datasetfiles)
* [Crowdsourcing Experiments](#crowdsourcingexperiments)
   * [Crowdsourcing Experimental Data](#crowdsourcingdata)
   * [Crowdsourcing Annotation Task](#crowdsourcingtask)
* [Experiments Results](#results)
   * [Single-NER vs. Multi-NER (entity surface)](#SingleNER-MultiNER-surface)
   * [Single-NER vs. Multi-NER (entity surface and entity type)](#SingleNER-MultiNER-surface-type)
   * [Crowd-Enhanced Multi-NER](#Crowd-MultiNER)


<a id="experimentaldata"></a>

## Experimental Data:

We performed named entity extraction with five state-of-the-art NER tools: <a href="http://nerd.eurecom.fr">NERD-ML</a>, <a href="https://www.textrazor.com">TextRazor</a>, <a href="http://ner.vse.cz/thd/">THD</a>, <a href="http://dbpedia-spotlight.github.io/demo/">DBpediaSpotlight</a>, and <a href="http://nlp.vse.cz/SemiTags/">SemiTags</a>. We performed a comparative analysis of (1) their performance (output) and (2) their combined performance (output), on <b>two ground truth (GT) evaluation datasets</b> used during Task 1 of the Open Knowledge Extraction (OKE) semantic challenge at ESWC in 2015 (<i>OKE2015</i>) and 2016 (<i>OKE2016</i>) respectively. The datasets can be checked here:
1. <b>OKE2015</b>: Open Knowledge Extraction 2015 (OKE2015) semantic challenge: https://github.com/anuzzolese/oke-challenge
2. <b>OKE2016</b>: Open Knowledge Extraction 2016 (OKE2016) semantic challenge: https://github.com/anuzzolese/oke-challenge-2016

In summary, there are $156$ Wikipedia sentences with $1007$ annotated named entities of types <i>place</i>, <i>person</i>, <i>organization</i> and <i>role</i> distributed across datasets in the following way:

<table class="tg">
  <tr>
    <th class="tg-s6z2" rowspan="6"></th>
    <th class="tg-s6z2" colspan="3" style="text-align:center;">OKE2015</th>
    <th class="tg-s6z2" colspan="3" style="text-align:center;">OKE2016</th>
  </tr>
  <tr>
    <td class="tg-baqh">Sentences</td>
    <td class="tg-baqh" colspan="2">Named Entities</td>
    <td class="tg-baqh">Sentences</td>
    <td class="tg-baqh" colspan="2">Named Entities</td>
  </tr>
  <tr>
    <td class="tg-baqh" rowspan="4" style="text-align:center;">101</td>
    <td class="tg-baqh">Place</td>
    <td class="tg-baqh" style="text-align:center;">120</td>
    <td class="tg-baqh" rowspan="4" style="text-align:center;">55</td>
    <td class="tg-baqh">Place</td>
    <td class="tg-baqh" style="text-align:center;">44</td>
  </tr>
  <tr>
    <td class="tg-baqh">Person</td>
    <td class="tg-baqh" style="text-align:center;">304</td>
    <td class="tg-baqh">Person</td>
    <td class="tg-baqh" style="text-align:center;">105</td>
  </tr>
  <tr>
    <td class="tg-baqh">Organization</td>
    <td class="tg-baqh" style="text-align:center;">139</td>
    <td class="tg-baqh">Organization</td>
    <td class="tg-baqh" style="text-align:center;">105</td>
  </tr>
  <tr>
    <td class="tg-baqh">Role</td>
    <td class="tg-baqh" style="text-align:center;">103</td>
    <td class="tg-baqh">Role</td>
    <td class="tg-baqh" style="text-align:center;">86</td>
  </tr>
  <tr>
    <td class="tg-baqh">Total</td>
    <td class="tg-baqh" style="text-align:center;">101</td>
    <td class="tg-baqh" colspan="2" style="text-align:center;">664</td>
    <td class="tg-baqh" style="text-align:center;">55</td>
    <td class="tg-baqh" colspan="2" style="text-align:center;">340</td>
  </tr>
</table>

      
<a id="datasetfiles"></a>

## Dataset Files:

```
|--/aggregate
```
Various aggregated datasets for analyzing the output of multiple state-of-the-art named entity recognition tools (SingleNER), their combined output (MultiNER) and crowdsourcing data for correcting and improving the MultiNER approach and the gold standard. 

```
|--/aggregate/OKE2015/OKE2015_SingleNER_and_MultiNER_eval.csv
|--/aggregate/OKE2016/OKE2016_SingleNER_and_MultiNER_eval.csv
```
These files contain the results of the five SOTA NER tools and the results of the MultiNER approach on the two gold standards datasets aforementioned. The files contain all the named entities in the gold standards and all the other alternatives (overlapping expressions) that were extracted by any SOTA NER for that entity. The columns are:

* *Identifier*: sentence ID as referenced in the gold standard datasets
* *Sentence*: sentence content as referenced in the gold standard datasets
* *NamedEntity*: a potential named entity extracted by any of the five SOTA NER tools; 
* *StartOffset*: start offset of the named entity
* *EndOffset*: end offset of the named entity
* *GoldEntityType*: the type of the named entity as provided in the gold standard
* *EntityScore*: the likelihood of an entity to be in the gold standard based on how many NER tools extracted it. The score is equal to the ratio of NER tools that extracted the entity. 
* *SingleNERCount*: the number of SOTA NER tools that extracted the named entity
* *Gold*: binary value describing whether the named entity is contained in the gold standard (1) or not (0)
* *MultiNER*: binary value describing whether any of the NER tools extracted the named entity (1) or not (0)
* *NERD,TextRazor,SemiTags,THD,DBpediaSpotlight*: binary value describing whether the given NER tool extracted the named entity (1) or not (0)
* *TP_MultiNER*: binary value describing whether the named entity is a TP case (1) or not (0), with regard to the MultiNER approach 
* *TP_NERD,TP_TextRazor,TP_SemiTags,TP_THD,TP_DBpediaSpotlight*: binary value describing whether the named entity is a TP case (1) or not (0), with regard to the SingleNER approach 
* *TN_MultiNER*: binary value describing whether the named entity is a TN case (1) or not (0), with regard to the MultiNER approach 
* *TN_NERD,TN_TextRazor,TN_SemiTags,TN_THD,TN_DBpediaSpotlight*: binary value describing whether the named entity is a TN case (1) or not (0), with regard to the SingleNER approach
* *FP_MultiNER*: binary value describing whether the named entity is a FP case (1) or not (0), with regard to the MultiNER approach 
* *FP_NERD,FP_TextRazor,FP_SemiTags,FP_THD,FP_DBpediaSpotlight*: binary value describing whether the named entity is a FP case (1) or not (0), with regard to the SingleNER approach
* *FN_MultiNER*: binary value describing whether the named entity is a FN case (1) or not (0), with regard to the MultiNER approach 
* *FN_NERD,FN_TextRazor,FN_SemiTags,FN_THD,FN_DBpediaSpotlight*: binary value describing whether the named entity is a FN case (1) or not (0), with regard to the SingleNER approach


```
|--/aggregate/OKE2015/OKE2015_MultiNER_and_Crowd_eval.csv
|--/aggregate/OKE2016/OKE2016_MultiNER_and_Crowd_eval.csv
```
These files contain the results of the five SOTA NER tools, the results of the MultiNER approach on the two gold standards and the crowdsourcing results for every named entity in the gold standard that has multiple alternatives.  The columns are:

* *Identifier*: sentence ID as referenced in the gold standard datasets
* *Sentence*: sentence content as referenced in the gold standard datasets
* *NamedEntity*: a potential named entity extracted by any of the five SOTA NER tools; 
* *StartOffset*: start offset of the named entity
* *EndOffset*: end offset of the named entity
* *GoldEntityType*: the type of the named entity as provided in the gold standard
* *EntityScore*: the likelihood of an entity to be in the gold standard based on how many NER tools extracted it. The score is equal to the ratio of NER tools that extracted the entity. 
* *SingleNERCount*: the number of SOTA NER tools that extracted the named entity
* *Gold*: binary value describing whether the named entity is contained in the gold standard (1) or not (0)
* *CrowdGold*: binary value describing whether the named entity is considered a valid named entity by the crowd (1) or not (0)
* *MultiNER*: binary value describing whether any of the NER tools extracted the named entity (1) or not (0)
* *NERD,TextRazor,SemiTags,THD,DBpediaSpotlight*: binary value describing whether the given NER tool extracted the named entity (1) or not (0)
* *TP_MultiNER*: binary value describing whether the named entity is a TP case (1) or not (0), with regard to the MultiNER approach 
* *TP_NERD,TP_TextRazor,TP_SemiTags,TP_THD,TP_DBpediaSpotlight*: binary value describing whether the named entity is a TP case (1) or not (0), with regard to the SingleNER approach 
* *TN_MultiNER*: binary value describing whether the named entity is a TN case (1) or not (0), with regard to the MultiNER approach 
* *TN_NERD,TN_TextRazor,TN_SemiTags,TN_THD,TN_DBpediaSpotlight*: binary value describing whether the named entity is a TN case (1) or not (0), with regard to the SingleNER approach
* *FP_MultiNER*: binary value describing whether the named entity is a FP case (1) or not (0), with regard to the MultiNER approach 
* *FP_NERD,FP_TextRazor,FP_SemiTags,FP_THD,FP_DBpediaSpotlight*: binary value describing whether the named entity is a FP case (1) or not (0), with regard to the SingleNER approach
* *FN_MultiNER*: binary value describing whether the named entity is a FN case (1) or not (0), with regard to the MultiNER approach 
* *FN_NERD,FN_TextRazor,FN_SemiTags,FN_THD,FN_DBpediaSpotlight*: binary value describing whether the named entity is a FN case (1) or not (0), with regard to the SingleNER approach
* *MainAlternativeSpan*: the largest span extracted by any NER tools that overlaps with a named entity in the gold standard; 
* *AlternativeStartOffset*: start offset of the named entity alternative
* *AlternativeEndOffset*: end offset of the named entity alternative
* *AlternativeCrowdScore*: the likelihood of an entity to be in the gold standard based on the crowd assessment. The score is computed using the cosine similarity measure 
* *RoleScore,PersonScore,OrganizationScore,PlaceScore,OtherScore*: the likelihood of an entity to refer to the given type based on the crowd assessment. The score is computed using the cosine similarity measure 


```
|--/input
|  |--/Valid Named Entity Expressions
|  |  |--/OKE2015
|  |  |--/OKE2016
```
The files contain the input for the crowdsourcing tasks for each dataset. An input unit is composed of a sentence and a set of expressions that refer to a named entity. 


```
|--/raw
|  |--/Valid Named Entity Expressions
|  |  |--/OKE2015
|  |  |--/OKE2016
```
The raw data collected from crowdsourcing tasks for each of the 2 datasets.


<a id="crowdsourcingexperiments"></a>

## Crowdsourcing Experiments:

Overall, the aim of the crowdsourcing experiments is to:
1. correct the mistakes of the NER tools
2. identify the ambiguities in the ground truth and provide a better ground truth 

<a id="crowdsourcingdata"></a>

### Crowdsourcing Experimental Data

We select every entity in the ground truth for which the NER tools provided alternatives. We have the following two cases:  
* <i>Crowd reduces the number of FP</i>: For each named entity in the ground truth that has multiple alternatives (span alternative) we create an entity cluster. We also add the largest span among all the alternatives.  
* <i>Crowd reduces the number of FN</i>: For each named entity in the ground truth that was not extracted, we create an entity cluster that contains the FN named entity and the alternatives returned by the NER. Further, we add every other combination of words contained in all the alternatives. This step is necessary because we do not want to introduce bias in the task, i.e., the crowd should see all the possibilities, not only the expected one.  

<a id="crowdsourcingtask"></a>

### Crowdsourcing Annotation Task

For the two cases described above, the goal of the crowdsourcing task is two-fold: 
* identification of valid expressions from a list that refer to a highlighted phrase in yellow (Step 2 from the crowdsourcing template below)
* selection of the type for each expression in the list, from a predefined set of choices - place, person, organization, role and other (Step 3 from the crowdsourcing template below). 

The input of the crowdsourcing task consists of a sentence and a named entity for which multiple expressions were given by the five state-of-the-art NER tools.

Check the crowdsourcing templates below. 

![Fig.1: CrowdTruth Workflow for Identifying Valid Named Entity Expressions and their Type.](https://raw.githubusercontent.com/CrowdTruth/Crowdsourcing-NamedEntities-GoldStandard/master/templates/Screen Shot 2016-11-29 at 15.20.34.png)
![Fig.2: CrowdTruth Workflow for Identifying Valid Named Entity Expressions and their Type.](https://raw.githubusercontent.com/CrowdTruth/Crowdsourcing-NamedEntities-GoldStandard/master/templates/Screen Shot 2016-11-29 at 15.26.11.png)

