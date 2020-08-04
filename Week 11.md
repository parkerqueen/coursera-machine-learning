# Week 11

## Section 1
* A machine learning pipeline is a series of steps/stages, some of which employ machine learning, to solve a complex problem.
* For example a photo OCR pipeline may be: Text Detection $\to$ Character Segmentation $\to$ Character Classification $\to$ Spelling Check
* For text detection, we can train a classifier to detect if there is some text present in a $x\times y$ image patch. Then we can use the sliding window tecnique to carve out $x\times y$ windows from our image and feed it to our hypothesis. In the sliding window technique, a window of specified dimensions moves over the data (image) with a preset step size/stride. After doing this, we can build a similar image to the original one but with black pixels where there is no text and white pixels where there is text. We can then pass this image through an expansion operator (make black pixels white if in vicinity of white pixels). Lastly, we can use this image to draw boxes around the regions of text. (We can also use sliding windows of different dimensions and rescale each window to $x\times y$ before feeding it to the classifier.)
* We can use a similar 1D sliding window to detect character segmentation. Lastly, we can use another hypothesis for character recognition in each of the segments.

## Section 2
* There are three ways to obtain more data (likely to help if your algorithm has low bias)
  * Artificial Synthesis (including distortions to the available dataset)
  * Manual Labelling/Collection
  * Crowd Sourcing
* Pipelines are pretty pervasive and complex in machine learning systems. Ceiling analysis can be done to identify what part of the pipeline to dedicate more resources to. First off, we evaluate the overall performance of a pipeline. Then we start from the initial stage and replace it with a 100% accurate output it's supposed to produce and run this output through the rest of the pipeline. We measure the overall performance once again. The process continues and we move along the pipeline stages, replacing them with the 100% accurate output they're supposed to produce. In this way, we can measure the potential performance gains by improving the components of a pipeline.