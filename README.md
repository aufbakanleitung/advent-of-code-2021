![](input/advent%20of%20code.jpg)
# Advent of Code 2021: Python solutions
https://adventofcode.com/2021

## Lessons learned:
### Assignment 1 

Load the input file as integers on a single line using list comprehension
```python
scans = [int(line) for line in open('input/01_input.txt').read().splitlines()]
```

### Assignment 2 

Convert list of lists to correct filetypes using list comprehension
```python
moves = [[move[0], int(move[1])] for move in moves]
```

Initialize multiple variables with sequential equal signs 
```python
x = y = aim = 0
```

### Assignment 3 

Use the binary left shift `<<` to append a binary variable without type conversion 
```python
gamma = 0
for i in range(x):
    gamma <<= 1
```


### Assignment 4

Load first variable in one var and all subsequent variables in another with `*var`

```python
numbers, *boards = open('input/04_input.txt').read().split('\n\n')
```

Don't remove values from a list you're iterating over while iterating. This will cause the iterator to skip items. For a set it is even prohibited and will throw this error `RuntimeError: Set changed size during iteration`
```python
for board in boards:
    if check(board):
        boards.remove(board)  # This is bad
```

Instead, make a separate list/set/dict to store removed values and check for them in for-loop.
Also consider using an enumerator to store indexes instead of entire datasets for efficiency.
```python
done_boards = set()
for index, board in enumerate(boards):
    if index in done_boards:  continue
    if check(board):  done_boards.add(index)
```


### Assignment 5

Don't generate an empty (3x3) list of lists like below; the grid will contain 3 references to the same data item.
```python
grid = [[0] * 3] * 3

for line in grid:
    print(id(line))
# 4390269824
# 4390269824
# 4390269824
```
Instead create a new list every time and append it to the list of lists.

```python
grid2 = [[0] * 3 for _ in range(3)]
```

Split and cast values over multiple variables using `map()`
```python
x, y = map(int, var.split(','))
```

### Assignment 13
Print a list as a string so it looks more compact.
```python
for line in grid:
    print(''.join(line))
```

### Assignment 14
Directly load a split line as a dictionary with dict comprehension
```python
lines = {x.split()[0]:x.split()[1] for x in lines.splitlines()}
```

It is common to count occurrences of certain values with a dict, e.g.: `{'x': 2, 'y': 3}` 
Initialize a dict with the all the values set at 0 using `.fromkeys(x, 0)`, and get all the unique values with a `set()`
```python
pc = dict.fromkeys(set(lines), 0)
```

To time a function it is common to use a wrapper, which then uses a decorator. 
A decorator is a function that takes a function as an argument.
```python
def decorator(func): 
    def wrap(): 
        func() 
    return wrap 
function_used = decorator(function_used)
```
A wrapper is a notation to replace this line `function_used = decorator(function_used)` with a more convenient `@decorator`
```python
@timer
def run():
    for _ in range(10):
        sleep(.5)
run()
# Time required: 5034.56 ms
```