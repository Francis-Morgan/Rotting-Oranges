# Rotting-Oranges

Task: [Rotting Oranges](https://leetcode.com/problems/rotting-oranges/)
## About task

In a given grid, each cell can have one of three values:

1. the value 0 representing an empty cell;
2. the value 1 representing a fresh orange;
3. the value 2 representing a rotten orange.

Every minute, any fresh orange that is adjacent (4-directionally) to a rotten orange becomes rotten.

Return the minimum number of minutes that must elapse until no cell has a fresh orange.  If this is impossible, return -1 instead.

**example**

![](https://github.com/Francis-Morgan/Rotting-Oranges/blob/master/Rotten%20orange/example.png)

Input: [[2,1,1],[1,1,0],[0,1,1]]
Output: 4

## Solution idea

Firstly, we will create

We will create three sets. 

1 - fresh oranges.

2 - rotten orangesю

3 - a set that temporarily stores the coordinates of new rotten oranges and each iteration (minute) will change. 

New rotten oranges we place in 3 sets of sweat from the set of fresh oranges takes away a set of rotten oranges, and to the set of rotten oranges we add a set of already rotten. And it's gonna go on like this until there's no fresh oranges left.

##### How do you look for new rotten oranges?

Firstly, we find a cell with a value of 2, which is rotten orange.

We will need a list of tuples : [ (0,1), (0,-1), (1,0), (-1,0) ].
Thanks to this list, we'll check the neighboring cells.

If a fresh orange is found, it will be considered rotten.

Then we check the neighboring cells of already rotten orange and so on.

## Code explanation

First we'll know the dimensions of this matrix and create two sets.
```python
        rows, columns = len(grid), len(grid[0])
        fresh, rotten = set(),set()
```

##### If you wonder why we create sets instead of lists or dictionaries.

You can find an explanation for that at the end of this section.

Fill these sets with the values. We'll find fresh and rotten oranges. 
```python
        for r in range(rows):
            for c in range(columns):
                if grid[r][c] == 1:
                    fresh.add((r,c))
                if grid[r][c] == 2:
                    rotten.add((r,c))
```
Add tuples with orange coordinates.

Okay, now we have two sets.
Let's set up a minute counter.
```python 
minut = 0 
```

Now let's get to the main part of the program.

```python
while fresh:
            minut += 1
            new_rotten = set()
                
            for r,c in rotten:
                for nr, nc in [(0,1),(0,-1),(1,0),(-1,0)]:
                    if (r + nr, c + nc) in fresh:
                        new_rotten.add((r + nr, c + nc))
            if not new_rotten:
                return -1
            rotten = new_rotten
            fresh -= new_rotten
        return minut

```

Let's create a cycle that will work as long as a set of oranges isn't empty. And consider exiting the cycle if there are any fresh oranges left. Each iteration in this cycle equals 1 minute.

We'll create a set-buffer that will store new rotten oranges.

Now let's take apart these nested cycles:
```python
            for r,c in rotten:
                for nr, nc in [(0,1),(0,-1),(1,0),(-1,0)]:
                    if (r + nr, c + nc) in fresh:
                        new_rotten.add((r + nr, c + nc))
```

The external cycle takes the coordinates of a cell with a rotten orange. 

The internal loop takes the values from the list of tuples mentioned above.

Now let's check the condition:
```python
if (r + nr, c + nc) in fresh:
```

We add to the coordinates of the cell with rotten orange values from the motorcade. This helps us check the adjacent cells on axis 0 and axis 1.

**As example:**
The rotten orange is in a cell with coordinates (2,3).

Well, then, (2,3) + (0,1) = (2,4)

We have the coordinate of the adjacent cell on axis 0.

We'll do the same operation for the other cells.

If this cell is fresh orange, we add it to the **new_rotten** set. 

Next is the intended exit from the function.

If a set is empty and there is no fresh orange in the neighboring cells, we return -1.

Since we are no longer interested in the original rotten orange cells, we redefine this set.
```python
rotten = new_rotten
```
Let's find the difference in sets. 

**The difference between two sets is an operation that results in a set that includes all elements of the fresh set that are not included in the new_rotten set.**

These operations will continue until all fresh oranges are found.

#### About the sets

First, we use operations that characterize the features of sets. 

Second, Sets are faster than lists.
The sets are notable for the fact that the operation of checking "whether the object belongs to the set" is much faster than similar operations in other data structures.

## Input/Output

![](https://github.com/Francis-Morgan/Rotting-Oranges/blob/master/Rotten%20orange/input_output.PNG)

## Complexity

![](https://github.com/Francis-Morgan/Rotting-Oranges/blob/master/Rotten%20orange/Complexity.PNG)



