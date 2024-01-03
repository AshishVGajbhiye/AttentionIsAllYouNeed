# AttentionIsAllYouNeed

This writing has based on the research paper 'Attention is all you need' publised in 2017 by scholars from google brain, which has completely changed the dimension 
of Natural Language Processing(commonly known as NLP). This paper has worked in better use of attention mechanism toward the improvement of the model called as Transformer.

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
Diagram

The objective was always to understand the context when the sentences are long or to co-relate the long sentences, 
this can be achieved by creating some sort of large and complex Neural Networdk which will have enough number of parameter to learn and retain the relations,
then there is chance that system will be able to understand in more possible way.
Let create a single system where in, on one side there is encoder and on other there is decoder,
encoder take the input and decoder give the output so the definition is not going to change in this 
system.

Diagram

If one encoder can understand the length of the sentences, then why not placed multiple encoder, one will try to understand something and give output to another and then other encoder 
will try to understand other relation and gives output to other, so base architecture uses the 6 set of encoder stack on one other and 6 set of decoder.


Diagram

The initial encoder is of various recurrent neural network(LSTM, GRU, Bi-Directional LSTM), however here it is completely
different, so lets have a look what has been changed in one encoder

Diagram

Every Encoder is composed of two block Feed Forward Neural Network and Self Attention,
feed forward neural network is clear, however what exactly it is Self Attention, lets see:
Take two word My and Name, this is an input and lebel them as X1 and X2.

Since system will not able to undrstand this input, so the next task is to convert them to
numerical representation and it is caled as Embedding, and these embeddings are nothing but 
N dimenstion(vector space) reprsentation of word. So one word can be reprsent in one two thousand vector.

Three things introduce here, Queries, Keys and Values., keeping in mind i will be able to focus
and relate the date, obj is how i will be able to focus on many words and even in that case it does not fail.
Convert this data into Queries, Key and Values, 

lets define weight vector  for queries k and values. Initally these weights will be a random and then they will be trained, deriving this neural networkd as a function. weith will 
learn the relationship in back propogation by minimising the loss.

So first step is to create a query. The input(imbeddings)is passed through the neural 
network the weights used are Wq and proudcing the queries.

2nd step, create a key value, another neural neworkd with different weight matrix.

What about values, here we will use another weight matrix and pass the embedding.
In that way keys value and queries are independent of each other for one particular word.
So for one particular word we are trying to use three different neural network and
trying to proudce some relation, some relations trying to learn.

The thought behind this is:
Generally what we do, if we have the same data like my name is, we create a neural network
like rnn, cnn whatever

i will give less flexibility, less num o independent parameter which can focus on my then , name
then those weight will change and try to learn the coorelation, 
Instead of doing that why not create multiple network with multiple weight matrix
 to adjust in other dimenstions and insted of learing one pattern allowing neural networkd
 to learn other three paterns depends upon input and output. so just to make my earnign 
 flexible and make something independent of each other, so may be one network may 
 not be able to understand the attention correctly but other can find out other attention
 and other neural will try to adjust and tune itself in backward propogation and if not 
 other will try to do that. so just to learn independent relation, different kind of realtin between th data and so 
 queries keys and values has been introduced., and they are just the output of the neural
 network independet of each other. So the question is hwo best possible way to buld the
 relation between different words.

  So lets move on to other step:
 Calculate Score:
 Rational: So far we were trying to create independent vector q, k and v and there 
 is no relation between them at all, now its time to understand what is the relation
 between my and name, or my is dependent on name or other data or something else.
So to do that q1 *k1

Diagram: multiplication

IF it is not able to learn something, if it is not able to train the weight
 then try to skip this particular path and try to send the input to addition and 
 normilization. add and normilization, addidion is normal additon and
 Normilization is bring donw data to a particular scale
Diagram of vector.

