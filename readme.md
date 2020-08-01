detail is here: 

https://community.wolfram.com/groups/-/m/t/1729623

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

Please see the link below for the detail 

https://community.wolfram.com/groups/-/m/t/1729623

