
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

### Properties of Recursion
 1. Same operation is performed multiple times with different inputs
 2. In every step, we try to make the problem smaller
 3. We mandatorily need to have a base condition, which tells system when to stop recursion.

Example: Finding an element in a BST.

    search(root, valueToBeSearched)
    	if(root equals null)   //Base condition
    		return null
    	else if(root.value equals valueToBeSearched) //Base con
    		return root
    	else if(root.value > valueToBeSearched) 
    		search(root.left, valueToBeSearched)
    	else if(root.value < valueToBeSearched)
    		search(root.right, valueToBeSearched)
	 
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTQ1MjQyNDcyOSwtNTQ1ODQzMDcyLC0xOT
k3MTAxOTY3LC0xMTAwODkyMDEyLC0yNDExOTQ2MzldfQ==
-->