---
title: "Basic Python"
teaching: 10
exercises: 2
---

[**Download Chapter notebook (ipynb)**](01-section1.ipynb)

:::::::::::::::::::::::::::::::::::::: questions 

- How are arrays useful in Python?
- Why do we need Numpy arrays?
- How can array data be iterated?

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: objectives

- Understanding arrays in Python
- Explaining the use of Numpy arrays
- Iterations on arrays
::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::: callout
## Note
Due to time restrictions, we will only cover the basic Python concepts required for the rest of this session. However, if you want to learn more about Python programming, please refer to the Software Carpentries full day course on [Programming in Python](https://swcarpentry.github.io/python-novice-gapminder/index.html).

::::::::::::::::::::

## Arrays

### List

We can use variables to store individual data in Python. However, in data science we often need to access multiple values to perform operations. In such cases, defining a variable for every single value becomes tedious. So instead, we can use arrays.

Arrays are variables that hold any number of values. Python provides 3 types of built-in arrays: ```list```, ```tuple```, and ```set```. There are a several shared features among all arrays in Python; however, each type of array enjoys its own range of unique features that each facilitate specific operations. 

```list``` is the most frequently used type of arrays in Python. The easiest way to explain how a ```list``` works is to think of it as a table that can have any number of rows. This is akin to a spreadsheet with one column.

Here is how to create a list using square brackets:




``` python
my_list = [1, 2, 3]
```

Type the name and execute a cell to see its content.


``` python
my_list
```

``` output
[1, 2, 3]
```

To access an item in a list, we use the name of the list, followed by square brackets. Inside the brackets we provide the index of the item requested. In Python, indices start from 0.



``` python
my_list[2]
```

``` output
3
```

The last item in an array is referred to with index `-1`


``` python
my_list[-1]
```

``` output
3
```

If the index refers to a non-existing item, an error will be "thrown" (in Python speak).


``` python
my_list[3]
```

``` output
IndexError: list index out of range
```

All items will be shown with the colon `:`

``` python
my_list[:]
```

``` output
[1, 2, 3]
```

Get segments of slices using index values to the left or right of the colon. Left is inclusive of, right excludes the item with the index specified. 



``` python
my_list[:2]
```

``` output
[1, 2]
```


``` python
my_list[1:]
```

``` output
[2, 3]
```
If you want to find index of a particular number: 


``` python
my_list.index(3)
```

``` output
2
```

You can obtain the number of items in a list using the function `len`

Arguments of functions are provided in round parentheses.


``` python
no_items = len(my_list)

no_items
```

``` output
3
```

:::::::::::::: callout
## Note

A `list` is a so-called mutable type of array. This means that it is possible to change a list's content. In contrast, if you create an array with round parentheses, it is immutable, and is referred to as a `tuple`. This cannot be changed in its current location in memory.
::::::::::::::

More items can also be added in a list using the `append` function.


``` python
my_list.append(4)

my_list
```

``` output
[1, 2, 3, 4]
```



``` python
my_list.append('Something')

my_list
```

``` output
[1, 2, 3, 4, 'Something']
```


``` python
my_list[-1]
```

``` output
'Something'
```

Similarly, items can also be deleted from a list using the `remove` function.


``` python
my_list.remove('Something')

my_list
```

``` output
[1, 2, 3, 4]
```

## Numpy Arrays

### Problems with Lists

Observe the results of executing the following code:


``` python
my_list = [1, 2, 3]

print(my_list)
```

``` output
[1, 2, 3]
```

``` python
print(my_list*2)
```

``` output
[1, 2, 3, 1, 2, 3]
```

One might expect each item in the list to be squared. Instead, the number of items is doubled.

Or: 


``` python
print(my_list)
```

``` output
[1, 2, 3]
```

``` python
print(my_list + 10)
```

``` output
TypeError: can only concatenate list (not "int") to list
```

Looking at this, it might be expected that 10 would be added to each item in the list. Instead, an error is thrown. This, and other features of `list` are not that intuitive.

In data science and machine learning, we therefore predominantly use `Numpy` arrays.

### Converting a List to a Numpy Array

First we import a function from the [Numpy library](https://numpy.org):


``` python
from numpy import array
```


``` python
my_np_array = array(my_list)

my_np_array
```

``` output
array([1, 2, 3])
```

This is more intuitive:


``` python
print(my_np_array)
```

``` output
[1 2 3]
```

``` python
print(my_np_array*2)
```

``` output
[2 4 6]
```

Similarly:


``` python
print(my_np_array)
```

``` output
[1 2 3]
```

``` python
print(my_np_array + 10)
```

``` output
[11 12 13]
```

In order to get the maximum and the index of the maximum in the array:


``` python
my_np_array.max()
```

``` output
np.int64(3)
```


``` python
my_np_array.argmax()
```

``` output
np.int64(2)
```

Indexing is with square brackets, as for `list` and `tuple`.

Click here to read more about `Numpy` arrays:

https://www.nature.com/articles/s41586-020-2649-2

## Iterations

### Iteration with a For Loop

Let us firstly create a `list` first and then iterate through it using a `for` loop.


``` python
my_list = [1, 22, 333, 4444, 55555]

my_list
```

``` output
[1, 22, 333, 4444, 55555]
```

Perform a set of operations on each item in the list. Display the item on your screen, using `print`.


``` python
for number in my_list:
    
    print(number)
```

``` output
1
22
333
4444
55555
```

To directly get the indices in a `for` Loop, use `enumerate`. This firstly provides the index, followed by the value of the item.


``` python
for index, item in enumerate(my_list):
    
    print('Index:', index, '    Item:', item)
```

``` output
Index: 0     Item: 1
Index: 1     Item: 22
Index: 2     Item: 333
Index: 3     Item: 4444
Index: 4     Item: 55555
```

If you want to print the positions of items in the list, remember to add `1` in the index and array start from index `0`.


``` python
for index, item in enumerate(my_list):
    
    print('Position:', index+1, '    Item:', item)
```

``` output
Position: 1     Item: 1
Position: 2     Item: 22
Position: 3     Item: 333
Position: 4     Item: 4444
Position: 5     Item: 55555
```


:::::::::::::::::::::::::::::::::::::keypoints 

- `list` is a mutable types of arrays.
- `NumPy` is a Python library optimised to deal for large, multi-dimensional arrays and matrices.
- Repetitive execution of the same block of code over and over is referred to as `iteration`.

::::::::::::::::::::::::::::::::::::::::::::::::
[r-markdown]: https://rmarkdown.rstudio.com/
