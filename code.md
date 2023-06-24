### Question #1: Turning Strings to URLs
URLs cannot have spaces. Instead, all spaces in a string are replaced with %20. Write an algorithm that replaces all spaces in a string with %20.

You may not use the replace() method or regular expressions to solve this problem. Solve the problem with and without recursion.

Example
* Input: "Jasmine Ann Jones"

* Output: "Jasmine%20Ann%20Jones"
```json
//EX1:
function urlConverter(inputString) {
  const inputArray = inputString.split(" ");
  const outputString = inputArray.join("%20");
  return outputString;
}

//EX2:
function urlConverterRecursive(inputString) {
  if (!inputString.includes(" ")) {
    return inputString;
  } else {
    let inputArray = inputString.split("");
    const spaceIndex = inputArray.findIndex((element) => element === " ");
    inputArray[spaceIndex] = "%20";
    const outputString = inputArray.join("");
    return urlConverterRecursive(outputString);
  }
}
```

### Question #2: Array Deduping
Write an algorithm that removes duplicates from an array. Do not use a function like filter() to solve this. Once you have solved the problem, demonstrate how it can be solved with filter(). Solve the problem with and without recursion.

Example
* Input: [7, 9, "hi", 12, "hi", 7, 53]

* Output: [7, 9, "hi", 12, 53]
```json
//EX1:
function arrayDeduper(inputArray) {
  let dedupedArray = [];
  inputArray.forEach(element => {
    if (!dedupedArray.includes(element)) {
      dedupedArray.push(element);
    } 
  });
  return dedupedArray;
}

//EX2:
function arrayDeduper2(inputArray) {
  const dedupedArray = [...new Set(inputArray)];
  return dedupedArray;
}

//EX3:
function arrayDeduperRecursive(inputArray, len = 0, deletable = false) {
  const sortedInput = inputArray.toSorted();
  if (len < sortedInput.length) {
    if (deletable) {
      sortedInput.splice(len,1);
      len--;
    }
    return arrayDeduperRecursive(sortedInput, len+1, sortedInput[len] === sortedInput[len+1])
  };
  return sortedInput;
}

//EX4:
function arrayDeduperFilter(inputArray) {
  const dedupedArray = inputArray.filter((char, index) => {
    return inputArray.indexOf(char) === index;
  });
  return dedupedArray;
}
```

### Question #3: Compressing Strings
Write an algorithm that takes a string with repeated characters and compresses them, using a number to show how many times the repeated character has been compressed. For instance, aaa would be written as 3a. Solve the problem with and without recursion.

Example
* Input: "aaabccdddda"

* Output: "3ab2c4da"
```json
//EX1:
function stringCompressorRecursive(inputString) {
  const inputArray = inputString.split("");
  let outputArray = [];
  for (let i = 0; i < inputArray.length; i++) {
    let count = 1;
    const checkNext = (e) => {
      if (e[i] === e[i+1]) {
        count = count +1;
        i++;
        checkNext(e);
      } else {
        if (count > 1) {
          outputArray.push(count);
        }
        outputArray.push(e[i])
      }
    }
    checkNext(inputArray);
  }
  const outputString = outputArray.join(""); 
  return outputString;  
}

//EX2:
function stringCompressor(inputString) {
  let compressedString = "";
  let count = 1;
  for (let i = 0; i < inputString.length; i++) {
    if (inputString[i] === inputString[i + 1]) {
      count++;
    } else {
      if (count > 1) {
        compressedString += count + inputString[i];
      } else {
        compressedString += inputString[i];
      }
      count = 1;
    }
  }
  return compressedString;
}
```

### Question #4: Checking for Uniqueness
Write an algorithm that determines whether all the elements in a string are unique. You may not convert the string into an array or use array methods to solve this problem. The algorithm should return a boolean.

Example
* Input: "hello"

* Output: false

* Input: "copyright"

* Output: true
```json
function stringChecker(inputString, len = 0) {
  if (len < inputString.length) {
    const checkChar = inputString[len];
    const checkString = inputString.replace(checkChar, "");
    if (checkString.includes(checkChar)) {
      return false;
    } else {
      return stringChecker(inputString, len+1);
    }
  }
  return true;
}
```

### Question #5: Array Sorting
Write an algorithm that sorts an array without using the sort() method. There are many different sorting algorithms — take the time to read about the following:

* Quick sort
* Merge sort
* Heap sort
* Insertion sort
* Bubble sort
* Selection sort
* You may implement any of the above algorithms (or your own) to solve the problem — as long as it doesn't use sort().

Example
* Input: [9, 2, 7, 12]

* Output: [2, 7, 9, 12]
```json
function arraySorter(inputArray) {
  if (inputArray.length <=1) {
    return inputArray;
  }
  const sortChar = inputArray[0];
  let leftArr = [];
  let rightArr = [];
  for (let i = 1; i < inputArray.length; i++) {
    if (inputArray[i] < sortChar) {
      leftArr.push(inputArray[i]);
    } else {
      rightArr.push(inputArray[i]);
    }
  }
  return [...arraySorter(leftArr), sortChar, ...arraySorter(rightArr)];
}
```