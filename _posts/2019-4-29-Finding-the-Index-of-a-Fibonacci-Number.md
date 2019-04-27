---
layout: post
title: Finding the Index of a Fibonacci Number
tags: python
---

Leonardo Fibonacci was an Italian mathematician born in the XII century, whose main heritage was introducing the Hindu-Arabic numeral system — the decimal system — in the western world, and also for creating the famous Fibonacci numbers [[1]](https://en.wikipedia.org/wiki/Fibonacci).

The Fibonacci numbers form a sequence that follows a remarkable pattern: as the number of the sequence increase, the ratio between two consecutive numbers gets closer to the golden ratio [[2]](https://en.wikipedia.org/wiki/Golden_ratio). This golden ratio can be observed in natural phenomena, like plants, insects' shells, galaxies, and so on.

<img src="https://blog.shawacademy.com/wp-content/uploads/2015/09/Golden-Ratio-Photography-1000x605.jpg" alt="Sunflower showing the golden ratio" width="300" height="300">


The Fibonacci sequence, $F$, can be described as follows:
<img src="https://latex.codecogs.com/svg.latex?F(0)=0" title="F(0)=0" />
<br>
<img src="https://latex.codecogs.com/svg.latex?F(1)=1" title="F(1)=1" />
<br>
$$
F(n) = F(n-1) + F(n-2); n≥2,
$$

where <img src="https://latex.codecogs.com/svg.latex?n" title="n" /> corresponds to the $n^{th}$ term of the sequence.

In this Snippet, we will show two practical ways to create a Fibonacci sequence. Then, we will do something even more interesting: we will create a function that, when provided a number, will tell if the number is a Fibonacci number or not, and if not, will tell between which indices of the sequence the number is located at.

## Creating a Fibonacci Sequence

### Method A — the longer way

For this method, we will grab the definition shown above and we will create a function that, first, creates the exception cases for when $n = 0$ and $n = 1$, and second, creates the sequence for when $n≥2$.

<script src="https://gist.github.com/rmoralesdelgado/082bf88a70f7b9e462f44522935cd5c1.js"></script>
<script src="https://gist.github.com/rmoralesdelgado/ee4153fcf6ed99e7db1715313020b7b8.js"></script>

Once the function has been defined, we will test it for a special condition, e.g. $F(1)$, and also for $n=10$, such that all the sequence up to the Fibonacci number at index 10 will be shown.


```python
fib_seq_A(1)
```




    [0, 1]




```python
fib_seq_A(10)
```




    [0, 1, 1, 2, 3, 5, 8, 13, 21, 34, 55]



### Method B — a shorter way

There are multiple ways to define functions that generate a Fibonacci sequence. Below, we present a shorter one — it will produce exactly the same output as the one above, but in less lines of code. One thing to note, is that this function 


```python
def fib_seq_B(n):
    
    # Creating an assertion to guarantee that n will be int:
    assert ((isinstance(n, int)) & (n >= 0)), '"n" must be int and positive.'
    
    # Assigning the first two elements of the sequence to a and b, respectively:
    a, b = 0, 1
    
    # Creating an empty list to append the new values to:
    final_seq = []
    
    # For-looping from index 0 to n+1 (last-inclusive):
    for i in range(n + 1):
        if i < 2:
            final_seq.append(i) # Taking advantage of i=0 and i=1 for n<2
            pass
        else:
            a, b = b, a + b
            final_seq.append(b)
            pass
        pass
    
    return final_seq
```

Once the function has been defined, we will test it for a special condition, e.g. $F(1)$, and also for $n=10$, such that all the sequence up to the Fibonacci number at index 10 will be shown.


```python
fib_seq_B(2)
```




    [0, 1, 1]




```python
fib_seq_B(10)
```




    [0, 1, 1, 2, 3, 5, 8, 13, 21, 34, 55]



## Finding the Index of a Fibonacci Number

Once the functions to create a Fibonacci sequence have been defined, our next step is to define a function that, when a passed in a positive integer (allegedly a Fibonacci number), returns its index in the sequence. Note that $F(1)=F(2)=1$. For this reason, we will make this function work for inputs greater than $1$ — that is, $F(n)>1$.


```python
def fib_index_getter(number):
    
    assert isinstance(number, int), 'The input must be an int.'
    assert (number > 1), 'The input must be greater than 1.'
    
    # Creating a variable to hold the last-calculated Fibonacci number, starting at 1:
    fib_number = 1
    
    # Creating a variable to set the starting index (i.e. F(2)):
    fib_index = 2
    
    # While-looping until the last-calculated Fibonacci number is ≥ than the input:
    while fib_number < number:
        fib_index += 1 # Increasing the index by 1
        fib_number = fib_seq_A(fib_index)[-1] # Grabbing the last number, using function fib_seq_A
    
    # Output condition: if input is not a Fib number, indicate between which indices is located
    # and return the upper-limit index:
    if fib_number > number:
        print('The number provided is not a Fibonacci one. It is between indices {} and {}.'.format(fib_index - 1, 
                                                                                                   fib_index))
        return fib_index
    
    # Output condition: if input is a Fib number, indicate its index and return it:
    elif fib_number == number:
        print('The Fibonacci number provided is in position {} of the sequence.'.format(fib_index))
        return fib_index
```

Now, we will first test the new function for an actual Fibonacci number, 21.


```python
b = fib_index_getter(21)
```

    The Fibonacci number provided is in position 8 of the sequence.



```python
b
```




    8




```python
fib_seq_A(b)
```




    [0, 1, 1, 2, 3, 5, 8, 13, 21]



As seen above, the function indicated that the input is a Fibonacci number and also retrieved its index correctly, which we verified by calling `fib_seq_A` with the returned index. Now, we will test the function with a non-Fibonacci number, let's say 20.


```python
b = fib_index_getter(20)
```

    The number provided is not a Fibonacci one. It is between indices 7 and 8.


**End.**

---

<script src="https://gist.github.com/rmoralesdelgado/cec9fbe2e1955829ab6714cd5a2fc594.js"></script>
