
# Introduction
Data Structure is a way to organize data in a way that enables it to be processed in efficient time.  
Algorithm is a set of rules to be followed to solve a problem.  

## Types of Data Structure 

### Primitive DS
 1. Integer
 2. Float
 3. Character
 4. Boolean
 5. ...and so on
 
### Non-primitive DS

#### Physical DS
 1. Array
 2. Linked List
 
#### Logical DS

(Logical DS are implemented using Physical DS)
 1. Stack
 2. Queue
 3. Tree
 4. Graph
 5. Hash
 6. ...and so on.
 
# Recursion

## Properties of Recursion
 1. Same operation is performed multiple times with different inputs
 2. In every step, we try to make the problem smaller
 3. We mandatorily need to have a base condition, which tells system when to stop recursion.

Example: Finding an element in a BST.

    search(root, valueToBeSearched)
    	if(root equals null)   //Base condition
    		return null
    	else if(root.value equals valueToBeSearched) //Base condition
    		return root
    	else if(root.value > valueToBeSearched) 
	    	//Same operation performed multiple times, making the problem smaller
    		search(root.left, valueToBeSearched)   
    	else if(root.value < valueToBeSearched)
	    	//Same operation performed multiple times, making the problem smaller
    		search(root.right, valueToBeSearched)     

## Why should we learn Resursion

 1. Makes code easy to write (compared to 'iterative' method) whenever a problem can be broken down into *similar* sub-problems.
 2. It is heavily used in data structures like Tree, Graph etc.
 3. Heavily used in techniques like Divide and conquer, Greedy, Dynamic Programming.
 
## Format of a Recursive Function
**Recursive Case:** Case where the function recur.  
**Base Case:** Case where the function does not recur.  

    SampleRecursion(parameter) {
	    if(base case is satisfied) {
		    return some base case value;
	    } else {
		    SampleRecursion(modified parameter);
	    }
    }
    
## Finding Factorial using Recursion

    Factorial(n)
	    if(n equals 0)
		    return 1
		else 
			return n * Factorial (n -1)

## Finding Fibonacci using Recursion
0, 1, 1, 2, 3, 5, 8, 13, 21.....

    fib(n)
	    if(n < 1)
		    return error message
		else if(n == 1 || n == 2)
				return n -1
		else
			reurn fib(n-1) + fib(n - 2)
				
## Recursion Vs Iteration
| Space Efficient                       | Recursion                  | Iteration |
|---------------------------------------|----------------------------|-----------|
| Space Efficient?                      | No (Due to stack)          | Yes       |
| Time Efficient?                       | No (Due to stack push/pop) | Yes       |
| Ease of code (to solve sub-problems)? | Yes                        | No        |

## When to use and avoid Recursion
### When to use

 - When we can easily break down a problem into sub-problems
 - When we're ok with extra overhead (time and space) that comes with it
 - When we need a quick working solution instead of efficient one
 
### When to avoid
If response to any of the above questions is NO

## Practical uses of Recursion 

 - Stack
 - Tree (Travesal, Insertion, Searching, Deletion)
 - Sorting (Quick sort, merge sort)
 - Divide and Conquer
 - Dynamic Programming
 - ...and so on.

# Algorithm Runtime Analysis
It is a study of a given algorithm's running time, by identifying its behavior as the input size for the algorithm increases. 
 
## Notations for Algorithm runtime analysis
### Omega (Ω) 
- Gives the tighter lower bound of a given algorithm 
- Helpful to determine the minimum resources required to be allocated
- Represents best case
### Big-o (O)
- Gives the tighter upper bound of a given algorithm
- Helpful to determine the maximum expected limit, e.g. car airbag system.
- Represents worst case
### Theta (θ)
- Decides whether upper and lower bound of a given algorithm are same or not
- Represents average case

## Examples of Algorithm runtime complexity

| Time complexity | Name               | Example                                       |
|-----------------|--------------------|-----------------------------------------------|
| O(1)            | Constant           | Adding an element at the front of Linked list |
| O(log n)        | Logarithmic        | Finding an element in a sorted array          |
| O(n)            | Linear             | Finding an element in an unsorted array       |
| O(n log n)      | Linear logarithmic | Merge sort                                    |
| O(n^2)          | Quadratic          | Shortest path between two nodes in a graph    |
| O(n^3)          | Cubic              | Matrix multiplication                         |
| O(2^n)          | Exponential        | Tower of Hanoi problem                        |

# Array

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTcwMjA0MDM2NiwtMjA5NDc2NTA3MSwxMz
ExOTM3NDE0LC03NTMwMzY2LC0xOTY3MTE3MzEwLC0xMjgyNTAx
NDU4LC03NjkzMjMzMjMsMTUxOTgyNjYyNyw0Nzk1NTAyMjEsMT
M2OTk0MjY3NiwtMTg4NjkxMjM0NiwxNjI2NTg4MDcsLTExNjAy
ODgwMDAsNzc1OTI3ODM2LC01NDU4NDMwNzIsLTE5OTcxMDE5Nj
csLTExMDA4OTIwMTIsLTI0MTE5NDYzOV19
-->