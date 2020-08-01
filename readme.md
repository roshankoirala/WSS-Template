# Introduction

The word cloud is a popular means of visualization of text data showing object sized according to there weights. However, if the text data is changing over time, for example the news paper article of each edition, then the position of the words in the word cloud can change drastically from time to time. This happens especially if the size of the words have changed over the time. See the picture below for an example.


Stable word position in the word cloud can help the viewer to keep track of the word and visually guide to see how it has changed over the time. Stabilizing the position of the words in word cloud for the dynamical data is a challenging issue. This project aims to solve this problem.

A general algorithm for static word cloud is to fill the space from larger to smaller size, starting from the center and spiraling outward until there is no more overlapping.

I tested the following modification to the algorithm to the dynamical system: The time is obviously discretized. For simplicity, we consider only two consecutive time frame and we want to minimize the displacement of the word between consecutive time lapse. In the long run the word can move, but the movement would look continuous making reading natural.

Here is the algorithm in plain English:

A. Take the initial word data (object and weights).

- Put the largest word at the center of the graph.
- Start with the next larger word from center to spiral outward until there is no overlap with previously placed word.
- Repeat for smaller words each time starting from the center.

B. Take the word data of next time step and take each word in size order

- If current word was present in the previous word cloud, start spiraling from its previous position until there is no overlap with already placed words. If it was not present start from the center of the graph.
- Take the next word, and repeat

C. Repeat at each time step on the new set of word data.

For the other approach to address the dynamical word cloud follow this link and the references therein.

# Generating the words

Rectangles of various sizes are used for the placeholder for the words in this project. We use labels on the rectangle to track them over the time. We define a container that gives a rectangle with specified label.


# Static word cloud



# Dynamic word cloud

## Current word in previous position

We start by calculating the starting position for the words in the current word data. In more general case it can be the average position of the center of the words in the previous word clouds. But here, I am working with two time steps. So, words are simply assigned at their previous centroid scaled by a factor which is the ratio of the total area occupied by the words in the previous word cloud to that of the present word cloud.

Here we define a function to assign each words in the new word list to to their previous position back in time. This function is limited to work with one static and next dynamic word cloud. But this handles the case of words appearing and disappearing from the previous word data.


## Off centered spirals

We define a function to calculate the spiral grid centered around the center of the word. The spirals are restricted so that it does not go beyond a projected area which is proportional to the sum of area of all the words in the word cloud. This partly helps to avoid from flying the word off from the center in the dynamical word cloud generation.

## Remove the overlap



## Dynamical word cloud generation
Finally, we find the non overlapped position for each word in the list and create a graphics out of it.




The positive points of this algorithm is that the biggest word will be placed first. So they relatively move lesser. But even for the smaller word they might find the smaller gap left by the bigger words so they also tend to move less.

# Future direction

- Detail tuning of the hyper-parameter for the better performance is to be done.

- It only consider evolution of the word cloud from previous static word cloud. The continuous evolution over the time is straight forward generalization.

- This algorithm might run into the problem of having words not packing compactly. A simple way to solve this problem is to finally pulling the words towards the center until it overlaps. Alternatively, this could be solved by assigning the weight such that the word will get penalized placing it away from the center of the graph. (not to confuse with the center of the spiral they are moving)

- Allowing vertical positioning of the word might help in the compactness. This can be achieved by rotating the word by 90 degree at each grid point before moving to the next grid point.

- Restricting the off centered spiral grid on the square gave more relative area for words to fit in. Restricting them in a circle of same relative area as the previous word cloud can improve the compactness of the word cloud.
