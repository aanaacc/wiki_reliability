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
Unreliable Sources:
![unreliable sources ROC]({{ "/assets/unreliablesources_roc_curve.png" | relative_url }})
![unreliable sources Precision/Recall]({{ "/assets/unreliablesources_precision_recall_curve.png" | relative_url }})
![unreliable sources Confusion Matrix]({{ "/assets/unreliablesources_confusion_matrix.png" | relative_url }})

More Citations Needed:
![more citations ROC]({{ "/assets/morecitations_roc_curve.png" | relative_url }})
![more citations Precision/Recall]({{ "/assets/morecitations_precision_recall_curve.png" | relative_url }})
![more citations Confusion Matrix]({{ "/assets/morecitations_confusion_matrix.png" | relative_url }})

Hoax:
![hoax ROC]({{ "/assets/hoax_roc_curve.png" | relative_url }})
![hoax Precision/Recall]({{ "/assets/hoax_precision_recall_curve.png" | relative_url }})
![hoax Confusion Matrix]({{ "/assets/hoax_confusion_matrix.png" | relative_url }})



### Quantitative Metrics
Hoax Metrics:
* F1 Score = 0.4391
* Balanced Accuracy = 0.3746
* Area Under ROC Curve = 0.3280
* All three metrics are much lower than our goal of around 0.7. The model has low precision and recall as shown by the low F1 score, low classification accuracy as the low balanced accuracy indicates, and the low AUC score meaning the model performs similarly to a random classifier. 

### Analysis of Naive Bayes
The accuracy of the Naive Bayes model was 37.38%. One possible reason that the model performed poorly could be the lack of sufficient training data. The smallest data set, hoax, only contained about 2700 tokens after running TF-IDF which may not be enough for Naive Bayes to correctly find correlations in the data for accurate classification. Another reason may be that our chosen preprocessing method, TF-IDF, does not include any semantic relationships in the text which could improve the classification accuracy.

### Next Steps
In regards to improving our classification of the three templates, hoax, more citations needed, unreliable sources, we want to fine tune our Naive Bayes algorithm such as changing parameters or experimenting with different variations of the method. The goal is to raise the accuracy score and ROC AUC so it will be around 0.7 for both. However, it seems there is not enough training data to find patterns based on the tf-idf method, which generated around 27000 tokens for the hoax and more citations needed templates and only 14000 for the unreliable sources template, so we will need to consider other ways to achieve more diverse training data. In addition to enhancing our current method, our next step is implementing a Random Forest algorithm as well as a Gradient Boosted Trees. These may be more fitting for the classification due to handling more complex relationships in the data compared to Naive Bayes. In addition, we might want to explore CNN as it may yield better results for this type of task, but it will require a larger dataset for training in order to capture hierarchical relationships.

[^1]: K. Wong, M. Redi, and D. Saez-Trumper, “Wiki-Reliability: A large scale dataset for content reliability on Wikipedia,” Proceedings of the 44th International ACM SIGIR Conference on Research and Development in Information Retrieval, Jul. 2021. doi:10.1145/3404835.3463253

[^2]: Q.-V. Dang and C.-L. Ignat, “An end-to-end learning solution for assessing the quality of Wikipedia articles,” Proceedings of the 13th International Symposium on Open Collaboration, Aug. 2017. doi:10.1145/3125433.3125448

[^3]: M. Schmidt and E. Zangerle, “Article Quality Classification on Wikipedia,” Proceedings of the 15th International Symposium on Open Collaboration, Aug. 2019. doi:10.1145/3306446.3340831 

## Gantt Chart
![gantt]({{ "/assets/gantt.png" | relative_url }})

## Contribution Table

| Name                 | Contribution |
| ------------------------ | ------ |
| [Ana Silva Carvalho](#)            | ML Algorithms/Model, GitHub Site     |
| [Remy Bondurant](#)            | Data Preprocessing  |
| [Or Yoked](#)          | Visualizations, Next Steps, Gantt Chart   |
| [James White](#)         | Data Preprocessing  |
| [Swarna Shah](#)         | Quantitative Methods, Analysis of ML Algorithms/Models  |

## References

<!-- {% highlight ruby %}
def print_hi(name)
  puts "Hi, #{name}"
end
print_hi('Tom')
#=> prints 'Hi, Tom' to STDOUT.
{% endhighlight %} -->

[dataset]: https://figshare.com/articles/dataset/Wiki-Reliability_A_Large_Scale_Dataset_for_Content_Reliability_on_Wikipedia/14113799?file=26648861

