# Text Classification


## I. In-class Design

1. **Classification Task**:
The task that will be addressed is the **Sentiment Analysis**.

2. **Dataset**
I will use a dataset of movie reviews: https://www.kaggle.com/datasets/lakshmi25npathi/imdb-dataset-of-50k-movie-reviews
The dataset comes form IMDB (Internet Media Database), contains about 50K reviews in two equally large training and test subsets. It has two columns: review and sentiment
3. **Classes**
The possible labels could be positive, negative and neutral review.
4. **Features**
The text features will be the words.

5. **Model**
I will use Naive Bayes for its simplicity in word association, the idea is to avoid the situation where an unintended feature is detected part of a class, such as the word "film" being detected as a good review. In other words the purpose is to choose which words are used as training sources.

6. **Limitations**
The purpose of using the Naive Bayes method (to separate the words) could lead to polarized reviews, when in reality it couldn't mean it with such an extreme sentiment, this leads to a partialized analysis of the reviews.

7. **Idea**
One idea is to include medium classes for sentiments to give a more diverse range of sentiments.
