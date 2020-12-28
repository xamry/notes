
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

Linear DS: Array, LinkedList, Stack, Queue  
Non-linear DS: Tree, Graph  
 
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

## When to use/ avoid Array
### When to use

 - When there is need to store multiple, similar type of data.
 - When random access is regular affair. (O(1) time operation)
 
### When to avoid
 - Data to be stored are non-homogeneous
 - Number of data to be stored is not known in advance

## Practical uses of Array

 - Dynamic Programming
 - Hashtable

# Linked List
A linked list is a linear data structure where each element is a separate object. Each element (node) comprises of two items - the data and the reference to next node. The most powerful feature of a linked list is that it is of variable size.

## Linked List Vs Array

 - Each node is a separate object
 - Variable size
 - Not random access like Array

## Components of a Linked List

 1. Node - Contains data and reference to next node
 2. Head - Reference to first node in the list
 3. Tail - Reference to last node in the list (Make insertion faster in O(1) time)

## Types of Linked List

### Single Linked List
Most basic for of Linked List which gives the flexibility to add/ remove nodes at runtime.

### Circular single linked list
When we want to loop through the list indefinitely until the list exists.
Example: Multiplayer board game, if we're tracking player's turn in linked list.

### Double linked list
When we want to move in both directions depending on requirement.
Example: Music player that has next and previous buttons.

### Circular double linked list
When we want to loop through the list indefinitely until the list exists. We also want to move forward and backward.
Example: 'Alt+TAB' button in Windows.

## Operations on Single Linked List (SLL)
### Creation of SLL

    createSingleLinkedList(nodeValue)
	    create a head, tail pointer and initialize with NULL
	    create a blank node
	    node.value = nodeValue
	    node.next = NULL
	    head = node
	    tail = node
Time complexity: O(1)		Space complexity: O(1)

### Insertion in SLL
There can be 3 cases:

Insertion at start of LL
Insertion at end of LL
Insertion at a specified location in LL   

    insertInLinkedList(head, nodeValue, location)
            Create a blank node
            node.value = nodeValue
            if(! existsLinkedLIst(head))
                return error //Linked list doesn't exist
        	else if(localtion equals 0)	//Insert at first position
        		node.next = head
        		head = node
        	else if(location equals last)	//Insert at last position
        		node.next = NULL
        		tail.next = node
        		tail = node
        	else	//Insert at specified location
        		loop : tmpNode = 0 to location -1	//loop till we reach specified node   O(n, rest all lines are O(1)
        		node.next = tmpNode.next
        		tmpNode.next = node
        					 
Time complexity: O(n)		Space complexity: O(1)

### Traversal of SLL

    traverseLinkedList(head):
    	if(head == NULL) 	//Empty linked list
    		then return;	
    	else
    		loop: head to tail
    			print currentNode.value
Time complexity: O(n)		Space complexity: O(1)

### Search node in SLL

    searchNode(head, valueToFind)
	    loop: tmpNode = head to tail
		    if(tmpNode.value == valueToFind)
			    print tmpNoe.value //value is found
			    return
		return node value not found
Time complexity: O(n)		Space complexity: O(1)

### Delete node from SLL
There can be 3 cases:  

Deletion first of LL (Two cases: 1. When node to be deleted is the only one present, 2. There are others)    
Deletion last node of LL (Two cases: 1. When node to be deleted is the only one present, 2. There are others)   
Deletion at a specified location in LL  

    deleteNode(head, location)
        if(doesNotExistLL(head))
	        return error //Linked list doesnot exist
	    else if(location == 0) //we want to delete first node
		    head = head.next
		    if this was the only element in LL, then set tail  NULL
		else if(locaton >=last)	//we want to delete last node (any value greater than last being considered as last for convenience, we could throw error as well)
			if(current node is the only node in list)
				head = tail = NULL
				return
			toop till second last node (tmpNode)
			tail = tmpNode; tmpNode.next = NULL
		else	//Any other internal node
			loop: tmpNode = head to location -1
			tmpNode.next = tmpNode.next.next;
