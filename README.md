[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-24ddc0f5d75046c5622901739e7c5dd533143b0c8e959d652212380cedb1ea36.svg)](https://classroom.github.com/a/IF3rQO50)
# Quicksort Pivots

in the lectures I only briefly mentioned strategies for determining a good pivot
for quicksort. The implementation on the slides simply picks the leftmost
element in the part of the array that we consider as a pivot. I also mentioned a
few other ways of picking a good pivot, e.g. randomly.

Median-of-three is also a good way of picking a pivot -- inspect the first,
middle, and last elements of the part of the array under consideration and
choose the median value. Using the probabilities for picking a pivot in a
particular part of the array (in the same way as we did on slide 34), argue
whether this method is more or less (or equally) likely to pick a good pivot
compared to simply choosing the first element. Assume that all permutations are
equally likely, i.e. the input array is ordered randomly.

Your answer must derive probabilities for choosing a good pivot and
quantitatively reason with them.

Add your answer to this markdown file. [This
page](https://docs.github.com/en/get-started/writing-on-github/working-with-advanced-formatting/writing-mathematical-expressions)
might help with the notation for mathematical expressions.

**MY ANSWER:**

When we consider the first, middle, and last elements of the subarray, and then pick the median value, we know for certain that there will be at least one element on either side of the median value picked.

Let's say our target is to pick a pivot that is greater than n/4 in the data set, and less than 3n/4 in the data set. If we were to randomly pick 1 element as out pivot, then the odds of it being in this target middle zone are 1/2. When we pick 3 elements, the odds of 1 of those elements being in the middle are 3 times as good. However, if both of the other elements selected are lower than the element in the target zone, then the median of the 3 elements may end up out of the target zone. And the same is true for the other way - if both of the other elements selected are higher than the element in the target zone, then the median of the 3 elements may end up out of the target zone as well.

The probability for all 3 elements to be within the same too-low zone is 1/4 * 1/4 * 1/4 = 1/64. This gives us a bad pivot.
The probability of all 3 being in the too-high zone is 1/64 as well. This gives us a bad pivot.
The probability of all 3 being in the good pivot zone is 1/2 * 1/2 * 1/2 = 1/8. This gives us a good pivot, and this probability is significantly greater than the 2 probabilities above.
The probability of all 3 elements being in the 3 different zones is 1/4 * 1/2 * 1/4 = 1/32. In these cases, we have a target in the too-low zone, the good-pivot zone, and the too-high zone. In this case, even if our too-low zone value is all the way to the left, and the good-pivot zone is all the way to the left in that zone, and the too-high zone is also all the way to the left in that zone, then our median value is still in the good pivot zone. So this gives us a good pivot.
The probability that 2 elements are in the good zone and 1 element is in a bad zone is 1/2 * 1/2 * 1/2 = 1/8. This should more often that not give us a good pivot.
The probability that 2 elements are in the same bad zone and 1 element is in the good zone is 1/4 * 1/4 * 1/2 = 1/32. This will more often than not give us a bad pivot, but the odds of this happening are not super high.
The probability that 2 elements are in the same bad zone and 1 element is in the other bad zone is 1/4 * 1/4 * 1/4 = 1/64. This should more often that not give us a good pivot.

Ultimately, the odds that we get a split that's 3-to-1 or better using this median-of-three pivot selection method are 11/16, or about 69%. This is certainly better than our 50% probability of picking a good pivot when just choosing the first element.

Obviously we also know that, for a sorted or reverse-sorted data set, we are guaranteed O(nlog(n)) time. And as I said earlier, we know for certain that there will be at least one element on either side of the median value picked.

For all these reasons, I would argue that the median of three method is more likely to pick a good pivot compared to simply choosing the first element.
