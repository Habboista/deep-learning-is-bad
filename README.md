# Why I don't believe in deep learning

With deep learning I have a controversial relationship. Here I'll try to order my thoughts about why I don't like deep learning and
in general I don't believe in this approach. Also keep in mind that I _believe_ that deep learning is not the way, it is a conjecture of mine if you want and not a proved statement. I also use this as an excersice in writing github .md files.

## What is deep learning?

The deep learning approach can be summarized in the following procedure(for most tasks):

- identify a problem that can be formulated as an input-output problem(in particular: deep learning community loves ill-posed problems)
- datify the problem(i.e. represent in digital format inputs and outputs)
- make your inputs and outputs constrained to some spaces $X$ and $Y$
- identify a set of parametric functions $f_{\theta}: X \to Y$, $\theta \in \Theta$, as much differentiable in $\theta$ as you can
- define a procedure(called "training") for picking a function in this space(your deep learning model) that solves your datified problem. Usually this is done by defining a loss function and differentiating it in order to update your $\theta$ in a clever way
- test your model

## Do I trust deep learning models?

I don't! And that's the main reason for which I don't believe in deep learning.

Deep learning is based on the following idea:

> if my model performs well on **_some_** new data then I assume it performs well **_in general_**.

So we take some data never seen by the model called _test data_ and we _test_ the model. Depending on how well the model performs we say that the model _generalizes_.

> [!WARNING]
> In the deep learning field there is the bad habit of using _suggestive_ words such as "learning", "generalizes", "training" for expressing **technical** concepts. In my opinion this creates confusion and false expectations. _The model doesn't "generalize" from the data any more than we do by looking at a bunch of numbers_. If the model "looks" at a lot of cat images, it's not that it "learns" and "generalizes" to distinguish features like a cat nose, ear or something. It could be that there is some "learnt" numerical feature correlated in some way to be investigated with some high-level human-meaningful feature, but this has to be tested properly. Instead of saying that the model "learns" I'd say it **_approximates_** the desired mapping and instead of saying it "generalizes" I'd say nothing because I don't believe in model generalization.

This is exactly my point: why should the model perform well on new data? Making things more unlikely is the fact that the performance is usually measured with a different criterion from the loss. Criterions used for measuring performance on new data are called _metrics_.

There are techniques, called _regularization_, which aims to improve model generalization, but most of the times these are not problem(in a narrow sense) specific. Regularization techniques don't give a damn wether you're trying to classify cats and dogs or sharks and whales! So your knowledge about these specific problems is usually not passed to the models! Usually knowledge is embedded in more subtle ways, like in the loss function or some data-preprocessing, etc... It is something, but still it is not enough specific for justifying generalization capabilities on each task, why should resnet50 better learns cat features if I use state-of-the-art regularization techniques? In addition to this, usually the test set is fixed, so basically researchers compete to find the model that generalizes better to **_that_** test data, what happens with the model in the wild?

### Psychology plays a role

Now... deep learning is highly experimental, this implies we don't care much about theory as long as results are achieved and results **are** achieved usually. Fair enough. But from my perspective what deep learning does is just taking big models, big data and big graphic cards and run experiments. The bigger everything the higher the probability of success(actually big things are not not that easy to manage - _that's what she said_ - and a lot of engineering efforts have been made over time to deal with it). What's wrong with this? Nothing, I just don't trust these models! The scale of models, of datasets and of computational power is just too much for the human mind and this is why we are all amazed by the results of this field![^1]
Irrationaly I am amazed like everyone else but rationally I don't trust deep learning models.

[^1]: It would be interesting to dig into this topic with some psychologist and check wether there's some truth in this.

### The curse of deep learning

The curse of dimensionality is the burden of all sciences that work with data! Deep learning particularly suffers this curse since it works with highly dimensional data.
The way I personally rephrase this principle is the following:

> The higher the dimensionality of your data, the less it makes sense to form an intuition of the problem and the more computational infeasible are precise methods.

> [!NOTE]
> Basically every statistical learning and deep learning method loses interpretability/explainability when applied to high dimensional data, that's why the majority of them result in _black boxes_ algorithms.

For me **a posteriori explanations of what models do don't make sense**. I reject the concept of ~~explainability~~ and the research on it. Interpretability instead is what I am interested into: the model has to be designed so that a priori it works in a transparent way! I'd say that interpretability is connected to generalization capabilities of models, in the sense that if it is clear how an algorithm makes its prediction then it is probable that knowledge about the problem is explicitly embedded into the algorithm(it is transparent by virtue of this shared human knowledge into it) and hence the model is facilitated in learning relevant patterns that goes beyond training data. Though developing useful interpretable models for dealing with complex problems is easier said than done, in fact the main and only interpretable model examples that I can think of are linear regression & co...

## BUILDING FROM BELOW

Classical algorithms were built from below, meaning that methods were developed for dealing with some problem in some specific setting(e.g. an algorithm for change detection with rain at night), these were put together and a functioning algorithm was written and calibrated so that it would function under pre-determined conditions(This is often done in industry, where environmental conditions can be controlled). So the algorithm is built **_from below_**, by considering more and more environmental conditions, fine-calibrating the machinery with experiments, etc... sometime statistical learning is used, but with low-dimensional data so that the resulting algorithm is reliable from a statistical point of view.
Building from below your algorithm assure it interpretability, reliability under desired conditions and generalization capabilities in the determined environment. For instance a canny edge detector will work very good with pretty every image consisting of a uniform monochromatic background an only one object in the foreground.

## BUILDING FROM ABOVE

Deep learning instead **_builds from above_** in a certain sense: it defines a parametric mapping(the model) which basically has a defined behaviour everywhere in the space of inputs, it just needs to be trained so that we adjust that to our needs. I say that it is built from above for two reasons:

- As opposed to classical algorithms which are explicitly built from below
- Because if I try to fit a model on a single point I usually will end up defining the model behaviour on a vast area to which the point belongs to(take as an example decision boundaries drawing in which the regions are way bigger than the single points)
  Anyway, this are just definitions. The problem of this approach is that in high dimensional spaces usually point clouds are low dimensional, so that basically curse of dimensionality applies even more since the possible patterns of low dimensional data in high dimensional spaces explodes combinatorially(think about configuration of planes in 3-dimensional spaces and configurations of points in those same spaces). Also I believe that constraining data to be high dimensional(for instance an image classifier that does not accept images with lower resolution than a certain threshold) implies that data is not properly represented. Images are rectangular usually, but the interesting segments of images are of disparate shapes! But we constrain the model to process only rectangular objects(big windows containing objects of interest, yet a from above approach).

I call it a day.
I'll update this whenever my thoughts mature or I see errors.
