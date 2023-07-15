# Lecture 1: Algorithms and Computation

Goals:

1.  Solve computational problems
2.  Prove correctness
3.  Argue efficiency
4.  Communication of these ideas

## Problem

What is a computational problem?

- inputs
- outputs

## Algorithm

What is an algorithm?

- A method for solving a problem. In other words it is a function that maps each input to a siongle output.

For birthday problem:

- maintain record
- interview students in some order
  - check if birthday is in record
  - if so return pair
  - else add new student to record
- return no pair

## Correctness

How do we prove correctness?

- for small inputs, we can use case analysis
- for large inputs, algorithms must be **recursive** or loop in some way
- We must use **induction**

**Example**: Proof of correctness of birthday problem

- Induct on _k_: the number of students in record
- **Inductive Hypothesis:** if first _k_ students contain a matching pair, then the algorithm returns a match before interviewing the (_k_+1)st student.
- **Base Case:** _k_ = 0, first _k_ contains no match
- Assume IH is true for _k_=_k_' and consider _k_ = _k_'+1
- if _k_' contains match &rarr; already returned by induction
- else if _k_'+1 contains match &rarr; algorithm checks all possibilities

## Efficiency

What is efficiency?

- How long does it take to run?
- How long does it take to run in comparison to other algorithms?
- Dont measure time, instead count fundamental operations
- Expect performance to depend on the size of our input

- Asymptotic notation: ignore constant factors and lower order terms
  - Big O notation upper bound 
  - Omega notation lower bound
  - Theta notation upper and lower bound

|input  | constant  | logarithmic        | linear          | log-linear       | quadratic        | polynomial       | exponential      |
| ---   | --------- | ------------------ | --------------- | ---------------- | ---------------- | ---------------- | ---------------- |
| n     | Θ(1)      | Θ(log n)           | Θ(n)            | Θ(n log n)       | Θ(n^2)           | Θ(n^c)           | 2Θ(n^c)          |
| 1000  | 1         | ≈ 10               | 1000            | ≈ 10,000         | 1,000,000        | 1000^c           | ≈ 10^301         |
| Time  | 1 ns      | 10 ns              | 1 µs            | 10 µs            | 1 ms             | 10^(-9)c s       | 10^281 millenia  |

## Model of Computation

- Specification for what operations on the machine can be performed in O(1) time
- Model in this class is called the Word-RAM
- Machine word: block of w bits (w is word size of a w-bit Word-RAM)
- Memory: Addressable sequence of machine words
- Processor supports many constant time operations on a O(1) number of words (integers):
  - Integer arithmetic: (+, -, *, //, %)
  - Logical operators: (&&, ||, !, ==, <, >, <=, =>)
  - Bitwise arithmetic: (&, |, <<, >>, ...)
  - Given word a, can read word at address a, write word to address a
- Memory address must be able to access every place in memory
  - Requirement: w ≥ # bits to represent the largest memory address, i.e., log2 n
  - 32-bit words → max ∼ 4 GB memory, 64-bit words → max ∼ 16 exabytes of memory
- Python is a more complicated model of computation, implemented on a Word-RAM

## Data Structure

- A data structure is a way to store non-constant data that supports a set of operations
- A collection of operations is called an interface
  - Sequence: Extrinsic order to items (first, last, nth)
  - Set: Intrinsic order to items (queries based on item keys)
- Data structures may implement the same interface with different performance
- Example: Static Array - fixed width slots, fixed length, static sequence interface
  - `StaticArray(n)`: allocate static array of size n initialized to 0 in Θ(n) time
  - `StaticArray.get_at(i)`: return word stored at array index i in Θ(1) time
  - `StaticArray.set_at(i, x)`: write word x to array index i in Θ(1) time
- Stored word can hold the address of a larger object
- Like Python tuple plus `set_at(i, x)`, Python list is a dynamic array (see L02)

```python
def birthday_match(students):
    '''
    Find a pair of students with the same birthday
    Input: tuple of student (name, bday) tuples
    Output: tuple of student names or None
    '''
    n = len(students)  # O(1)
    record = StaticArray(n)  # O(n)
    for k in range(n):  # n
        (name1, bday1) = students[k]  # O(1)
        # Return pair if bday1 in record
        for i in range(k):  # k
            (name2, bday2) = record.get_at(i)  # O(1)
            if bday1 == bday2:  # O(1)
                return (name1, name2)  # O(1)
        record.set_at(k, (name1, bday1))  # O(1)
    return None  # O(1)
