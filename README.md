# Depression Detection Using Twitter Data
Depression Detection using Twitter data

1. [Project Motivation](#motivation)
2. [Proposed Model](#proposedModel)
2. [Dataset Construction](#dataset)
3. [Project Phases](#phases)
4. [Installation](#installation)
5. [Files Description](#filesdiscription)
6. [Future Plan](#futureplan)
7. [Contributors](#contributors)
8. [Recources](#recources)



## Project Motivation <a name="motivation"></a>

As the society becomes more and more technically advanced, we are tuning more into the online world. But as a result, some people can feel more isolated and this can in turn increase the occurrence of anxiety and depression.

Ironically, some people turn to social media to outlet their thoughts and emotions, and platforms like twitter, offers users a level of anonymity, which can entice the user to be more uninhibited in their expressions.

This offers an opportunity for emotional detection of users based on their tweets. From the medical perspective, it provides a good opportunity to identify potential depression in the users and from there offer suitable support and assist them to a path of recovery, by introducing them to self-care chatbots such as woebot, that uses Cognitive Behavioral Therapy to help its users change their negative thought patterns, as well as providing friendship in their time of need.

We also aim to provide a dataset that is specifically designed for depression identification based on tweets. Our research so far shows such data is not readily available, and proves to be a major stumbling block in the development of this project.

## Proposed Model <a name="proposedModel"></a>

Our depression detector can be incorporated into existing products such as GBoard on Android, the Google Keyboard, which uses federated learning to improve the user experience based on their search history . As GBoard already collects user history, it is conceivable it can be extended to incorporate our model and identify instances of depression, especially based on user´s textual input over a period of time.

If signs of depression has been detected, then it would be desirable to suggest the user to use a self-care chatbot. (we need to think of a way to do this without infringing on the user's privacy, for example, we do not want to send this diagnosis back to the server in its raw form) Perhaps the suggestion of self-care bot can be an automatic feature that is integrated into GBoard upon depression detection, so that the raw data does not need to go back to the centralised server, and does not require revelation of the user's identity. Here we may implement federated learning along with local differential privacy, to ensure the user~s privacy is protected.

We also aim to provide a dataset that is specifically designed for depression identification based on tweets. Our research so far shows such data is not readily available, and proves to be a major stumbling block in the development of this project.

-- a diagram -- 


##  Dataset Construction <a name="dataset"></a>

Dataset construction turned out to be the biggest piece of work in our project.

Initially we used data from an existing github repository [Detecting-Depression-in-Tweets](https://github.com/viritaromero/Detecting-Depression-in-Tweets), which has the same purpose of detecting depression in tweets. However, our initial model was able to achieve over 99% accuracy during validation, because the data was too simplistic and most of the labelled depressive entries contain the word **depression**.

So we decided to create our own twitter dataset for depression by using the third party tool, [TWINT](https://github.com/twintproject/twint).


### Collecting data   

We constructed a script (data_scraper.ipynb) to apply the following steps to identify potentially depressive tweets:
1. Used twint to collect tweets based on the following hashtags
-    #depressed
-    #depression
-    #loneliness
-    #hopelessness1. 

2. Remove duplicated entries based on tweet id.

3. Remove entries that contain these positive or medical or educational sounding hashtags
-   #mentalhealth
-    #health
-    #happiness
-    #mentalillness
-    #happy
-    #joy
-    #wellbeing1. 

4. Remove entries with any of the following characteristics, as they are more likely to be promotional messages
 -  Containing more than three hashtags
-   Containing @mentions
-   Containing URLs

5. Remove entries with less than 25 characters, or 5 words.

6. Lastly, remove all hashtags from the tweets. This is because the hashtags themselves are an obvious indicator of depressive text, and we would like to train our model to focus on the content of the tweet rather than the existence of depressive hashtags.


The results are saved into csv files and allocated to our team members for review.


### Reviewing dataset

We manually reviewed csv files generated by the previous script, which contain filtered tweets that originally contained depressive hashtags. The csv files have a target column set to 1 by default, and we manually set the non-depressive entries to have target of 0, and also removed non-English tweets from the file.

The resulting csv files contain roughly 50-50 split of depressive and non-depressive tweets. This is a good resource to train our model on, as all of the tweets originally had depressive hashtags, so by distinguishing the tweets based on its content rather than tags, we are training the model to be more sensitive to the content and more precise in its predictions.


### More CLearning

We also collected additional tweets from other sources, to represent non-depressive texts. These contain other emotions, such as joy, love, surprise, as well as some emotionally neutral tweets. 

### Finalizing Dataset
Combine the datasets from Part 3 and Part 4 to create a final dataset



Even though the dataset creation took a lot of time and effort, we believe that it was really important to get this right, as this is the basis of creating an accurate depression detector and potentially differentiate it from just a sentiment detector.


![Positive words](https://user-images.githubusercontent.com/14244685/63386084-108a0d80-c3c4-11e9-8735-77afc986cc33.png)
![negitive words](https://user-images.githubusercontent.com/14244685/63386087-108a0d80-c3c4-11e9-9796-588ce316ed70.png)





## Installation<a name="installation"></a>

## Files Description<a name="filesdiscription"></a>


## Future Plan<a name="futureplan"></a>

- Use an external software such as liwc (http://liwc.wpengine.com/) to review the linguistic and emotional content of the tweets, and verify that the labels are correct.



## Contributors<a name="contributors"></a>

Contributor | Slack Handle
------------ | -------------
Susan Wang | @SusanW
Labiba Kanij Rupty | @Labiba 
Mahfuza Humayra Mohona | @Mohona 
Aarthi Alagammai | @Aarthi Alagammai
Munira Omar | @Munira Omar
Marwa Qabeel | @Marwa

![Team depression-detection](https://user-images.githubusercontent.com/14244685/63355476-00543d00-c388-11e9-961c-71f4bc01162b.png)

## Resources<a name="resources"></a>
- Anne Bonner's Medium article [You Are What You Tweet](https://towardsdatascience.com/you-are-what-you-tweet-7e23fb84f4ed).
- [Sentiment Analysis — TorchText](https://medium.com/@sonicboom8/sentiment-analysis-torchtext-55fb57b1fab8)
- Pranjal Chaubey repo [Sixty AI](https://github.com/pranjalchaubey/Sixty-AI)



