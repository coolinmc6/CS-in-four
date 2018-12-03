# Four Semesters of Computer Science in 5 Hours

**Resources**

[http://btholt.github.io/four-semesters-of-cs/](http://btholt.github.io/four-semesters-of-cs/)

[http://bigocheatsheet.com/](http://bigocheatsheet.com/)

**Part 2:** 

[https://btholt.github.io/four-semesters-of-cs-part-two/](https://btholt.github.io/four-semesters-of-cs-part-two/)

## Big O and Recursion
- look at the big picture
- we can ignore the little parts and focus on the big parts
- constant time: O(1)
- O(log n) => diminishing time for each additional item added. If the first 10 items takes 10 seconds, the next 10 could take 5 seconds, and then the next 10 items takes 2.5 seconds
- the first line of Recursion is when you STOP recursing. If you don't write this, your function will just keep running
- 

## Sorting Algorithms

### Bubble Sort
- not really used in production code
- the outer loop continues running if one of the numbers was swapped
- O(n^2)
- Why? There's an inner loop checking to see if the indexes of the array need to be swapped and then the outer
loop just checks whether or not something was swapped.
- This is a very inefficient algorithm because it keeps checking the array if it's sorted regardless of whether
we sorted it or not. Algorithms we'll learn in the future allow us to not check larger and larger parts of the
array, saving us time.

```js
var bubbleSort = nums => {  
  do {
    var swapped = false;
    for (var i = 0; i < nums.length; i++) {
      snapshot(nums);
      if (nums[i] > nums[i+1]) {
        var temp = nums[i];
        nums[i] = nums[i+1];
        nums[i+1] = temp;
        swapped = true;
      }
    }
  } while(swapped);
  snapshot(nums);
};

// BubbleSort from AlgoCasts
function bubbleSort(arr) {
	// implement bubblesort
	for(let i = 0; i < arr.length; i++) {
		for(let j = 0; j < (arr.length - i - 1); j++) {
			if(arr[j] > arr[j+1]) {
				const lesser = arr[j+1];
				arr[j+1] = arr[j];
				arr[j] = lesser;
			}
		}
	}
	// return the sorted array
	return arr;
}
```

### Insertion Sort

```js

var insertionSort = nums => {  
  for (let i = 1; i < nums.length; i++) {
    for (let j = 0; j < i; j++) {
      snapshot(nums);
      if (nums[i] < nums[j]) {
        let spliced = nums.splice(i, 1);
        nums.splice(j, 0, spliced[0]);
      }
    }
  }
};
```

### Merge Sort
- this is most often the one that we'd use
- Divide and Conquer which means it's going to use recursion
- Take a big list and break into two smaller lists. It does that by breaking
- MergeSort is also stable which means if you have equivalent elements, it will keep their original order in the array. This is sometimes important
- Big O is `O(n log n)`
- to write recursion, you have to get used to "using" something before you've actually written it. You
"use" it by assuming that it'll work just so you can have the function recursing

```js
const mergeSort = nums => {
  if (nums.length < 2) {
    return nums;
  }
  const length = nums.length;
  const middle = Math.floor(length / 2);
  const left = nums.slice(0, middle);
  const right = nums.slice(middle);
  
  return merge(mergeSort(left), mergeSort(right));
};

const merge = (left, right) => {
  
  const results = [];
  
  while (left.length && right.length) {
    
    if (left[0] <= right[0]) {
      results.push(left.shift());
    }
    else {
      results.push(right.shift());
    }
  }
  
  return results.concat(left, right);
};

////////////////////////////////////////////////////////
// AlgoCasts
function mergeSort(arr) {
  if(arr.length === 1) {
    return arr;
  }

  const center = Math.floor(arr.length / 2);

  const left = arr.slice(0,center);
  const right = arr.slice(center);

  return merge(mergeSort(left), mergeSort(right));
}

function merge(left, right) {
  const results = [];

  while(left.length && right.length) {
    if(left[0] < right[0]) {
      results.push(left.shift())
    } else {
      results.push(right.shift())
    }
  }

  return [...results, ...left, ...right];
}
```


### Quicksort
- this is another Divide and Conquer algorithm
- there are many variations of Quicksort, this is just one of them
- It's a recursive algorithm
- we have an array and then pick a pivot. Everything smaller than that pivot goes into one list, the
the other list gets everything greater. The pivot is often the last element
- the pivot isn't actually passed down; it stays out of the two lists
- you then concatenate
- Big O: O(n log n)
- You can get an n-squared Big O if the array is sorted and you pick the last item as the index
- Quicksort 3 is the most popular implementation of Quicksort

```js
const quickSort = nums => {
  if (nums.length <= 1) return nums;
  
  const pivot = nums[nums.length-1];
  const left = [];
  const right = [];
  
  for (let i = 0; i < nums.length-1; i++) {
    if (nums[i] < pivot) {
      left.push(nums[i]);
    }
    else {
      right.push(nums[i]);
    }
  }
  return [...quickSort(left), pivot, ...quickSort(right)];
};
```

## Data Structure Interfaces

### Interfaces
- interfaces are something that we know how to interact with it but have no idea how it works on the inside

### Set
- A set is more of an object, not an array
- a set has no duplicates
- it's very useful with a large data set and you don't want duplicates
- they basically do add, removes and contains
- there is no sense of order

### Map
- Maps also known as dictionaries
- Maps are closer to JavaScript objects
- Maps don't have prototypes, inheritance, methods, or anything of that sort
- Maps have a **set** of key-value pairs
- JavaScript has weakmaps and weaksets
- 2ality - JavaScript stuff

### Stack
- Stacks are an interface and are last-in-first-out (only push and only pop)
- programming is a stack - you are putting functions onto the stack, doing them, and then pushing them off

### Queue
- Queue is first-in-first-out; unlikely stack which is LIFO
- Queues are "fair"
- 


## Implementing Data Structures

### ArrayList

- An ArrayList is close to what most people know as arrays in JavaScript
- JavaScript i a garbage-collected language so we don't have to worry about allocation and de-allocation, it is
simplified
- your index is descriptive of where an item is in memory
- With ArrayList implementations, you have to worry about collapsing the array. So if you delete index 3
from the array `[a, b, c, d, e, f, g]`, you'll have a,b,c,(blank),e,f,g and now my index is no longer descriptive of where the thing is.
- So now I have to go shift everything over. And if you have an array of 10 million objects and you delete number two, that's actually hugely expensive, because you have to shift you know, 9,999,998 objects over.
- Lookups are cheap (i.e. go to index 4) whereas deletions and inserts are expensive.
- You are optimizing for gets and de-optimizing for deletes and insert intos.
- When figuring out whether to use ArrayList, you need examine whether you are going to be doing a lot more
deletes/inserts or gets
- ArrayLists do gets well while LinkedLists do deletes/insertions well

```js
class ArrayList {
  constructor() {
    this.length = 0;
    this.data = {};
  }
  // add value to end of ArrayList
  push(value) {
    this.data[this.length] = value;
    this.length++;
  }

  pop() {
    const ans = this.data[this.length-1];
    delete this.data[this.length-1];
    this.length--;
    return ans;
  }
  get(index) {
    return this.data[index];
  }
  delete(index) {
    const ans = this.data[index];
    this._collapseTo(index);
    return ans;
  }
  _collapseTo(index) {
    for (let i = index; i < this.length; i++) {
      this.data[i] = this.data[i+1];
    }
    delete this.data[this.length-1];
    this.length--;
  }
  serialize() {
    return this.data;
  }
}
```

### Linked List

- with linked lists, gets are expensive but deletes are cheap

```js
class LinkedList {
  constructor() {
    this.tail = this.head = null;
    this.length = 0;
  }
  push(value) {
    const node = new Node(value);
    this.length++;
    if (!this.head) {
     this.head = node;
    }
    else {
      this.tail.next = node;
    }
    this.tail = node;
  }
  pop() {
    if (!this.head) return null;
    if (this.head === this.tail) {
      const node = this.head;
      this.head = this.tail = null;
      return node.value;
    }
    const penultimate = this._find(null, (value, nodeValue, i, current) => current.next === this.tail );
    const ans = penultimate.next.value;
    penultimate.next = null;
    this.tail = penultimate;
    this.length--;
    return ans;
  }
  _find(value, test=this.test) {
    let current = this.head;
    let i = 0;
    while(current) {
      if (test(value, current.value, i, current)) {
        return current;
      }
      current = current.next;
      i++;
    }
    return null;
  }
  get(index) {
    const node = this._find(index, this.testIndex);
    if (!node) return null;
    return node.value;
  }
  delete(index) {
    if (index === 0) {
      const head = this.head;
      if (head) {
        this.head = head.next;
      }
      else {
        this.head = null;
      }
      this.length--;
      return head.value;
    }
    
    const node = this._find(index-1, this.testIndex);
    const excise = node.next;
    if (!excise) return null;    
    node.next = excise.next;    
    if (!node.next.next) this.tail = node.next;
    this.length--;
    return excise.value;
  }
  test(search, nodeValue) {
    return search === nodeValue;
  }
  testIndex(search, __, i) {
    return search === i;
  }
  serialize() {
    const ans = [];
    let current = this.head;
    if (!current) return ans;
    while (current) {
      ans.push(current.value);
      current = current.next;
    }
    return ans;
  }
}



class Node {
  constructor(value) {
    this.value = value;
    this.next = null;
  }
}


```

- One line if-statement: `if (!node.next.next) this.tail = node.next;`

### Binary Search Tree
- every node on a BST has either 0, 1, or 2 nodes
- Lesser is to the left, Greater is to the right
- Lookups are log n

```js
class Tree {
  constructor() {
    this.root = null;
  }
  add(value) {
    if (this.root === null) {
      this.root = new Node(value);
    }
    else {
      let current = this.root;
      while(true) {
        if (current.value > value) {
          // go left
          
          if (current.left) {
            current = current.left;
          }
          else {
            current.left = new Node(value);
            break;
          }
        }
        else {
          // go right
          if (current.right) {
            current = current.right;
          }
          else {
            current.right = new Node(value);
            break;
          }    
        }
      }
    }
    return this;
  }
  toJSON() {
    return JSON.stringify(this.root.serialize(), null, 4);
  }
  toObject() {
    return this.root.serialize();
  }
}

class Node {
  constructor(value=null, left=null, right=null) {
    this.left = left;
    this.right = right;
    this.value = value;
  }
  serialize() {
    const ans = { value: this.value };
    ans.left = this.left === null ? null : this.left.serialize();
    ans.right = this.right === null ? null : this.right.serialize();
    return ans;
  }
}
```
- BST's would be good for any kind of ordered data
- one example was autocomplete for search

### AVL Tree
- by definition, an AVL is a BST but not vice versa.
- An AVL tree is designed to keep the tree pretty flat
- worst case is O (log n)
- leaf nodes don't have children
- a double rotation is a left rotation on one of the children and then a right rotation on the root node

```js
class Tree {
  constructor() {
    this.root = null;
  }
  add(value) {
    if (!this.root) {
      this.root = new Node(value);
    }
    else {
      this.root.add(value);
    }
  }
  toJSON() {
    return JSON.stringify(this.root.serialize(), null, 4);
  }
  toObject() {
    return this.root.serialize();
  }
}

class Node {
  constructor(value=null, left=null, right=null) {
    this.left = left;
    this.right = right;
    this.value = value;
    this.height = 1;
  }
  add(value) {
    
    if (value < this.value) {
      // go left
      
      if (this.left) {
        this.left.add(value);
      }
      else {
        this.left = new Node(value);
      }
      if (!this.right || this.right.height < this.left.height) {
        this.height = this.left.height + 1;
      }      
    } else {
      // go right
      
      if (this.right) {
        this.right.add(value);
      }
      else {
        this.right = new Node(value);
      }
      if (!this.left || this.right.height > this.left.height) {
        this.height = this.right.height + 1;
      } 
    }
    this.balance();
  }
  balance() {
    const rightHeight = (this.right) ? this.right.height : 0;
    const leftHeight = (this.left) ? this.left.height : 0;
    
    console.log( this.value, leftHeight, rightHeight );
    
    if ( leftHeight > rightHeight + 1 ) {
      const leftRightHeight = (this.left.right) ? this.left.right.height : 0;
      const leftLeftHeight = (this.left.left) ? this.left.left.height : 0;
      
      if (leftRightHeight > leftLeftHeight) {
        this.left.rotateRR();
      }
      
      this.rotateLL();
    }
    else if ( rightHeight > leftHeight + 1 ) {
      const rightRightHeight = (this.right.right) ? this.right.right.height : 0;
      const rightLeftHeight = (this.right.left) ? this.right.left.height : 0;
      
      if (rightLeftHeight > rightRightHeight) {
        this.right.rotateLL();
      }
      
      this.rotateRR();
    }
  }
  rotateRR() {
    const valueBefore = this.value;
    const leftBefore = this.left;
    this.value = this.right.value;
    this.left = this.right;
    this.right = this.right.right;
    this.left.right = this.left.left;
    this.left.left = leftBefore;
    this.left.value = valueBefore;
    this.left.updateInNewLocation();
    this.updateInNewLocation();
  }
  rotateLL() {
    const valueBefore = this.value;
    const rightBefore = this.right;
    this.value = this.left.value;
    this.right = this.left;
    this.left = this.left.left;
    this.right.left = this.right.right;
    this.right.right = rightBefore;
    this.right.value = valueBefore;
    this.right.updateInNewLocation();
    this.updateInNewLocation();
  }
  updateInNewLocation() {
    if (!this.right && !this.left) {
      this.height = 1;
    }
    else if (!this.right || (this.left && this.right.height < this.left.height)) {
        this.height = this.left.height + 1;
    }
    else { //if (!this.left || this.right.height > this.left.height)
        this.height = this.right.height + 1;
    }
  }
  serialize() {
    const ans = { value: this.value };
    ans.left = this.left === null ? null : this.left.serialize();
    ans.right = this.right === null ? null : this.right.serialize();
    ans.height = this.height;
    return ans;
  }
}
```

### Hash Tables
- the key itself is where to find it in memory
- hashing algorithms must be indempotent (like a pure function, have no side-effects)
- 

## Functional Programming 101
- Not having side effects means that it doesn't affect variables outside the function. You should be able
to do a function and given the same input, deliver the same answer ALWAYS
- Map is a higher order function
- Reduce you condense an array into a single value (or object)
- 










