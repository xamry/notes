
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



<!--stackedit_data:
eyJoaXN0b3J5IjpbMTUxOTgyNjYyNyw0Nzk1NTAyMjEsMTM2OT
k0MjY3NiwtMTg4NjkxMjM0NiwxNjI2NTg4MDcsLTExNjAyODgw
MDAsNzc1OTI3ODM2LC01NDU4NDMwNzIsLTE5OTcxMDE5NjcsLT
ExMDA4OTIwMTIsLTI0MTE5NDYzOV19
-->