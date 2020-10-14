
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
Array is a data structure consisting of a collection of elements, each identified by an array index. An array is stored such that the position of each element can be computed from its index cell by mathematical formula.

## Properties of an Array
 - Can store data of specific data type
 - It has contiguous memory location
 - Every cell has a unique index
 - Index starts with 0
 - Size of array needs to be specified mandatorily and can't be modified
 
## Types of Array
 - One Dimensional
 - Multi-dimensional
	 - Two-dimensional
	 - Three-dimensional
	 - Four-dimensional
	 - ....
	 - n-dimensional
	 
## Common operation on an Array
 - Declaring, instantiating, initializing
 - Inserting a value
 - Traversing a given array
 - Accessing a given cell#
 - Searching a given value
 - Deleting a given value

### Declare, Instantiate, Initialize Array
Declare: int[] arr  				---------  O(1)  
Instantiate: arr = new int[5]        ---------  O(1)  
Initialize: arr[0] = 10; arr[1]=20; arr[2] = 30;     ---------  O(n)  
Declare, Instantiate, Initialize: int arr[] = new int[] {10, 20, 30};      ---------  Time complexity: O(1)	Space complexity: O(n)      

### Insertion

    insert(arr, valueToBeInserted, location)
    	if(arr[location] is occupied)
    		return error //location is already occupied
    	else
	    	arr[location] = valueToBeInserted\
	    	
Time complexity: O(1)      Space complexity: O(1)

### Traversal

    traverseArray(arr)
    	loop: i = 0 to arr.length
	    	print(arr[i]);
Time complexity: O(n)      Space complexity: O(1)

### Accessing a given cell#

    accessingCell(arr, cellNumber)
	    if(cellNumber > arr.size)
		    return exception	//Cell number cant' be bigger than array size
		else
			return arr[cellNumber]
			
Time complexity: O(1)		Space complexity: O(1)

### Searching a given value

    searchInAnArray(arr, valueToBeSearched)
	    loop: i = 0 to arr.length
		    if(arr[i] == valueToBeSearched)
			    return i
		return error	//value not found

Time complexity: O(n)		Space complexity: O(1)

### Deleting a given value

    deleteFromArray(arr, location)
	    if(arr[location] is occupied)
		    arr[location] = Integer.minValue
		else
			return error //location is already blank
Time complexity: O(1)		Space complexity: O(1)

### Create 2D Array
Declare: int[][] arr      --- O(1)
Instantiate: arr = new int[2][3]    --- O(1)  
Initialize: arr = arr[0][0] =  10, arr[0][1] =  20, arr[0][2] =  30, arr[1][0] =  40, arr[1][1] =  50, arr[1][2] =  60 --- O(mn)  
Declare, instantiate, initialize: int[][] arr = {{10, 20, 30}, {40, 50, 60}}   --- O(1)  

### Insertion in 2D array
insert(arr, valueToBeInserted, row, col)
    	if(arr[row][col] is occupied)
    		return error //location is already occupied
    	else
	    	arr[row][col] = valueToBeInserted
	    	
Time complexity: O(1)      Space complexity: O(1)

### Traversing a 2D array
    traverseArray(arr)
    	loop: i = 0 to rows
	    	look j = 0 to cols
		    	print(arr[i][j]);
		    	
Time complexity: O(mn)      Space complexity: O(1)

### Accessing a given cell# in 2D Array

    accessingCell(arr, row, col)
	    return arr[row][col]
			
Time complexity: O(1)		Space complexity: O(1)

### Searching a given value in 2D Array

    searchInAnArray(arr, valueToBeSearched)
	    loop: i = 0 to rows
		    loop: j = 0 to cols
			    if(arr[i][j] == valueToBeSearched)
				    print i, j
				    return;
		return error	//value not found

Time complexity: O(mn)		Space complexity: O(1)

### Deleting a given value in 2D Array

    deleteFromArray(arr, row, col)
	    if(arr[row][col] is occupied)
		    arr[row][col] = Integer.minValue
		else
			return error //location is already blank
			
Time complexity: O(1)		Space complexity: O(1)
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE2MjE3NTQ4NywzMjU3NDg3NTAsLTg3OD
gzMzIwLC00MzY4MjU3NTAsLTE3OTk4MjIwNDYsLTEwODE3MTUx
MjksLTU5NTkzMTQ3NywtMTAyNjUwMjYxOSwxNjA4NDEzMTA0LD
IwNzkzOTAwOSwxMDgwMTI1OCwtMTg1NzgwMDc2MSwyMDY4MDg1
MTAxLC0yNjA3OTExODMsLTcwMjA0MDM2NiwtMjA5NDc2NTA3MS
wxMzExOTM3NDE0LC03NTMwMzY2LC0xOTY3MTE3MzEwLC0xMjgy
NTAxNDU4XX0=
-->