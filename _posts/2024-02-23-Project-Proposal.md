---
layout: post
---
## Introduction/Background
Wikipedia is a common source of information that can be accessed around the world, so it’s crucial that accuracy and reliability is maintained. Currently, the Wikipedia community relies on editors to manually classify the quality of articles, however, one study proposes automatically assessing quality using gradient boosted trees. The method incorporates a features set to demonstrate the effectiveness in classifying the reliability of Wikipedia content and simplifying the moderation process [^3]. Another study tests an end-to-end learning method that doesn’t rely on manual feature engineering and utilizes Recurrent Neural Networks, which revealed higher performance in evaluating articles across multiple languages [^2]. These approaches highlight that ML techniques offer more efficient and accurate solutions to determining the reliability of Wikipedia content. To expand on current advancements, our project aims to classify articles based on citations and deliberate misinformation. The dataset used in this project consists of three different template files used by Wikipedia editors to flag for possibly unreliable content: hoax, more citations needed, unreliable sources. For each template, feature has_template will be used as the ground truth [^1].

[View our dataset!][dataset]
{: .alert .alert--success}

## Problem Definition
The reliability of Wikipedia articles are hindered by deliberate spreading of misinformation and ignorance of the requirements that go into making a quality article such as appropriate citations and valid sources. These problematic articles are moderated by editors who use templates to mark areas in which articles need to be improved including no citations, biased sources, or contradictory information. Reading millions of articles to determine which, if any, problematic templates an article falls into takes substantial time. A ML algorithm that automatically classifies articles as negative or positive for its appropriate templates would save the time of editors and make Wikipedia a more reliable source.

## Methods
### Data Preprocessing
* Remove duplicate data points - remove articles belonging to multiple templates. sklearn.model_selection.GroupKFold will remove revisions of the same article
* TF-IDF to process raw text data (sklearn.feature_extraction.text.TfidfTransformer) - converts raw text into numerical features based on word occurrence frequency
* Word embedding (Word2vec) - processes text data to include semantic relationships between words



### ML Algorithms/Models
1. Random Forest Classifier: uses multiple decision trees to offset bias and overfitting seen in single decision trees
2. Gradient Boosted Trees: combines weak learners so that the next tree corrects errors of previous trees
3. Naive Bayes: assumes features are conditionally independent, high processing speed

## (Potential) Results and Discussion
### Quantitative Methods
* F1 Score - balance of precision and recall
* Balanced Accuracy -  mean of sensitivity and specificity that considers the class imbalance of the dataset
* Area Under the ROC Curve - measures the model’s ability to discriminate between classes

### Project Goals
* Balanced Accuracy: high ratio of true positives to false positives and negative, ideally >0.7
* F1 score: match or improve existing methods with accuracy ranging from 0.6-0.7 [^2] [^3]
* Area Under the ROC Curve: >0.7

### Expected Results
The model is expected to at least match or improve the accuracy of previous work. The dataset used is reliable and complete, so we expect a high F1 score and area under the ROC curve, which would characterize a successful Wikipedia article reliability classification.

## Video
{% include youtubePlayer.html id=page.youtubeId %}

[^1]: K. Wong, M. Redi, and D. Saez-Trumper, “Wiki-Reliability: A large scale dataset for content reliability on Wikipedia,” Proceedings of the 44th International ACM SIGIR Conference on Research and Development in Information Retrieval, Jul. 2021. doi:10.1145/3404835.3463253

[^2]: Q.-V. Dang and C.-L. Ignat, “An end-to-end learning solution for assessing the quality of Wikipedia articles,” Proceedings of the 13th International Symposium on Open Collaboration, Aug. 2017. doi:10.1145/3125433.3125448

[^3]: M. Schmidt and E. Zangerle, “Article Quality Classification on Wikipedia,” Proceedings of the 15th International Symposium on Open Collaboration, Aug. 2019. doi:10.1145/3306446.3340831 

## Gantt Chart
![gantt]({{ "/assets/gantt.png" | relative_url }})

## Contribution Table

| Name                 | Contribution |
| ------------------------ | ------ |
| [Ana Silva Carvalho](#)            | ML Algorithms, Dataset Description/Link, Slideshow, GitHub Site     |
| [Remy Bondurant](#)            | Problem Definition and Motivation   |
| [Or Yoked](#)          | Literature Review, Quantitative Metrics   |
| [James White](#)         | Project Goals, Citations, Recording Slides  |
| [Swarna Shah](#)         | Preprocessing Methods, Expected Outcomes  |

## References

<!-- {% highlight ruby %}
def print_hi(name)
  puts "Hi, #{name}"
end
print_hi('Tom')
#=> prints 'Hi, Tom' to STDOUT.
{% endhighlight %} -->

[dataset]: https://figshare.com/articles/dataset/Wiki-Reliability_A_Large_Scale_Dataset_for_Content_Reliability_on_Wikipedia/14113799?file=26648861
