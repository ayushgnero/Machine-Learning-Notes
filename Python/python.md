# Unpacking a Sequence into Separate Variables
### Problem
You have an N-element tuple or sequence that you would like to unpack into a collectionof N variables.
### Solution
Any sequence (or iterable) can be unpacked into variables using a simple assignmentoperation. The only requirement is that the number of variables and structure matchthe sequence. For example:


```python
p = (4,5)
```


```python
x,y = p
```


```python
x
```




    4




```python
y
```




    5




```python
data = [ 'ACME', 50, 91.1, (2012, 12, 21) ]
```


```python
name, shares, price, date = data
```


```python
name
```




    'ACME'




```python
shares
```




    50




```python
price
```




    91.1




```python
data
```




    ['ACME', 50, 91.1, (2012, 12, 21)]




```python
name, shares, price, (year, mon, day) = data
```


```python
year
```




    2012




```python
mon
```




    12




```python
day
```




    21



### Discussion
Unpacking actually works with any object that happens to be iterable, not just tuples or lists. This includes strings, files, iterators, and generators. For example:


```python
s = 'hi'
```


```python
a,b = s
```


```python
a
```




    'h'




```python
b
```




    'i'



When unpacking, you may sometimes want to discard certain values. Python has nospecial syntax for this, but you can often just pick a throwaway variable name for it. For example:


```python
_,shares,price,_ = data
```


```python
_
```




    (2012, 12, 21)



However, make sure that the variable name you pick isn’t being used for something else already

# Unpacking Elements from Iterables of ArbitraryLength

### problem
You need to unpack N elements from an iterable, but the iterable may be longer than Nelements, causing a “too many values to unpack” exception.
### Solution
Python “star expressions” can be used to address this problem. For example, supposeyou run a course and decide at the end of the semester that you’re going to drop the firstand  last  homework  grades,  and  only  average  the  rest  of  them.  If  there  are  only  fourassignments, maybe you simply unpack all four, but what if there are 24? A star expres‐sion makes it easy


```python
def drop_first_last(grades):    
    first, *middle, last = grades
    return str(sum(middle)/len(middle))+str(middle)
```


```python
grades = [21,45,65,75,85,65,45,72]
drop_first_last(grades)
```




    '63.333333333333336[45, 65, 75, 85, 65, 45]'




```python

```
