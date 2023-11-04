In regression, our model takes the shape $t = f(x ; w)$. We have discussed (at some length now) how to select the best $w$ to optimise the model. But how do we pick $f$?


## Why We can't use Loss
You might say 'But we've already got a way of measuring how good our model is - why not just use loss?' Unfortunately, while loss helps us optimise and existing model, it doesn't help us compare between different functions $f$. 

To understand this, we need to understand what loss is in more detail. When we came across it earlier, it was introduced as 'a measure of how good the model is'. But really, it's a bit more precise and subtle than that; Loss measures how well the model fits the data we train it on. This makes it excellent for optimising the model to find the best fit. But it also means that it doesn't measure performance outside of this narrow definition. 

When we use a regression model in the real world, we usually want to use it for a particular task - for example, predicting a new value $t$ for some unseen $x$.


Loss $\mathcal{L}$ represents 

So far, we have discussed how to optimise a model - how to find the best $w$. But remeber, our model takes the shape $t = f(x | w)$. W