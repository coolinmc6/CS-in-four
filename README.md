# Four Semesters of Computer Science in 5 Hours

**Resources**
[http://btholt.github.io/four-semesters-of-cs/](http://btholt.github.io/four-semesters-of-cs/)

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


### Merge Sort

### Quicksort

## Data Structure Interfaces

## Implementing Data Structures