Time complexity: O(n)		Space complexity: O(1)

### Delete entire SLL

    deleteLinkedList(head, tail)
	    head= NULL
	    tail  = NULL
Time complexity: O(1)		Space complexity: O(1)	    

## Operations on Circular Single Linked List (CSLL)
### Creation of CSLL

    createCircularSingleLinkedList(nodeValue)
	    create a head, tail pointer and initialize with NULL
	    create a blank node
	    node.value = nodeValue
	    **node.next = node**
	    head = node
	    tail = node
Time complexity: O(1)		Space complexity: O(1)

### Insertion in CSLL
There can be 3 cases:  

Insertion at start of CSLL  
Insertion at end of CSLL  
Insertion at a specified location in CSLL   (Algo exactly similar to SLL)

    insertInCircularSingleLinkedList(head, nodeValue, location)
            Create a blank node
            node.value = nodeValue
            if(! existsLinkedLIst(head))
                return error //Linked list doesn't exist
        	else if(localtion equals 0)	//Insert at first position
        		node.next = head
        		head = node
        		**tail.next = head**
        	else if(location equals last)	//Insert at last position
        		**node.next = head**
        		tail.next = node
        		tail = node
        	else	//Insert at specified location
        		loop : tmpNode = 0 to location -1	//loop till we reach specified node   O(n, rest all lines are O(1)
        		node.next = tmpNode.next
        		tmpNode.next = node
        					 
Time complexity: O(n)		Space complexity: O(1)

### Traversal of CSLL
Similar to SLL  
    traverseSingleLinkedList(head):
    	if(head == NULL) 	//Empty linked list
    		then return;	
    	else
    		loop: head to tail
    			print currentNode.value
Time complexity: O(n)		Space complexity: O(1)

### Search node in CSLL
Similar to SLL  
    searchNode(head, valueToFind)
	    loop: tmpNode = head to tail
		    if(tmpNode.value == valueToFind)
			    print tmpNode.value //value is found
			    return
		return node value not found
Time complexity: O(n)		Space complexity: O(1)

### Delete node from CSLL
There can be 3 cases:  

Deletion first node of LL (Two cases: 1. When node to be deleted is the only one present, 2. There are others)    
Deletion last node of LL (Two cases: 1. When node to be deleted is the only one present, 2. There are others)   
Deletion at a specified location in LL  

    deleteNodeFromCSLL(head, location)
        if(doesNotExistLL(head))
	        return error //Linked list doesnot exist
	    else if(location == 0) //we want to delete first node
		    head = head.next
		    **tail.next = head**
		    **if this was the only element in LL, then update head=tail=node.next=NULL**
		else if(locaton >=last)	//we want to delete last node (any value greater than last being considered as last for convenience, we could throw error as well)
			if(current node is the only node in list)
				**head = tail = node.next = NULL**
				return
			toop till second last node (tmpNode)
			tail = tmpNode; 
			**tmpNode.next = head**
		else	//Any other internal node
			loop: tmpNode = head to location -1
			tmpNode.next = tmpNode.next.next;
Time complexity: O(n)		Space complexity: O(1)

### Delete entire CSLL
In addition to what we did in case of SLL, we also have to delete the circular link in order for GC to reclaim the memory correctly.
    deleteCircularSingleLinkedList(head, tail)
	    head= NULL
	    ** tail.next = NULL**
	    tail  = NULL
Time complexity: O(1)		Space complexity: O(1)	    

## Operations on Double Linked List (DLL)
### Creation of DLL

    createDoubleLinkedList(nodeValue)
	    Create a blank node
	    node.value = nodeValue
	    head = node
	    tail = node
	    node.next = node.previous = NULL	

Time complexity: O(1)		Space complexity: O(1)	  

### Insertion in DLL
There can be 3 cases:

