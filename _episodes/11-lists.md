---
title: "Sets"
teaching: 5
exercises: 5
questions:
- "What is a set, and how do I use it?"
objectives:
- "Explain how sets work."
- "Learn about set operations"
keypoints:
- "A set stores unsorted unique values."
- "The set list contains no values."
- "Sets may contain values of different types."
---
## A set keeps an unsorted unique collection of things.

* Different from lists
  * Lists have a defined order of elements, sets are unordered.
  * Lists can contain the same value multiple times, sets do not.
* Sets have a number of fast operations you can use to compare or combine them.
* Sets are great to keep track of things where order an count don't matter.
* If you put a value that is already in a set into that set again, the set will not change.

~~~
beatles = set(['John', 'Paul', 'George', 'Ringo'])
print('Beatles:', beatles)
print('length:', len(beatles))
beatles.add('Ringo')
print('Beatles:', beatles)
print('length:', len(beatles))

~~~
{: .python}
~~~
Beatles: {'John', 'Ringo', 'Paul', 'George'}
length: 4
Beatles: {'John', 'Ringo', 'Paul', 'George'}
length: 4
~~~
{: .output}

## Use `in` to check if something is in a set

Sets allow for efficient check of members.

~~~
print('Ringo is one of the Beatles:', 'Ringo' in beatles)
print('Keith is one of the Beatles:', 'Keith' in beatles)
~~~
{: .python}
~~~
Ringo is one of the Beatles: True
Keith is one of the Beatles: False
~~~
{: .output}

## You can add values to the set by using `add()`

~~~
beatles.add('Pete')
print('beatles is now:', beatles)
~~~
{: .python}
~~~
beatles is now: {'Pete', 'John', 'Ringo', 'Paul', 'George'}
~~~
{: .output}

## You can remove values from the set by using `remove()`

~~~
beatles.remove('Pete')
print('beatles is now:', beatles)
~~~
{: .python}
~~~
beatles is now: {'John', 'Ringo', 'Paul', 'George'}
~~~
{: .output}


## Multiple sets can be combined using `union()`

~~~
odd = set([1, 3, 5, 7, 9])
even = set([2, 4, 6, 8, 10])
all_numbers = odd.union(even)
print('Odd numbers:', odd)
print('Even numbers:', even)
print('All numbers:', all_numbers)
~~~
{: .python}
~~~
Odd numbers: {1, 3, 5, 9, 7}
Even numbers: {8, 2, 10, 4, 6}
All numbers: {1, 2, 3, 4, 5, 6, 7, 8, 9, 10}
~~~
{: .output}

> ## Sets are unordered
> As sets are unordered, the order of the elements can be different when you print this.
{: .callout}

## You can intersect two sets
This gives a new set containing only members existing in both sets

~~~
primes = set([2, 3, 5, 7])
odd_primes = primes.intersection(odd)
print('Primes that are also odd numbers:', odd_primes)
~~~
{: .python}
~~~
Primes that are also odd numbers: {3, 5, 7}
~~~
{:output}

## You can get the difference between to sets

This gives a new set containing all members of the first set not in the second set

~~~
even_non_primes = even.difference(primes)
print('Even numbers that are not prime numbers:', even_non_primes)
~~~
{: .python}
~~~
Even numbers that are not prime numbers: {8, 10, 4, 6}
~~~
{: .output}

## For `difference()`, the order matters

Using the same sets in a different order gives a different result.

~~~
uneven_primes = primes.difference(even)
print('Primes that are not even:', uneven_primes)
~~~
{: .python}
~~~
Primes that are not even: {3, 5, 7}
~~~
{: .output}

## Convert to a list and sort to get sorted output

~~~
sorted_primes = list(primes)
sorted_primes.sort()
print('Sorted primes:', sorted_primes)
~~~
{: .python}
~~~
Sorted primes: [2, 3, 5, 7]
~~~
{: .output}

> ## Initialising
>
> What does the following program print?
>
> ~~~
> letters = set('Hello world!')
> sorted_letters = list(letters)
> sorted_letters.sort()
> print('Letters in greeting:', sorted_letters)
> ~~~
> {: .python}
{: .challenge}

> ## Fill in the Blanks
>
> Fill in the blanks so that the program below produces the output shown.
>
> ~~~
> multiples_of_two = set([2, 4, 6, 8, 10])
> multiples_of_three = set([3, 6, 9])
> result1 = multiples_of_two._______(multiples_of_three)
> print('1', result1)
> result2 = multiples_of_____.______(multiples_of______)
> sorted_result2 = list(result2)
> sorted_result2.sort()
> print('2', sorted_result2)
> ~~~~
> {: .python}
>
> ~~~
> 1 {6}
> 2 [3, 9]
> ~~~
> {: .output}
{: .challenge}

