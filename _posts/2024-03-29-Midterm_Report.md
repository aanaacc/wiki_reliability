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
For data preprocessing, we implemented tf-idf on three different Wikipedia editor templates (hoax, more_citations_needed, and unreliable_sources. Before tf-idf, each csv was lemmatized. See tfidf_vectorizer.py, data_preprocessor.py and groundtruth.py for tfidf implementation and general data clean up. 

### ML Algorithms/Models
A Multinomial Naive Bayes was implemented as our first model. We used the vectorized version of all the Wikipedia articles tagged for each template in order to predict whether it was marked as reliable or not. Therefore, Naive Bayes was run three times on an 80/20 data split for each group of articles. See nb.py for Naive Bayes implementation and test/training data split. 
Naive Bayes was selected because it establishes a good baseline as to how learnable the task is. It is also quite simple and inexpensive, making it a good first algorithm to run. 

## Results and Discussion
### Visualizations
Unreliable sources ROC:
![unreliable sources ROC]({{ "/assets/unreliable_resources_roc_curve.png" | relative_url }})
![unreliable sources ROC](/assets/unreliable_resources_roc_curve.png)
Unreliable sources Precision/Recall:
![unreliable sources Precision/Recall](/assets/unreliable_sources_precision_recall_curve.png)

### Quantitative Metrics
* Balanced Accuracy: high ratio of true positives to false positives and negative, ideally >0.7
* F1 score: match or improve existing methods with accuracy ranging from 0.6-0.7 [^2] [^3]
* Area Under the ROC Curve: >0.7

### Analysis of Naive Bayes
The model is expected to at least match or improve the accuracy of previous work. The dataset used is reliable and complete, so we expect a high F1 score and area under the ROC curve, which would characterize a successful Wikipedia article reliability classification.

### Next Steps
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

