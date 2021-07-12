---
layout: post
title:  "HELLO WORLD!"
date:   2021-07-07 10:04:38 -0400
categories: general, NLP, BERT
---
FIRST POST so obviously must HELLO WORLD!

So what's the point of all of this. A bit of documenting my learnings (because if I don't write it down I'll forget it all). So what I typically do is explain everything as if I was trying to explain it to a child (with SOME technical vocabulary.) And I also like to break packages down to piece everything together. So yes, you will see me destroy beautifully constructed classes. It. Will. Be. Amazing.

The focus will be mostly on deep learning, particularly applications in NLP (though won't necessarily restrict myself to this, honestly it's whatever tickles my fancy, which sometimes includes RL and computer vision). And this is my first time using github pages, so this will be good learning experience overall **(see the following for a [markdown guide])**

**So the first couple posts I think will be related to NLP and specifically BERT.**

BERT I found was not very accessible. Unlike something like word2vec which was really easy to use, with BERT, since it's a pretrained model, there was a lot of playing with tensorflow, modelhub, etc. Huggingface has generally made it easier, but I'm also wondering if we can do anything without Huggingface... anyway...

## The basic problem with topic modeling...

Couple of problems I find when dealing with text data (nothing too complicated, let's be clear, no Q-A, etc.) But something as simple as classification. If we're to do it in a supervised way, requires a lot of labeled data, and your label set may not be static (e.g. if you're doing something like topic modeling, topics change overtime.) I haven't had much success with unsupervised approaches (LDA specifically - probably I need to tune more). But I found a really interesting approach called **[top2vec]** which was a really nice gateway into using BERT and using unsupervised approaches. Along with sentence embeddings.

Also, we can look at few shot learning, which again shows some potential (again, labeled data being expensive).

Some preamble:

## BERT
- really kickass embeddings
- generated on the fly (unlike word2vec, where you have a vector for each word), BERT has embeddings based on it's context (which is actually the entire document)
- hence computationally expensive
- does better than something like ELMo, which I believe is built using LSTMs **(fact check this :P)** with their associated problems
- BERT uses transformers, which are awesome **(how would I know? have I used them? no but that's what everyone claims so blah to you)**

## SBERT
- BERT is great but it's only **word** embeddings 
> ***do you still have embeddings for each word when BERT breaks all the words down into word pieces (to reduce the number of tokens)?***
- what can we do for sentences?
- so you can be conventional and go some kind of summary of the embeddings (e.g. average)
- note that BERT has a sentence seperator token (CLS and SEP), which *can* be used as a sentence embedding, but people claim that it's garbage
- what are other options? **[UNIVERSAL SENTENCE ENCODER]**
  - see the following which provides a good explanation of the construction: https://amitness.com/2020/06/universal-sentence-encoder/
  - basically there are two ways to encode the sentences, either using transformers or a deep averaging network
  - then the encodings are trained on several tasks (multi-task learning) to get the actual sentence embeddings, which include:
  1) modified skip-thought to predict previous and next sentence
  - three sentences are encoded and vectors are generated, use dot product to determine relevance **(fact check this)**
  2) conversational input-response prediction to predict the response
  - similarly as above, generate vectors and use dot product to determine relevance
  3) natural language inference - encode the premise and hypothesis and use a softmax to determine whether they are entailment, contradiction or neutral)
  > ***how to do multi-task learning?***

## PET (Pattern Extractive Training)



You’ll find this post in your `_posts` directory. Go ahead and edit it and re-build the site to see your changes. You can rebuild the site in many different ways, but the most common way is to run `jekyll serve`, which launches a web server and auto-regenerates your site when a file is updated.

Jekyll requires blog post files to be named according to the following format:

`YEAR-MONTH-DAY-title.MARKUP`

Where `YEAR` is a four-digit number, `MONTH` and `DAY` are both two-digit numbers, and `MARKUP` is the file extension representing the format used in the file. After that, include the necessary front matter. Take a look at the source for this post to get an idea about how it works.

Jekyll also offers powerful support for code snippets:

{% highlight ruby %}
def print_hi(name)
  puts "Hi, #{name}"
end
print_hi('Tom')
#=> prints 'Hi, Tom' to STDOUT.
{% endhighlight %}

Check out the [Jekyll docs][jekyll-docs] for more info on how to get the most out of Jekyll. File all bugs/feature requests at [Jekyll’s GitHub repo][jekyll-gh]. If you have questions, you can ask them on [Jekyll Talk][jekyll-talk].

[jekyll-docs]: https://jekyllrb.com/docs/home
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/

[markdown guide]: https://www.markdownguide.org/basic-syntax#headings
[top2vec]: https://github.com/ddangelov/Top2Vec
[UNIVERSAL SENTENCE ENCODER]: https://arxiv.org/pdf/1803.11175.pdf