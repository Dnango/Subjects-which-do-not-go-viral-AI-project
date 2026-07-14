# Subjects-which-do-not-go-viral-AI-project
Final project for the Building AI course


## Summary

Social media are all about topics or content going viral. But what is actually left behind? What stays there in the trenches of SM? That is what this project is about; to figure out what content is not going viral and  any commonalities in that content. Let's say there are patterns, then this project hopes to find these patterns. Let's see if we can give a voice to the unheard ;-)


## Background

On social media it is all about the winner, the one that got the most views, likes or other. This is coherent to a certain world view where the loudest, the best, the most competitive succeed. But in a real social environment or construct it is much more complex, it works more like a soccer team, you have all kinds of teamplayers and not just the one that scores but those who defend or distribute the ball to other tactically. If I look at my own social environment there are thos who are good at selling there stories, there those who are more in the back ground but good at ideating, or asking questions, those who are good at organizing and distributing roles or tasks, and those that will really florish only when there is a emergency, etc. So can we find the same patterns in social media intereactions and make those visible?

In the bigger picture but out of scope for this project. In order for people to have a more diverse view on social interactions it could help (assumption) if social media allow for a more diverse role play (like mentioned above) of interactions, but because of the current main stream model this is not of interest to a lot of the social platforms. What can be learned from an analysis of that what is "forgotten" quickly?



Suspected problems:
* Defining what is "unpopular"? When is some content on a social media platform unpopular: is it based on likes, shares, views or a combination of? What is the threshold for these?   
* Hypothesis: since media are aimed at creating the most attractive and responsive content in order to attracked the most people, certain topics will be naturally blanked out.
* Hypothesis 2: since media are culturally and therfore regionally biased certain content might be underprefferd by the system
* Hypothesis 3: social media might be pilotically biased and being use to emit a certain world view by preferring certain stories over other. 
* It is questionable if the relevant data is going to be comprehensive enough to find anything relevant patterns related to the topic above


## How is it used?

The algorythm can be run on social media data to find patterns on content that is impopular and find different types categories in content and of roles in having content impoluar (or popular).

![Bored person](https://upload.wikimedia.org/wikipedia/commons/6/6a/Bored_Cartoon_Man_Using_A_Computer.svg)

Code example:
```
# Chap02-03/twitter_term_frequency.py from https://github.com/bonzanini/Book-SocialMediaMiningPython
import sys
import string
import json
from collections import Counter
from nltk.tokenize import TweetTokenizer
from nltk.corpus import stopwords

def process(text, tokenizer=TweetTokenizer(), stopwords=[]):
    """Process the text of a tweet:
    - Lowercase
    - Tokenize
    - Stopword removal
    - Digits removal

    Return: list of strings
    """
    text = text.lower()
    tokens = tokenizer.tokenize(text)
    # If we want to normalize contraction, uncomment this
    # tokens = normalize_contractions(tokens)
    return [tok for tok in tokens if tok not in stopwords and not tok.isdigit()]

def normalize_contractions(tokens):
    """Example of normalization for English contractions.

    Return: generator
    """
    token_map = {
        "i'm": "i am",
        "you're": "you are",
        "it's": "it is",
        "we're": "we are",
        "we'll": "we will",
    }
    for tok in tokens:
        if tok in token_map.keys():
            for item in token_map[tok].split():
                yield item
        else:
            yield tok

if __name__ == '__main__':
    tweet_tokenizer = TweetTokenizer()
    punct = list(string.punctuation)
    stopword_list = stopwords.words('english') + punct + ['rt', 'via']

    fname = sys.argv[1]
    tf = Counter()
    with open(fname, 'r') as f:
        for line in f:
            tweet = json.loads(line)
            tokens = process(text=tweet.get('text', ''),
                             tokenizer=tweet_tokenizer,
                             stopwords=stopword_list)
            tf.update(tokens)
        for tag, count in tf.most_common(30):
            print("{}: {}".format(tag, count))
```


## Data sources and AI methods
Data is being drawn from external (3rd party) sources. Sources are:

  **Source**               | **Description**                                                                                     |
 |--------------------------|-----------------------------------------------------------------------------------------------------|
 | [Twitter API](https://developer.twitter.com/en/docs) | Real-time and historical tweets. | Filter by **low engagement**                |
 | [Pushshift (Reddit)](https://pushshift.io/) | Historical Reddit posts/comments. | Filter by **low upvotes**                          |
 | [Mastodon API](https://joinmastodon.org/servers) | Decentralized, privacy-focused alternative to Twitter. | Filter by **low engagement**          |

## Challenges

* Getting stuck on details 
* Not being able to filter out one off content without infringing privacy rights
* Scope being to large in order to provide specific outcomes (see below)

This project does not interpret what outcomes mean in terms of the data and data-sources it is drawing data from. It will just aim to find patterns, like in a word-cloud, but then showing the most unpopular topics being most visible.
Therefore it is questionable if hypothesis 2 and hypothis 3 will be (un)proven.

Ethically it is important not have the unpopular topics matched to individuals, or social media accounts... in order to safeguard privacy. This will be challenging since unpopular topics are naturally mentioned by the few.

## What next?
* Approach:
Understanding virallity & defining the MVP
Data gathering / writing data gathering scripts
Development of data pre-processing layer: writing data preparation scripts, incl. handling potential data issues, and programmatically defining technical indicators
Model development, experimenting with various options
Developing an AI based strategy for generating relevant insights (categories, etc.)
Writing clean scripts for implementation

* Further development:
In order to answer hypothesis 2, 3 the project should be specfied further; for instance to "EU Policy Topics Ignored on Social Media". Machine learning methods will need to be ellaborated.
Proper data scientist and python skills would be needed in order to determine if data is properly analysed and outputs are making sense in terms of the hypthesis. Data journalists for the same reasons and to ask the right questions.

## [TODO] Acknowledgments

* Social Media Mining with Python
Repository with code for analyzing Twitter/Reddit data by Marco Bonzanini
Python (tweepy, praw)
Filter and analyze low-engagement posts.
GitHub: https://github.com/bonzanini/Book-SocialMediaMiningPython

* Slapping Cats, Bopping Heads, and Oreo Shakes: Understanding Indicators of Virality in TikTok Short Videos
Chen Ling, Boston University, USA, ccling@bu.edu
Jeremy Blackburn, Binghamton University, USA, jblackbu@binghamton.edu
Emiliano De Cristofaro, University College London, United Kingdom, e.decristofaro@ucl.ac.uk
Gianluca Stringhini, Boston University, United Kingdom, gian@bu.edu
DOI: https://doi.org/10.1145/3501247.3531551
WebSci '22: 14th ACM Web Science Conference 2022, Barcelona, Spain, June 2022

* Bored Cartoon Man using a Computer](https://commons.wikimedia.org/wiki/File:[Bored_Cartoon_Man_Using_A_Computer.svg](Bored_Cartoon_Man_Using_A_Computer.svg#filelinks) / [CC BY 2.0](https://creativecommons.org/licenses/by/2.0)

## Privacy Notice
This project analyzes **publicly available tweets** and does store personal data. All data is anonymized.

## Ethical Use
This project is intended for **educational and research purposes only**. Do not use it for harmful or unethical activities.

## License
This project is licensed under the [MIT License](LICENSE).
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
