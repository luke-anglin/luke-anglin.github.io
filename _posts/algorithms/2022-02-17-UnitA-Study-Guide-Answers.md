---
layout: post
title: Unit A Study Guide Answers
categories: algorithms
---

# Asymptotics

1. Give the three cases of the master theorem
   - **Case 1** - if $f(n) \in O(n^{\log _b a - \epsilon})$, then $f(n) \in \Theta(n^{\log _b a})$
   - **Case 2** - if $f(n) \in \Theta(n^{\log _b a})$, then $f(n) \in \Theta(n^{\log _b a} \log n)$
   - **Case 3** - if $f(n) \in \Omega(n^{\log _b a + \epsilon})$ **and** $af(n/b) \le cf(n)$, then $f(n) \in \Theta(f(n))$
2. Provide the limit cases for asymptotics
   - $[0, \infty)$ - $O$
   - $(0, \infty]$ - $\Omega$
   - $c$ - $\Theta$
   - $0$ - $o$
   - $\infty$ - $\omega$

# Sorting

1. Give the asymptotic runtime of **adjacent sorts**
   - $\Omega(n^2)$, because we can only fix one inversion at a time, $n(n-1)/2$ maximum inversions
2. List the five properties of sorting algorithms (not including **online**)
   - Runtime
   - Parallelizable
   - Stable
   - Adaptive
   - Inplace
   - Acronym - **Real puppies stay adolescents indefinitely**
3. Give the satisfied properties for the following sorting algos (if $n \log n$, say it satisfies runtime):
   - Merge sort - runtime, parallelizable, stable
   - Quicksort - runtime, parallelizable, (mostly) inplace
   - Bubble sort - inplace, stable
   - Insertion sort - stable, adaptive, inplace (also it is online)
   - Heap sort - runtime, in place
4. Explain in simple English the `Partition` algorithm that `Quicksort` uses
   1. If begin is less than end, increment begin pointer
   2. If begin is greater than end, swap the pointers, and decrement the end pointer
   3. If the pointers meet, you're done. That is your pivot to split the list on
5. When analyzing quicksort using median of medians, why can we add $S(0.7n)$ and $S(0.2n)$ in our analysis?
   - $f(n+m) \ge f(n) + f(m)$
6. What are the disadvantages of counting sort and radix sort, respectively (i.e. why not use these linear time sorts?)
   - Counting sort - too much memory
   - Radix sort - more memory, inflexible because of relying on digits
7. Explain how insertion sort, bubble sort, and heap sort function (just give the general algorithm)
   - Insertion sort - Insert element at the correct position in the sorted prefix.
   - Bubble sort - make $n$ passes through the list, swapping adjacent elements if out of order
   - Heap sort - Build heap, repeatedly extract min or max depending on if it is a max or min heap, build sorted list

## Lower bound proofs

1. Explain why `findMin` is $\Omega(n)$ with a lower bound proof (can be simple words for studying)
   - Best case scenario we have to do $n/2$ comparisons
2. Give the general idea of why comparison-based sorting algorithms are $\Omega(n \log n)$
   - Permutations at leaf nodes
   - Height $\log (n!)$ which is $\Theta (n \log n)$, and anything $\Theta$ is also $\Omega$