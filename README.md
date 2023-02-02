In common sense, question answering tasks, how well does a model differentiate the entities in each sentence sample? To start thinking about what's going on, we know it represents input text in a rich and complex feature vector. The simplest word vectors learn co-occurence probabilities between words and represent each word within context with every other word. Better embeddings use the maximum space allowed to represent words as far away from each other as possible. Does the fact that similar words are represented similarly perhaps lead a model to become more confused in question answering tasks, where a human wouldn't?

When Roberta trains on Winogrande, how is it able to differentiate the different words in its task? For example, 
> "After swimming in the ocean, the children dried off in the sand. The sand was dry." (True/False)

One thing: The word "dry" way more likely to co-occur with "sand". How does that skew results? But let's try to confuse the model. "Ocean" is represented very differently in vector space than "sand". It should be no problem for the classifier to differentiate those nouns. What happens if we mask the objects, thereby removing the representational advantage these words have. If we use masking terminology that is semantically similar, such as "mask1" and "mask2", will the classifier become confused and guess masked entities randomly?  Do different masking techniques alter accuracy to any noticable degree?

One quick note on why masking is important. In areas of sentiment analysis and common sense reasoning, the model may learn inappropriate relations between subject words and the task. These relations may warp the task. Take for example sentiment analysis on news articles. It may be that subjects related to negative sentiment then bias the model just by their appearance. For example, Trump is correlated with negative sentiment. Masking keeps the model safe from this biasing while allowing us to mine its information. 

We will look at arbitrary masking strings, as malicious as I can imagine them, as well as  using the built in UNKNOWN mask to mask either the subject of the question, or the entity not in the question to test how well the model deals with missing information. Can it tell that two uses of the \<unk\> token refers to the same entity?

I find that the model normally does a fine job regardless of my malicious tests, but some masking techniques are worse than others. However, after one epoch of training on my masking technique, results are not meaningfully different than performance without masks. 

 Read the ipynb for more. Yes, sorry, I know I spelled "Segundo" wrong. That was really low hanging fruit...

![image](https://user-images.githubusercontent.com/9337973/176798553-ca53d6f8-b1ab-46e0-9111-f81cc0a2225f.png)
