# Lecture 1: Algorithms and Computation

Goals:

1.  Solve computational problems
2.  Prove correctness
3.  Argue efficiency
4.  Communication of these ideas

## Problem

What is a computational problem? 
* inputs 
* outputs

## Algorithm

What is an algorithm? 
* A method for solving a problem. In other words it is a function that maps each input to a siongle output.

For birthday problem:
* maintain record 
* interview students in some order 
  * check if birthday is in record
  * if so return pair 
  * else add new student to record
* return no pair

## Correctness

How do we prove correctness?
* for small inputs, we can use case analysis
* for large inputs, algorithms must be *recursive* or loop in some way
* We must use *induction* 

*Example*: Proof of correctness of birthday problem

* Induct on k: the number of students in record
* *Inductive Hypothesis:* if first k students contain a matching pair, then the algorithm returns a match before interviewing the (k+1)st student.
* *Base Case:* k = 0, first k contains no match
* Assume IH is true for k=k' and consider k = k'+1
* if k' contains match &rarr; already returned by induction
* else if k'+1 contains match &rarr; algorithm checks all possibilities
