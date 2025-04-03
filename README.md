# JavaScript Interview Questions

## Theoretical Questions

### 1. What are the differences between var, let, and const?

### 2. What are closures in JavaScript? Can you give an example?

### 3. Explain the difference between == and === in JavaScript.

### 4. How does JavaScript handle asynchronous code execution?

## DOM & Event Handling

### 5. What is the difference between event.stopPropagation() and event.preventDefault()?

### 6. How do you select elements using JavaScript?

## Practical Questions

### 7. Finding the Longest Word in a Sentence

**Question:** Write a function that returns the longest word in a given sentence.

```javascript
function longestWord(sentence) {
  // Your code here
}

console.log(longestWord("The quick brown fox jumped over the lazy dog"));
// Expected output: "jumped"
```

**Answer:**

```javascript
function longestWord(sentence) {
  let words = sentence.split(" "); // Split sentence into words
  let longest = ""; // Initialize an empty string for the longest word

  for (let word of words) {
    if (word.length > longest.length) {
      longest = word; // Update longest if current word is longer
    }
  }

  return longest;
}

console.log(longestWord("The quick brown fox jumped over the lazy dog"));
// Expected output: "jumped"
```

### 8. Checking if Two Arrays are Equal (Ignoring Order)

**Question:** Write a function that checks if two arrays contain the same elements, regardless of order.

```javascript
function areArraysEqual(arr1, arr2) {
  // Your code here
}

console.log(areArraysEqual([1, 2, 3], [3, 2, 1])); // Expected output: true
console.log(areArraysEqual([1, 2, 3], [1, 2, 2])); // Expected output: false
```

**Answer:**

**First Approach:**

```javascript
function areArraysEqual(arr1, arr2) {
  if (arr1.length !== arr2.length) return false; // Different lengths mean they can't be equal

  let sortedArr1 = arr1.slice().sort(); // Sort a copy of arr1
  let sortedArr2 = arr2.slice().sort(); // Sort a copy of arr2

  return sortedArr1.every((value, index) => value === sortedArr2[index]);
}

console.log(areArraysEqual([1, 2, 3], [3, 2, 1])); // Expected output: true
console.log(areArraysEqual([1, 2, 3], [1, 2, 2])); // Expected output: false
console.log(areArraysEqual([1, 2, 3, 4], [1, 2, 3])); // Expected output: false
```

**Alternative approach:**

```javascript
function areArraysEqual(arr1, arr2) {
  if (arr1.length !== arr2.length) return false;

  let freqMap = {};

  for (let num of arr1) {
    freqMap[num] = (freqMap[num] || 0) + 1;
  }

  for (let num of arr2) {
    if (!freqMap[num]) return false; // If missing, return false
    freqMap[num]--; // Decrease count
  }

  return true;
}

console.log(areArraysEqual([1, 2, 3], [3, 2, 1])); // Expected output: true
console.log(areArraysEqual([1, 2, 3], [1, 2, 2])); // Expected output: false
```

### 9. Finding the First Non-Repeating Character

**Question:** Write a function to find the first non-repeating character in a string.

```javascript
function firstUniqueChar(str) {
  // Your code here
}

console.log(firstUniqueChar("aabbccde")); // Expected output: "d"
console.log(firstUniqueChar("aabb")); // Expected output: -1
```

**Answer:**

**First Approach (Using a Hash Map - O(n)):**
 
```javascript
function firstNonRepeatingChar(str) {
  let charCount = {}; // Object to store character frequencies

  // Step 1: Count occurrences of each character
  for (let char of str) {
    charCount[char] = (charCount[char] || 0) + 1;
  }

  // Step 2: Find the first character with a count of 1
  for (let char of str) {
    if (charCount[char] === 1) {
      return char; // Return the first non-repeating character
    }
  }

  return null; // If no non-repeating character is found
}

console.log(firstNonRepeatingChar("aabccdeff")); // Expected output: "b"
console.log(firstNonRepeatingChar("abcabc")); // Expected output: null
console.log(firstNonRepeatingChar("aabbcde")); // Expected output: "c"
```
 
**Alternative Approach: Using Map() (Preserves Order):**

```javascript
function firstNonRepeatingChar(str) {
  let map = new Map();

  for (let char of str) {
    map.set(char, (map.get(char) || 0) + 1);
  }

  for (let char of str) {
    if (map.get(char) === 1) return char;
  }

  return null;
}
```

### 10. Flatten a Nested Array

**Question:** Write a function to flatten a nested array into a single-level array.

```javascript
function flattenArray(arr) {
  // Your code here
}

console.log(flattenArray([1, [2, [3, 4], 5], 6])); // Expected output: [1, 2, 3, 4, 5, 6]
```

**Answer:**

**Approach 1: Using Recursion (Best for Deep Nesting):**

```javascript
function flatten(arr) {
  let result = [];

  for (let item of arr) {
    if (Array.isArray(item)) {
      result = result.concat(flatten(item)); // Recursively flatten
    } else {
      result.push(item); // Push non-array values
    }
  }

  return result;
}

console.log(flatten([1, [2, [3, [4, 5]]]]));
// Expected output: [1, 2, 3, 4, 5]
```

**Approach 2: Using reduce() (Concise, Functional Style):**

```javascript
function flatten(arr) {
  return arr.reduce((acc, item) =>
    acc.concat(Array.isArray(item) ? flatten(item) : item), []);
}

console.log(flatten([1, [2, [3, [4, 5]]]]));
// Expected output: [1, 2, 3, 4, 5]
```

**Approach 3: Using flat(Infinity) (Modern & Best for Simple Cases):**

```javascript
function flatten(arr) {
  return arr.flat(Infinity);
}

console.log(flatten([1, [2, [3, [4, 5]]]]));
// Expected output: [1, 2, 3, 4, 5]
```
