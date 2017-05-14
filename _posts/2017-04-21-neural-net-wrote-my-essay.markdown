---
layout: post
title:  "A Neural Network Wrote My English Essay"
date:   2017-04-21
categories: jekyll update
---
As a computer science major in the final semester of my undergrad degree, the ‘senioritis’ has started to set in. Especially when it comes to my writing GE. Unfortunately, without this class I cannot graduate. Thus, I was presented with a very standard optimization problem. Get a high enough grade to pass, with the minimal amount of  writing required. It turns outs that we can define a function:  

<div><center> $$f(w) = \frac{1}{w}$$  </center></div>  

where $$w$$ is the amount of time spent writing and the output, $$f(w)$$, is the happiness I feel. What’s great about this function is that it is continuous and therefore differentiable. Hurray optimization! It turns out that as the hours spent writing approaches zero my happiness level increases infinitely. We should definitely exploit this finding.

How, you ask? With a Long Short Term Memory ([LSTM](http://colah.github.io/posts/2015-08-Understanding-LSTMs/)) network obviously! **Spoiler alert:** I'm training a neural net to write my essay for me.  

First, we'll need to gather lots of training data for our network. My essay is supposed to be a reflective piece on the class as a whole. To accomplish this I used the books we read for class, articles we talked about and numerous samples of my own writing.  

[The Glass Castle](http://english4success.ru/Upload/books/268.pdf)  
[1984](http://www.george-orwell.org/1984)  
[Humans Need Not Apply](http://www.cgpgrey.com/blog/humans-need-not-apply)  
[Jordan Ott](www.jordanott.com)  
[Dr. Seuss](http://www.seussville.com/books/book_detail.php?isbn=9780375851568) is it a crime to want your model to rhyme?  

Once we have our data we can start creating our model. We'll be using a type of recurrent structure called an LSTM. These models are very useful when dealing with time dependent data i.e. current data samples are dependent on prior samples. Feed-forward networks are indifferent to time sensitive data and have no notion of memory. Structuring sentences depends on one's ability to relate current words to previous one.s This is where LSTMs will be very useful.      

I won't go into the low level details of how they work since many others have wonderful explanations of them. We'll use Python and Keras for our implementation which makes it very easy to stack multiple LSTM cells. Initializing our network is very straight forward.

{% highlight python %}
from keras.models import Sequential
from keras.layers import Dense, Activation
from keras.layers import LSTM
from keras.optimizers import RMSprop

model = Sequential()
# set return_sequences=True so we can feed the output of one cell right into another
model.add(LSTM(256,return_sequences=True, input_shape=(maxlen, len(chars))))
model.add(LSTM(256,return_sequences=True))
model.add(LSTM(256))
# add a fully connected layer for our character level predictions
model.add(Dense(len(chars)))
model.add(Activation('softmax'))
# more optimization!
optimizer = RMSprop(lr=0.01)
model.compile(loss='categorical_crossentropy', optimizer=optimizer)
{% endhighlight %}

### Results ###
{% raw %}
~~~
‘No! Not merely to extract your confession, not to punish you. Shall I
tele st te as eers aedr the the  the the th t the fall  the sode and  
and woul happe and the the ald were not and ofr the sary and we he  
I ton wasee o no the so hase t therot an I saugnt he  t he ker  
andhne the  and at was eton Whe the thi as the andile the to the  
ingou and t the the oh wge s ante we whe  the stit an and the and  
of te the the  the bast w the the the fo ande the he wonoth  
stern and animated.
~~~
{% endraw %}
The phrase ```‘No! Not merely to extract your confession, not to punish you. Shall ``` is what is fed to the network to prompt it to generate the resulting paragraph. Everything that follows was produced by the LSTM. I think what's very interesting about this is if you glance very quickly at it you can't tell that it's complete gibberish. The network learns proper spacing, punctuation and even spells a few words correctly.  

You can find my full "essay" [here]({{ site.url }}/assets/results.txt). I hope my professor likes it!

### Moving Forward ###  

Character level LSTMs are nice and pretty efficient but when it comes to generating meaningful text they might not be the best choice. Think about how you write. You don't think one letter at a time and generate a probability distribution for what letter comes next. You think in complete words with concrete ideas of what you want to convey. This area of natural language processing still has a long ways to go.


{% comment %}
# ![Network diagram]({{ site.url }}/assets/network_diagram.jpg)
{% endcomment %}
