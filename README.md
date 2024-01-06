# AttentionIsAllYouNeed

This writing has based on the research paper 'Attention is all you need' publised in 2017 by scholars from google brain, which has completely changed the dimension 
of Natural Language Processing(commonly known as NLP). This paper has worked in better use of attention mechanism toward the improvement of the model called as Transformer.

![487-4875552_transformer-jpeg-en-png-transparent-ratchet-transformers-michael png](https://github.com/AshishVGajbhiye/AttentionIsAllYouNeed/assets/53076609/92e2b69f-babd-4e93-b088-5fd1dacadaaf)

## Why Transformer

Issue with attention model based on encoder and decoder:
If the length of the input increase beyond certain limit lets say for eg. 50 or 70 words, then
it does create a issue, issue how to focus and on which word to focus so that model can
a give a accurate translation, or give some kind of answer if you are trying to build
QnA  model.

So it has some limitiation beyound that it will not be able to perform as per expectation.
So the Transformer try to eliminate the existing problem of Attention based model,
and it is state of architecture.
All other model like GPT, GPT3, BERT, BARD etc are derived from it, albiet with dozens of stacked transfomers.

So lets try to wrap each and every arrow and block of below architecture one by one.
![1*CUeVcFFBclKsH504JraLQg](https://github.com/AshishVGajbhiye/AttentionIsAllYouNeed/assets/53076609/735e356c-6351-4efb-8ef0-1d40fb9d0c7a)

The objective was always to understand the context when the sentences are long or to co-relate the long sentences, 
this can be achieved by creating some sort of large and complex Neural Networdk which will have enough number of parameter to learn and retain the relations,
then there is chance that system will be able to understand in more possible way.
Let create a single system where in, on one side there is encoder and on other there is decoder,
encoder take the input and decoder give the output so the definition is not going to change in this 
system.

![hld](https://github.com/AshishVGajbhiye/AttentionIsAllYouNeed/assets/53076609/0b23dfd9-73bb-41f3-85d3-019ddad70ee8)


If one encoder can understand the length of the sentences, then why not placed multiple encoder, one will try to understand something and give output to another and then other encoder 
will try to understand other relation and gives output to other, so base architecture uses the 6 set of encoder stack on one other and 6 set of decoder.

![Eight](https://github.com/AshishVGajbhiye/AttentionIsAllYouNeed/assets/53076609/aea1c612-79c8-4686-84ab-f033df607568)


The initial encoder is of various recurrent neural network(LSTM, GRU, Bi-Directional LSTM), however here it is completely
different, so lets have a look what has been changed in one encoder

![multifeed](https://github.com/AshishVGajbhiye/AttentionIsAllYouNeed/assets/53076609/a6e7e252-10ae-47bd-be04-27e681e0143d)

Every Encoder is composed of two block Feed Forward Neural Network and Self Attention,
feed forward neural network is like any other neural network, however what exactly is Self Attention here, lets see:
Take two word 'I' and 'am', this is an input and label them as X1 and X2.

Since system will not able to understand this input, so the first task is to convert them to
numerical representation which is called as Embedding, and these embeddings are nothing but 
N dimenstion(vector space) representation of word. 

![Untitled Diagram-Embedding](https://github.com/AshishVGajbhiye/AttentionIsAllYouNeed/assets/53076609/bad0ae17-365b-4b4a-ae87-f86e9899ba6c)

So one word can be represent in N number of vector depends upon use case, 
however here the dimension of embedding is 512 (array), so one word is represented by 512 numbers.

![embeddings](https://github.com/AshishVGajbhiye/AttentionIsAllYouNeed/assets/53076609/86a1c25b-64ce-419c-998c-a9f3e14653bd)


So until here we are taking input ('I' and 'Am') and converting them to embeddings(numerical representations), i.e Encoder receiving the vectors as Input

Three things introduce here, Queries, Keys and Values., keeping in mind it  will be able to focus
and relate the data, objective here is very simple, how it will be able to focus on many words and even in that case it does not fail.
Convert this data into Queries, Key and Values, 

lets define weight vector  for queries k and values. Initally these weights will be a random and then they will be trained, deriving this neural networkd as a function. weith will 
learn the relationship in back propogation by minimising the loss.

####
So first step is to create a query.
The input(imbeddings) 'I' word is passed through the neural network the weights used are Wq and proudcing the queries and this is refered as q1
similarly pass the word 'Am' and generate q2

####
2nd step, create a key value k1 and k2, like query we will use another neural neworkd and pass I and AM however with different weight matrix i.e. Wk.

What about values(v1 & v2), here we will use another weight matrix Wk and pass the embedding.
In that way keys, value and queries are independent of each other for one particular word.
So for one particular word we are trying to use three different neural network and
trying to proudce some relation, some complex relations trying to learn.

The thought behind this is:
Generally what we do, if we have the same data like 'I' , 'am', we create a neural network
like rnn, cnn or whatever., since we know that weight is the function of neural network and same weights were used for all these word, if we have the same nerual network
it will give less flexibility, less num of independent parameter which can focus on 'I' then 'am' and
then those weight will change and try to learn the coorelation.
Instead of doing that why not create multiple network with multiple weight matrix
 to adjust in other dimensions and instead of learing one pattern allowing neural network
 to learn other three paterns depends upon input and output. so just to make my learnin 
 flexible and make something independent of each other, so may be one network  
 not be able to understand the attention correctly but other can find out other attention
 and other neural will try to adjust and tune itself in backward propogation and if not 
 other will try to do that. So just to learn independent relation, different kind of realtion between the data and so 
 queries, keys and values has been introduced., and they are just the output of the neural
 network independet of each other and that way system is allowing itself to learn many pattern.
 So the question is how best possible way to build the relation between different words.

##### 
So lets move on to other step:

Calculate Score: This is another atribute

Rational: So far we were trying to create independent vector q, k and v and there 
is no relation between them at all, now its time to understand what is the relation
between 'I' and 'AM', or 'I' is dependent on 'AM' or other data or something else.
So to do that lets multiply q1 *k1, infact q1*k1 is dot product or vector multiplication
q1*k1 = 12, q1*k=21

Diagram: multiplication

#### Next step is to divide the score by 8 which is nothing but dimension of key and calculate the Softmax

Diagram

Since softmax is we can say that I word is more related to AM than by itelf, that is intution we are getting by whatever hardcode value we have taken, that way
we are trying to see on which word it is focusing more.
Lets we have few more words in the sentence like "I am learning hindi" so we will have x3=learning, x4=hindi, q3, q4, k3, k4, v3 and v4.
So we will calculate score q1*k3, q1*k4 and softmax for all of these.
In case of 'Am' word we will calculate q2*k1, q2*k2, q2*k3, q2*k4. So for 4 word, 4 softmax will be calculated for single word like 4 softmax for I, 4 softmax for AM and same for learning and hindi.
So if there are 10 word in the sentence then for every word there will 10 softmax, becasue we have to find the relation of one word with all, 2nd word with all 10, 3rd word with all 10 and so n so forth.
Rational: Softmax score determines how much focus each words at this position.

The next calculation is to multiply each value vector by the softmax score and sum up all the value vector.
Diagram:
So Z1 is for I word and Z2 is for AM word, so here the whole thing is how we will try to create a function which will try to relate it each and every word and still focus on one word or other word or many word. 

#### Multi-Headed Attention
Until now above we have seen one neural netword is used each to generate the query, key and value, however in original architecture the Transformer uses eight attention heads, so we end up with eight sets for each encoder/decoder.
And this improves the performance of the attention in two ways-
1. Add more flexibility to focus on  different position of the words by understanding the context in much better way
2. By understanding the full stop, exclamation mark and its importance and relation to the words

#### Positional Encoding
If we look at the architecture the input to the attention layer is Embedding along with positional encoding, lets go over what exactly is positional encoding:
To understand the order of words and understand the focus the transformer adds a vector to each input embeddings, that vector is nothing but the position of word in the sentence and follows
a specific pattern that model learns and helps it determinte the position of each word and distance between different word in the sentence.
The rational here is that addition of these position or vector along with embeddings is to provide meaningful distances between the embeddings vectors once they are used to generate the
queries, key and value.

### Addition and Normalization
If we look closely to the architecture then right after positional encoding one arrow goes to Add & Norm block, which is nothing but the skip connection (ResNet concept), so the rational here 
is if multiheaded connection which is nothing but a neural network is not able to learn something, if it is not able to train the weight or if there is nothing to train/change the weight or if system is not able to minimize the loss then try to skip this particular step and send dataset directly to Addition and Normalization.
Addition is normal addition operation (X1+Z1 for e.g.) and Normalization is to bring down the data in between particular scale.

### Feed Forward Network
The data moved over to the next block i.e. Feed Forward Network again it will have n numbers of layers, numers of hidden units will be present and then again it will send data to Addition and Normalization layer.

With this Encoder part is Done! (left hand side of the architecture)

The output from this encoder or from this entire neural network can be used for various task like sentence classification or may to generate new data ortext or new word.

### Practical Usage:
Bidirectional Encoder Representation from Transformer is a LLM (large language module) is encoder based transfomer model introduced in 2018 by Google

Add a output layer or softmax function and it can used as a classification and can be used for any task like tokenization generation.

If we talk about GPT, it is completely based on Decoder which has been (GPT 3) trained on 1.7 B parameters.


Now let's come to the other side of the Architercture i.e Decoder.

#### Decoder
-----------------
The simple role of the decoder is provide the outcome

The output from the Enocder which we can say query, key and value and pass the entire output to Multi-Head Attention block of Decoder, plus output from 'Masked Multi-Head Attention' block.
So what is the Masked here..It is nothing but hide some information or detail and send it to the network, the rational behind is to check whether my network is capable enough to generate that hidden information or not, so this is one change on decoder part.

Decoder will try to give the final outcome, now whatever outcome it is going to give you for sure it need classification or probability of occurence of data for that reason a simple linear neural network is placed and logit function of softmax or probaitliyt function as a softmax so that i ca tel you final classificaiton for whtever the word we have.

