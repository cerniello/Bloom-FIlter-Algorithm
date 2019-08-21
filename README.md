# Personalized Bloom FIlter Algorithm
Personalized version of the Bloom Filter Algorithm for duplicate detection of massive datasets of passwords.

![alt text](https://miro.medium.com/max/1838/1*HKQtaB1_m6Bt7xqTKr-HXg.png)

## Find the ***duplicates***!

Given [`passwords2.txt`](https://drive.google.com/open?id=1wTmOU-yqk4qdQYg42AquhzgpNGrRA96d), a 2GB file of alphanumeric passwords as input, each row corresponds to a string of 20 characters. The goal is to check whether there are some duplicate strings. Our definition of duplicate is that the two strings have the __same characters__, order is not important. Thus, "AABA" = "AAAB".

* We know In the file there are 10M duplicates, can we detect them?
* Does it happen that two strings with different characters are hashed to the same value? If yes, could you provide the number of *False Positive*?

____
## The Files

* **Final Notebook.ipynb**: The Jupyter notebook which contains the key steps of our work and where we explain each decision we have made and the usage of the algorithm. It shows our outcomes and our results with comments.

* **bloomfilter.py**: BloomFilter class which performs basic class methods (*check*, *add*, *get_size*, *get_hash_count*) used to set the filter.
____

## What is Bloom Filter?

A Bloom filter is a **space-efficient probabilistic** data structure that is used to test whether an element is a member of a set. For example, checking availability of username is set membership problem, where the set is the list of all registered username. The price we pay for efficiency is that it is probabilistic in nature that means, there might be some False Positive results. False positive means, it might tell that given username is already taken but actually it’s not.

### Interesting Properties of Bloom Filters

* Unlike a standard hash table, a Bloom filter of a fixed size can represent a set with an arbitrarily large number of elements.
* Adding an element never fails. However, the false positive rate increases steadily as elements are added until all bits in the filter are set to 1, at which point all queries yield a positive result.
* **Bloom filters never generate false negative** result, i.e., telling you that a username doesn’t exist when it actually exists.
* Deleting elements from filter is not possible because, if we delete a single element by clearing bits at indices generated by k hash functions, it might cause deletion of few other elements.

We can control the probability of getting a false positive by controlling the size of the Bloom filter. More space means fewer false positives. If we want decrease probability of false positive result, we have to use more number of hash functions and larger bit array. This would add latency in addition of item and checking membership.

### Probability of False positivity
Let **m** be the size of bit array, **k** be the number of hash functions and **n** be the number of expected elements to be inserted in the filter, then the probability of false positive **p** can be calculated as:

![alt text](https://www.geeksforgeeks.org/wp-content/ql-cache/quicklatex.com-78e77c34323cfb8afff2a80c0e91b26d_l3.svg)

### Size of Bit Array
 If expected number of elements **n** is known and desired false positive probability is **p** then the size of bit array **m** can be calculated as :

![alt text](https://www.geeksforgeeks.org/wp-content/ql-cache/quicklatex.com-8a21b35f5419f7968aafd408590b37bd_l3.svg)

### Optimum number of hash functions
The number of hash functions **k** must be a positive integer. If **m** is size of bit array and **n** is number of elements to be inserted, then **k** can be calculated as :

![alt text](https://www.geeksforgeeks.org/wp-content/ql-cache/quicklatex.com-88930c4f1e1c21cd0ce0569adbddde16_l3.svg)