Insertion at start of LL
Insertion at end of LL
Insertion at a specified location in LL   

    insertInDoubleLinkedList(head, nodeValue, location)
            Create a blank node
            node.value = nodeValue
            if(! existsLinkedList(head))
                return error //Linked list doesn't exist
        	else if(localtion equals 0)	//Insert at first position
        		node.next = head
        		**node.prev = NULL**
        		**head.prev = node**
        		head = node
        	else if(location equals last)	//Insert at last position
        		node.next = NULL
        		**node.prev = tail**
        		tail.next = node
        		tail = node
        	else	//Insert at specified location
        		loop : tmpNode = 0 to location -1	//loop till we reach specified node   O(n, rest all lines are O(1)
        		node.next = tmpNode.next
        		**node.prev = tmpNode**
        		tmpNode.next = node
        		**node.next.prev = node**
        					 
Time complexity: O(n)		Space complexity: O(1)

### Traversal of DLL
Similar to Single LL
    traverseDoubleLinkedList(head):
    	if(head == NULL) 	//Empty linked list
    		then return;	
    	else
    		loop: head to tail
    			print currentNode.value
Time complexity: O(n)		Space complexity: O(1)

### Reverse Traversal of DLL
    ReverseTraverseDoubltmpNode.next = node
        					 
Time complexity: O(n)		Space complexity: O(1)

### Traversal of SLL

    traverseLinkedList(head):
    	if(head == NULL) 	//Empty linked list
    		then return;	
    	else
    		**loop: tail to head**
    			print currentNode.value
    			
Time complexity: O(n)		Space complexity: O(1)

### Search node in DLL

    searchNode(head, valueToFind)
	    loop: tmpNode = head to tail
		    if(tmpNode.value == valueToFind)
			    print tmpNoe.value //value is found
			    return
		return node value not found
Time complexity: O(n)		Space complexity: O(1)

### Delete node from DLL
There can be 3 cases:  

Deletion first of LL (Two cases: 1. When node to be deleted is the only one present, 2. There are others)    
Deletion last node of LL (Two cases: 1. When node to be deleted is the only one present, 2. There are others)   
Deletion at a specified location in LL  

    deleteNode(head, location)
        if(doesNotExistLL(head))
	        return error //Linked list doesnot exist
	    else if(location == 0) //we want to delete first node
		    if this was the only element in LL, then set head = tail = NULL; return;
		    head = head.next; 
		    **head.prev = NULL**
		    		    
		else if(locaton >=last)	//we want to delete last node (any value greater than last being considered as last for convenience, we could throw error as well)
			if(current node is the only node in list)
				head = tail = NULL
				return
			//No looping required for DLL
			**tail = tail.prev; tail.next = NULL**
		else	//Any other internal node
			loop: tmpNode = head to location -1
			tmpNode.next = tmpNode.next.next;
			**tmpNode.next.prev = tmpNode**
			
Time complexity: O(n)		Space complexity: O(1)

### Delete entire DLL
Due to cyclic dependencies between adjoining nodes, just setting head and tail to null won't free up the node's memory. We have to traverese all the nodes and delete previous references.

    deleteLinkedList(head, tail)
	    loop (tmp: head to tail)
		    tmp.pre = NULL
	    head = tail  = NULL
	    
Time complexity: O(n)		Space complexity: O(1)	    

## Operations on Circular Double Linked List (CDLL)
### Creation of CDLL
In CDLL, the last node points to first node, and first node points to last node.

    createCircularDoubleLinkedList(nodeValue)
	    Create a blank node
	    node.value = nodeValue
	    head = node
	    tail = node
	    **node.next = node.previous = node**	

Time complexity: O(1)		Space complexity: O(1)	  

### Insertion in CDLL
There can be 3 cases:

