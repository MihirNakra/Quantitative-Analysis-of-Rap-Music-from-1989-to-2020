# Quantitative Analysis of Rap from 1989 to 2020

by Parth Wokhlu and Mihir Nakra 

# I. Introduction

After spending the past year delving into every era of rap music, the intricacies of the genre and its change became extremely intriguing to us. We were interested in quantifying how rap music has evolved over the past 30 years, specifically in regards to its origin, and how that evolution correlates to African-American culture. Specifically, an article, titled "How Polticial Hip-hop Has Evolved Over Time" by Dan Runcie, explains that the style of music was created as a way to express the oppression experienced by underrepresented African-Americans. Since then, there's been a wide consesnsus that the themes of systemic racism, police brutality, and generational poverty have fallen out of rap music, so we decided to use deep learning to find a correlation between changes in the content of hip hop and racial injustices.


# II. Methodology

All the code for this project is open sourced (not all of it is written completely by us, so please give the original authors their due credit).

## Data Collection
The first step was collecting the names of all the popular rap songs of the past 30 years. Because Billboard had not started a "Hot 100" List for Rap in its earlier eras, we began by taking songs from the weekly charts that have been updated since March of 1989. We used [Allen Guo’s Python API](https://github.com/guoguo12/billboard-charts) for retrieving the song and artist names and saved them to a json file, sorting them by the year that they were on the charts. The full list of the yearly top rap songs can be found in the file named “rapData.json”. 
After that testing data was compiled, we then had to go through the most gruesome process: collecting training data. Using Google and our own playlists, we came up with 75 songs stretching across every era that were good examples of rap music that discussed systemic inequalities. Then, we repeated the same process for 75 songs that discussed any content besides anti-black oppression. The full list of training data can be found in the “master song database.csv” file. We switched around the training data for different trials in order to make sure there was consistency within the results. 

## Neural Network
At first, the idea of a neural network seemed like a far off possibility. It seemed interesting, but neither of us had any idea what it actually was. As we delved into the topic, we found numerous [YouTube videos](https://www.youtube.com/watch?v=aircAruvnKk&feature=youtu.be) and [articles](https://news.codecademy.com/taylor-swift-lyrics-machine-learning/) that allowed us to wrap our head arounds this topic. 

From what we understood, the method we should attack this problem with was to classify a song based on the lyrics using a linear support vector machine. This method had a fast computational time and could provide accurate results without thousands and thousands of training inputs. Essentially, a linear support vector machine is made to mathematically determine a hyperplane which will allow it to classify data points. A hyperplane is, to put it simply, a line of best fit for the data with a margin outside of it. The calculations done by the machine create a hyperplane with the largest margin possible so that data can be classified as accurately as possible. 

So now we have the hard part: how do we turn words into data points for the machine to use? The method we used was implementing a count vectorizer, which creates a matrix using the words given. 

![Example of count vectorizer matrix](https://kavita-ganesan.com/wp-content/uploads/how-hashingvectorizer-works.png)

From the matrix, we used something called a tfidf transformer to allow the machine to get a better understanding of what words matter. A tfidf transformer highlights the words that are unique to certain songs and helps to reduce the influence of a word like “the,” which appears likely in all songs numerous times. After applying these calculations to our text, we gave the training data to the model and allowed it to determine the hyperplane. To do all of this, we used the python sklearn library.

To determine the accuracy of our training data, we split it up so that 70% of it would be used to train and then 30% of it would be used to test. We would then train the model with that 70% and tell it to predict the themes of the song of the remaining 30% of the songs. Then we would compare the data it predicted to what we know it should’ve predicted. We tested it many times, and it had an average accuracy of about 85%. 

After determining our model was fairly accurate, we could use it to predict the themes of all the songs we had. Each time we wanted to predict if a song had themes of racial injustice or systemic racism in it, we could give that model the count vectorized and tfidf transformed song lyric, and using the already determined hyperplane, it would identify where the song lyrics would lie on the graph in relation to the hyperplane. Based on that it would tell us if a certain song contained the ideas of racial injustice or not. 

The credit for providing us with the design of this model goes to [Shanglun Wang](https://www.toptal.com/machine-learning/nlp-tutorial-text-classification), who made another linear support vector machine to classify wine reviews. He was kind enough to open source the code and explain it thoroughly, which allowed us to understand and adapt it to our needs.


## Implementing the Code
Now that we had an accurate model and the required testing and training data, the rest of the code was pretty simple. The syntax for the class can be found under the title of “mainSVC.py”. After training the model on the given data, it was time to run it through the rap lyrics of the past 30 years. We did this by utilizing [John Miller’s Genius API](https://github.com/johnwmillr/LyricsGenius), which is a website that stores the lyrics of nearly every song we needed. 

From there, the process was standard. We created a for loop to stop when the year the AI was analyzing was equal to 2021 and established a new count of songs the computer deemed as about racism, and the total number of songs. At the end of processing the songs for the respective year, the computer returned the percentage of songs it thought discussed racism, and we put it into our data. This cycle repeated until we had quantified the content of rap song for every year of every era (see more details about results in the next section). 

## Limitations/Flaws
The first limitation of this study is the most obvious: we’re two high schoolers that conducted this “experiment” within winter break, there’s a relatively moderate margin of error.

Second, this project isn’t reflective of every rap song created, only the most popular, as we pulled the songs from the Billboard charts. Hypothetically, there could be the same amount of songs about systemic racism being created, but people are simply listening to other topics more. This distinction is especially key when realizing that during the early 2000s, hip-hops audience grew massively to non-black people with artists like Ms. Lauryn Hill and Eminem. 

Third, institutional racism is a system that influences every aspect of the lives of the people who it affects. For example, a song about drug dealing and robbing a bank is still directly linked to policies like the War on Drugs and redlining, but our AI may not pick it up.


# III. Results


# IV. Conclusion and Implications 


