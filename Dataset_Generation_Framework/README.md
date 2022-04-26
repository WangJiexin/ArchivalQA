# Dataset Generation Framework

The following figure shows the architecture of our QG framework, which consists of five modules: <em>Article Selection Module</em>, <em>Question Generation Module</em>, <em>Syntactic & Temporal Filtering/Transforming Module</em>, <em>General & Temporal Ambiguity Filtering Module</em> and <em>Triple-based Filtering Module</em>.
<p align="center">
  <img src="Figures/QG_Framework.png">
</p>

In the paper, the NYT corpus is utilized as the underlying temporal news collection for creating ArchivalQA dataset. Note that due to the NYT corpus policy, we need to prevent exposing the whole NYT corpus to the public. To obtain the corpus, refer to https://catalog.ldc.upenn.edu. The data of the NYT corpus is used in the codes of the first module.

For better explaining the last four modules of the framework, we randomly sample three paragraphs of three news articles in NYT corpus, that are stored in `examples.pkl`. Each example paragraph is consist of the paragraph-id information, the paragraph text and the publication date of the article.

The processing notebooks should be run in the order of:
## 1_Article_Selection_Module.ipynb
In Article Selection Module, we use two selection strategies to select news articles of NYT corpus: (1).Selection based on Wikipedia Events and (2).Random Selection. 

The `Article_Selection_Module.ipynb` only contains the code of the first strategy as the second one is simple, and you can also define your own selection methods, too. Note that Yake! is used as our keyword extraction method and the keywords are then sent to the ElasticSearch, which returns top-25 NYT articles ranked by BM25. The codes of this module need to use the NYT corpus and ElasticSearch, that you need to obtain or set up in advance.

## 2_Question_Generation_Module.ipynb
In Question Generation Module, we use the fine-tuned T5-base to generate questions for each paragraph.

There are a few hyperparameters in `Article_Selection_Module.ipynb` that need to be set and will influence the results: min_para_token_num, min_anssent_token_num, ans_ent_type_exclude_list. They influence the QG results by: (1).The paragraphs that have less than min_para_token_num tokens are eliminated. (2).The answers whose corresponding sentences have less than 10 tokens are eliminated. (3).The answers whose corresponding NER types in ans_ent_type_exclude_list(["PERSON", "ORG", ...], but not used in our work and set to empty list) are eliminated.

## 3_Syntactic&Temporal_Processing_Module.ipynb
Question Generation Module consists of 8 basic processing steps that further remove or transform the candidate question-answer pairs obtained so far. Please check the paper for more details.

## 4_General&TemporalAmbiguity_Filtering_Module.ipynb
In General & Temporal Ambiguity Filtering Module, two models are trained for filtering the questions using two different training data. The specificity model aims to remove questions that are generated from general sentences. The ambiguity model aims to remove temporally ambiguous questions. Note that you can define your own model with better architecture and achieve better performance by using the training data.

## 5_Triple-based_Filtering_Module.ipynb
The final module -- Triple-based Filtering Module aims to remove remaining poor quality data instances by analyzing the entire <question, answer, paragraph> triples. The triple-base model is trained by using the 10k annoated triple samples and then filter the triples that are classified as Bad. Note that you can also define your own model by using the training data.
