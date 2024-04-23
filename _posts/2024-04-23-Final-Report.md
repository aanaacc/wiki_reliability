---
layout: post
image_sliders:
  - slider1
  - slider2
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
Random Forest was the second model implemented. It consisted of the same preprocessed data and test/train split mentioned before. See CNN.py for the Random Forest implementation. Random Forest was chosen because it is known to offset bias and overfitting often found in singular decision trees. 
Lastly, the third model that was implemented was a Convolutional Neural Network. CNNs have historically captured semantic features well, which is a contrast to the two other models we have implemented so far.

## Results and Discussion: Visualizations

### Naive Bayes Visualizations
{% include slider.html selector="slider1" %}

### Random Forest Visualizations
{% include slider.html selector="slider2" %}

### CNN Visualizations

## Results and Discussion: Quantitative Metrics

### Naive Bayes
* F1 Score = 0.4391
* Balanced Accuracy = 0.3746
* Area Under ROC Curve = 0.3280
* All three metrics are much lower than our goal of around 0.7. The model has low precision and recall as shown by the low F1 score, low classification accuracy as the low balanced accuracy indicates, and the low AUC score meaning the model performs similarly to a random classifier.

### Random Forest
Hoax Metrics:
* Scores Mean = 0.2936
* F1 Score = 0.2872
* Balanced Accuracy Score = 0.2675
* Area Under the ROC Curve = 0.1959

More Citations Metrics:
* Scores Mean = 0.2784
* F1 Score = 0.2092
* Balanced Accuracy Score = 0.2078
* Area Under the ROC Curve = 0.1378

Unreliable Sources Metrics:
* Scores Mean = 0.3066
* F1 Score = 0.2893
* Balanced Accuracy Score = 0.2650
* Area Under the ROC Curve = 0.2016

### CNN


## Results and Discussion: Analysis of Models

### Naive Bayes
The accuracy of the Naive Bayes model was 37.38%. One possible reason that the model performed poorly could be the lack of sufficient training data. The smallest data set, hoax, only contained about 2700 tokens after running TF-IDF which may not be enough for Naive Bayes to correctly find correlations in the data for accurate classification. Another reason may be that our chosen preprocessing method, TF-IDF, does not include any semantic relationships in the text which could improve the classification accuracy.

### Random Forest
The average accuracy of the random forest model was about 24.6%, which is significantly lower than 50%, the accuracy of a random classifier. The confusion matrices indicated many more false positives and false negatives than correct classifications, which is also shown by the low F1 score, balanced accuracy score, and AUC. All of the quantitative metrics used were much lower than we anticipated. The poor performance may be because the data was too sparse to use Random Forest. Another possibility is that this method cannot include any semantic nuances in the classification, which could have potentially improved the classification accuracy.

### CNN

## Results and Discussion: Comparisons of Models
Each of the models used presented different challenges and results with regards to the data. Naive bayes and random forest both performed similarly with accuracies around as low as 20%. CNN performed “better” but still came out to an accuracy of about 51%. Looking at these accuracies it is clear that the model did not learn anything from the given data. The CNN model is almost as accurate as flipping a coin, and naive bayes and random forest are even less accurate. There are many points of failure in our methodology that could have led to this outcome. One possibility is that there is an error in the way the data was preprocessed, either during the cleaning phase or the TF-IDF phase. Another possibility is that the algorithm used to turn the data from text to numbers was not useful for this specific situation. We used TF-IDF but there is a chance that another algorithm would have organized the data in a way that would have allowed our models to learn a pattern from the data. Finally, it is possible that trying to classify Wikipedia articles based on the text within is not a problem that can be learned by relatively simple algorithms such as the ones used in this project.

## Next Steps
The next step in this project would be to try to improve the model accuracy by using a different preprocessing method than TF-IDF. One option is to use a method that includes semantic relationships between words instead of just the occurrence frequency of each word, which may improve the model’s ability to learn the data. We would test that method using CNN since out of the three models that we used, CNN had the best performance. We could also choose another model to train the data on, since fine tuning the parameters of each model has not been successful.

[^1]: K. Wong, M. Redi, and D. Saez-Trumper, “Wiki-Reliability: A large scale dataset for content reliability on Wikipedia,” Proceedings of the 44th International ACM SIGIR Conference on Research and Development in Information Retrieval, Jul. 2021. doi:10.1145/3404835.3463253

[^2]: Q.-V. Dang and C.-L. Ignat, “An end-to-end learning solution for assessing the quality of Wikipedia articles,” Proceedings of the 13th International Symposium on Open Collaboration, Aug. 2017. doi:10.1145/3125433.3125448

[^3]: M. Schmidt and E. Zangerle, “Article Quality Classification on Wikipedia,” Proceedings of the 15th International Symposium on Open Collaboration, Aug. 2019. doi:10.1145/3306446.3340831 

## Gantt Chart
![gantt]({{ "/assets/gantt.png" | relative_url }})

## Contribution Table

| Name                 | Contribution |
| ------------------------ | ------ |
| [Ana Silva Carvalho](#)            | ML Algorithms/Model, GitHub Site, Slide Deck     |
| [Remy Bondurant](#)            | Data Preprocessing, Comparisons   |
| [Or Yoked](#)          | Visualizations, Gantt Chart, Quantitative Methods, Video   |
| [James White](#)         | Data Preprocessing, ML Algorithms/Model, Metrics  |
| [Swarna Shah](#)         | Quantitative Methods, Analysis of ML Algorithms/Models, Next Steps  |

## References

<!-- {% highlight ruby %}
def print_hi(name)
  puts "Hi, #{name}"
end
print_hi('Tom')
#=> prints 'Hi, Tom' to STDOUT.
{% endhighlight %} -->

[dataset]: https://figshare.com/articles/dataset/Wiki-Reliability_A_Large_Scale_Dataset_for_Content_Reliability_on_Wikipedia/14113799?file=26648861


