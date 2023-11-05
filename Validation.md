---
next: "[[Random Noise]]"
previous: "[[Vectorising Linear Regression]]"
---
In regression, our model takes the shape $t = f(x ; w)$. We have discussed (at some length now) how to select the best $w$ to optimise the model. But how do we pick $f$? We need a way to decide which functions produce the best models. Lets think about that.

## Loss - Why We can't use it
You might say 'We've already got a way of measuring how good our model is - why not just use loss?' Unfortunately, while loss helps us optimise parameters to a model ($w$), it doesn't help us compare between different functions $f$. 

To understand this, we need to understand what loss is in more detail. When we came across it earlier, it was introduced as 'a measure of how good the model is'. More precisely, loss measures how well the model fits the data we train it on. This makes it excellent for optimising the model to find the best fit, but it also means that it doesn't measure performance outside of this narrow definition. 

When we use a regression model in the real world, we usually want to use it for a particular task - for example, predicting a new value $t$ for some unseen $x$. We want our model to be **generalisable** - it should perform well on new data, not just the training set. 

Loss does not capture this nuance; a 'perfect fit' with a loss of zero (i.e. it passes through every data point exactly) is very likely a bad model for predicting unseen data. We say that the model is **overfitted** on the data. 


## Noise
Another important thing to remember is that our data is usually noisy - the measurements are not perfect. Noise in this case could refer to anything we don't include in the model - either because we can't or because we don't want to. We will formalise this idea a bit more later, but it means that even a 'true model' (i.e. one that describes a real relationship in the data) should have a non-zero loss when we test. More complex models can always decrease loss - but at some point, they are fitting the 'noise' in the data 


## Validation
The way we actually pick models is to test their predictive ability. To do this, we split up our data into a 'training set' and a 'validation set'. You train some models with the training set, and then check how well they can predict unseen values with the validation set. We can get a numerical measure of how well the model handles unseen data by computing the loss on the validation set - this is called the **validation loss**. This lets us measure not just how well the model fits the known data, but also how generalisable it is.

## Cross-validation
Choosing the validation data is important. In most cases, its OK to just randomly select a sample.

We can also perform cross-validation. In cross-validation, we split our input data into sections, and use each section as a validation set for the model. We then average the validation loss and pick the model with the minimum. Doing this with with $n$ sections is called $n$-fold cross-validation.

At the extreme, we could choose $n$ to be the same size as our input data set, treating each data-point as a validation set. This is called leave-one-out cross validation, and it gives us the strongest confidence in picking the correct model. However, note that the more validation sets we create, the more computationally expensive it becomes. Sometimes it's just not feasible. 