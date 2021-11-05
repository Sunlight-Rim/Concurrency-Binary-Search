# Concurrency Binary Search Proof of Concept
Consider an threading usage example. \
Let's imagine that we searching for X in a certain range. Using binary search algorithm to find X we need to deal 5 comparison operations, for example. \
However, as you know, currently our computers and computing devices can perform data with the task parallelism, and we can use it to optimize binary search for X. \
The image below illustrates the idea behind this implementation, where the search is shown in the tree form on the top. Having only 4 threads we can divide our range with X into 4 parts and perform a comparison for all of them in one clock cycle — thereby "jumping over" several tree nodes (that is comparison operations). As soon as we know that X is contained in the range AB, which is 1/4 of the entire range, then we again divide AB into 4 parts and assign comparisons to all threads, and so on, until we find X. With this method, instead of 5 comparisons, we only make 2.

Also, with more knowledge about X, we can more optimize this algorithm using concurrency. In the described above method we made comparisons from top to bottom, "jumping over" the nodes of a tree to a level which the number of nodes is equal to the number of available threads. But these numbers may not necessarily be equal. With 4 threads we can divide the entire range into 8 parts, then perform all 8 comparisons in 2 clock cycles. This is a luck-oriented search method, which however becomes useful if, for example, we know that X likely to have roughly small values, although we do not want to exclude huge ones. On the image below we allocated 2 threads for searching X at the lowest level of the tree, among concrete values.

![Illustration](Illustration.jpg)
