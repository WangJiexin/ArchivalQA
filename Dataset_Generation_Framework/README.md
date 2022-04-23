# Dataset Generation Framework

The following figure shows the architecture of our QG framework, which consists of five modules: <em>Article Selection Module</em>, <em>Question Generation Module</em>, <em>Syntactic & Temporal Filtering/Transforming Module</em>, <em>General & Temporal Ambiguity Filtering Module</em> and <em>Triple-based Filtering Module</em>.
<p align="center">
  <img src="Figures/QG_Framework.png">
</p>

In the paper, the NYT corpus is utilized as the underlying temporal news collection for creating ArchivalQA dataset. Note that due to the NYT corpus policy, we need to prevent exposing the whole NYT corpus to the public. To obtain the corpus, refer to https://catalog.ldc.upenn.edu. For better explaining last four modules of the framework, we randomly select a news article in NYT corpus as an example that stored in `example.txt`. 

The processing notebooks should be run in the order of:
## 1.Article Selection Module
In this module, we use two selection strategies on NYT corpus: (1).Selection based on Wikipedia Events and (2).Random Selection.


## 2.Question Generation Module

## 3.Syntactic & Temporal Filtering/Transforming Module

## 4.General & Temporal Ambiguity Filtering Module

## 5.Triple-based Filtering Module