Insertion at start of LL
Insertion at end of LL
Insertion at a specified location in LL   

    insertInCircularDoubleLinkedList(head, nodeValue, location)
            Create a blank node
            node.value = nodeValue
            if(! existsLinkedList(head))
                return error //Linked list doesn't exist
        	else if(localtion equals 0)	//Insert at first position
        		node.next = head
        		**node.prev = tail**
        		**head.prev = node**
        		head = node
        		**tail.next = node***
        	else if(location equals last)	//Insert at last position
        		**node.next = head**
	        	node.prev = tail
        		**head.prev = node**        		
        		tail.next = node
        		tail = node
        	else	//Insert at specified location
        		loop : tmpNode = 0 to location -1	//loop till we reach specified node   O(n, rest all lines are O(1)
        		node.next = tmpNode.next
        		node.prev = tmpNode
        		tmpNode.next = node
        		node.next.prev = node
        					 
Time complexity: O(n)		Space complexity: O(1)

### Traversal of CDLL
Similar to Single/ Double LL

    traverseDoubleLinkedList(head):
    	if(head == NULL) 	//Empty linked list
    		then return;	
    	else
    		loop: head to tail
    			print currentNode.value
    			
Time complexity: O(n)		Space complexity: O(1)

### Reverse Traversal of CDLL
    ReverseTraverseDoubleLinkedList(head):
    	if(head == NULL) 	//Empty linked list
    		then return;	
    	else
    		**loop: tail to head**
    			print currentNode.value
    			
Time complexity: O(n)		Space complexity: O(1)

### Search node in CDLL
Similar to DLL

    searchNode(head, valueToFind)
	    loop: tmpNode = head to tail
		    if(tmpNode.value == valueToFind)
			    print tmpNode.value //value is found
			    return
		return node value not found
Time complexity: O(n)		Space complexity: O(1)

### Delete node from CDLL
There can be 3 cases:  

Deletion first of LL (Two cases: 1. When node to be deleted is the only one present, 2. There are others)    
Deletion last node of LL (Two cases: 1. When node to be deleted is the only one present, 2. There are others)   
Deletion at a specified location in LL  

    deleteNode(head, location)
        if(doesNotExistLL(head))
	        return error //Linked list doesnot exist
	    else if(location == 0) //we want to delete first node
		    if this was the only element in LL, then set head.next = head.prev = head = tail = NULL; return;	//Corner case: Necessary to remove the self loop in order for it to become eligible for garbage collection
		    head = head.next		    
		    **head.prev = tail**
		    **tail.next = head**
		    		    
		else if(locaton >=last)	//we want to delete last node (any value greater than last being considered as last for convenience, we could throw error as well)
			if(current node is the only node in list)
				head = tail = NULL
				return
			//No looping required for DLLtoop till second last node (tmpNode)
			**tail = tail.prev; tailmpNode; tmpNode.next = NULL**
		else	//Any other internal node
			loop: tmpNode = head to location -1
			tmpNode.next = tmpNode.next.next;
			**tmpNode.next.prev = tmpNode**
			
Time complexity: O(n)		Space complexity: O(1)

### Delete entire DSLL
Due to cyclic dependencies between adjoining nodes, just setting head and tail to null won't free up the node's memory. We have to traverese all the nodes and delete previous references.

    deleteLinkedList(head, tail)
	    loop (tmp: head to tail)
		    tmp.pre 
    deleteLinkedList(head, tail)
	    head= NULL
	    head = tail  = NULL
	    
Time complexity: O(n1)		Space complexity: O(1)	    

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEyNDgyMDc5MSwxNDcyNDgyMzQ1LC0xNz
U2MjQzMDgwLC0xODM5OTA4ODY1LDIwMTU3ODAyMjgsNDQ0NTY0
NTA5LDE3NjYyMjQ3MTYsMTAyMjkzODg0NywyNjY4NDc5MzMsLT
IzMDE2OTA5Myw1MDMxMzUzMTAsLTk1NTQ4MTgzMyw3MTQ4NjY1
Miw5OTg3NTg1NjQsOTY1MjA5NTg3LC0xMzIyOTc0MzAxLDE2Nj
E0MDI0OTgsMjI0OTg3NTg0LC01NTE2NjQ0MzgsLTUzNDg1Njgw
M119
-->