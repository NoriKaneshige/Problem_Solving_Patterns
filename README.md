# Problem_Solving_Patterns



> ## 1) Frequency Counter Pattern: :wink: 
> Write a function called same, which accepts two arrays.The function should return true if ever yvalue in the array has it's corresponding value squared in the second array.The frequency of values must be the same.

> naive solution, O(N^2)


``` js
function same(arr1, arr2){
    if(arr1.length !== arr2.length){
        return false;
    }
    for(let i = 0; i < arr1.length; i++){
        let correctIndex = arr2.indexOf(arr1[i] ** 2)
        if(correctIndex === -1) {
            return false;
        }
        console.log(arr2);
        arr2.splice(correctIndex,1)
    }
    return true;
}


```


> refactored solution, O(N)

``` js
function same(arr1, arr2){
    if(arr1.length !== arr2.length){
        return false;
    }
    let frequencyCounter1 = {}
    let frequencyCounter2 = {}
    for(let val of arr1){
        frequencyCounter1[val] = (frequencyCounter1[val] || 0) + 1
    }
    for(let val of arr2){
        frequencyCounter2[val] = (frequencyCounter2[val] || 0) + 1        
    }
    console.log(frequencyCounter1);
    console.log(frequencyCounter2);
    for(let key in frequencyCounter1){
        if(!(key ** 2 in frequencyCounter2)){
            return false
        }
        if(frequencyCounter2[key ** 2] !== frequencyCounter1[key]){
            return false
        }
    }
    return true
}
```


> Frequency Counter - validAnagram
> Given two strings, write a function to determine if the second string is an anagram of the first.
> An anagram is a word, phrase, or name formed by rearranging the letters of another, such as cinema, formed from iceman.
> Note: You may assume the string contains only lowercase alphabets.

> Time Complexity - O(n)


``` js
function validAnagram(first, second) {
  if (first.length !== second.length) {
    return false;
  }

  const lookup = {};

  for (let i = 0; i < first.length; i++) {
    let letter = first[i];
    // if letter exists, increment, otherwise set to 1
    lookup[letter] ? lookup[letter] += 1 : lookup[letter] = 1;
  }
  // console.log(lookup)

  for (let i = 0; i < second.length; i++) {
    let letter = second[i];
    // can't find letter or letter is zero then it's not an anagram
    if (!lookup[letter]) {
      return false;
    } else {
      lookup[letter] -= 1;
    }
  }
  console.log(lookup)
  return true;
}

console.log(validAnagram('', '')) // true
console.log(validAnagram('aaz', 'zza')) // false
console.log(validAnagram('anagram', 'nagaram')) // true
console.log(validAnagram("rat","car")) // false)
console.log(validAnagram('awesome', 'awesom')) // false
console.log(validAnagram('amanaplanacanalpanama', 'acanalmanplanpamana')) // false
console.log(validAnagram('qwerty', 'qeywrt')) // true
console.log(validAnagram('texttwisttime', 'timetwisttext')) // true

``` 



> Frequency Counter - sameFrequency
> Write a function called sameFrequency. Given two positive integers, find out if the two numbers have the same frequency of digits.
> Your solution MUST have the following complexities:

> Time: O(N)

``` js

function sameFrequency(num1, num2){
  let strNum1 = num1.toString();
  let strNum2 = num2.toString();
  if(strNum1.length !== strNum2.length) return false;
  
  let countNum1 = {};
  let countNum2 = {};
  
  for(let i = 0; i < strNum1.length; i++){
    countNum1[strNum1[i]] = (countNum1[strNum1[i]] || 0) + 1
  }
  
  for(let j = 0; j < strNum1.length; j++){
    countNum2[strNum2[j]] = (countNum2[strNum2[j]] || 0) + 1
  }
  
  for(let key in countNum1){
    if(countNum1[key] !== countNum2[key]) return false;
  }
 
  return true;
}


```



> Implement a function called, areThereDuplicates which accepts a variable number of arguments,
> and checks whether there are any duplicates among the arguments passed in. 
> You can solve this using the frequency counter pattern OR the multiple pointers pattern.

> Restrictions:
> Time - O(n)
> Space - O(n)

``` js
function areThereDuplicates() {
  let collection = {}
  for(let val in arguments){
    collection[arguments[val]] = (collection[arguments[val]] || 0) + 1
  }
  for(let key in collection){
    if(collection[key] > 1) return true
  }
  return false;
}

areThereDuplicates(1, 2, 3) // false
areThereDuplicates(1, 2, 2) // true 
areThereDuplicates('a', 'b', 'c', 'a') // true 

``` 



> ## 2) Multiple Pointers Pattern: :wink: 
> Write a function called sumZero which accepts a sorted array of integers.
> The function should find the first pair where the sum is 0.
> Rerutn an array that includes both values that sum to zero or undefined if a pair does not exist.

> O(N^2)

``` js
function sumZero(arr){
    for(let i = 0; i < arr.length; i++){
        for(let j = i+1; j < arr.length; j++){
            if(arr[i] + arr[j] === 0){
                return [arr[i], arr[j]];
            }
        }
    }
}


console.log(sumZero([-4,-3,-2,-1,0,1,2,5])) // [ -2, 2 ]
``` js


> refactored
> time complexity: O(N)
> space complexity: O(1)
``` js
function sumZero(arr){
	let left = 0;
	let right = arr.length - 1;
	while(left < right){
		let sum = arr[left] + arr[right];
		if(sum === 0){
			return [arr[left],arr[right]];
		} else if(sum > 0){
			right--;
		} else {
			left++;
		}
	}
}

console.log(sumZero([-4,-3,-2,-1,0,1,2,5])) // [ -2, 2 ]
```



> Multiple Pointers - countUniqueValues
> Implement a function called countUniqueValues, which accepts a sorted array,
> and counts the unique values in the array. There can be negative numbers in the array,
> but it will always be sorted.

> Time Complexity - O(n)
> Space Complexity - O(n)

> Bonus
> You must do this with constant or O(1) space and O(n) time.

``` js
function countUniqueValues(arr){
    if(arr.length === 0) return 0;
    var i = 0;
    for(var j = 1; j < arr.length; j++){
        if(arr[i] !== arr[j]){
            i++;
            arr[i] = arr[j]
        }
    }
    return i + 1;
}
console.log(countUniqueValues([1,2,2,5,7,7,99])) // 5
console.log(countUniqueValues([1,1,1,1,1,2])) // 2
console.log(countUniqueValues([1,2,3,4,4,4,7,7,12,12,13])) // 7
console.log(countUniqueValues([])) // 0
console.log(countUniqueValues([-2,-1,-1,0,1])) // 4
``` 


> Implement a function called, areThereDuplicates which accepts a variable number of arguments,
> and checks whether there are any duplicates among the arguments passed in. 
> You can solve this using the frequency counter pattern OR the multiple pointers pattern.

> Restrictions:
> Time - O(n)
> Space - O(n)

> Bonus:
> Time - O(n log n)
> Space - O(1)

``` js
function areThereDuplicates(...args) {
  // Two pointers
  args.sort((a,b) => a > b);
  let start = 0;
  let next = 1;
  while(next < args.length){
    if(args[start] === args[next]){
        return true
    }
    start++
    next++
  }
  return false
}

console.log(areThereDuplicates(1, 2, 3)) // false
console.log(areThereDuplicates(1, 2, 2)) // true 
console.log(areThereDuplicates('a', 'b', 'c', 'a')) // true 


// One line solution:
function areThereDuplicates() {
  return new Set(arguments).size !== arguments.length;
}
```



> Write a function called averagePair. Given a sorted array of integers and a target average,
> determine if there is a pair of values in the array where the average of the pair equals the target average.
> There may be more than one pair that matches the average target.

> Bonus Constraints:
> Time: O(N)
> Space: O(1)

``` js
function averagePair(arr, num){
  let start = 0
  let end = arr.length-1;
  while(start < end){
    let avg = (arr[start]+arr[end]) / 2 
    if(avg === num) return true;
    else if(avg < num) start++
    else end--
  }
  return false;
}

console.log(averagePair([1,2,3],2.5)) // true
console.log(averagePair([1,3,3,5,6,7,10,12,19],8)) // true
console.log(averagePair([-1,0,3,4,5,6], 4.1)) // false
console.log(averagePair([],4)) // false
```


> Write a function called isSubsequence which takes in two strings and checks 
> whether the characters in the first string form a subsequence of the characters in the second string.
> In other words, the function should check whether the characters in the first string appear
> somewhere in the second string, without their order changing.

> Your solution MUST have AT LEAST the following complexities:

> Time Complexity - O(N + M)
> Space Complexity - O(1)

``` js
function isSubsequence(str1, str2) {
  var i = 0;
  var j = 0;
  if (!str1) return true;
  while (j < str2.length) {
    if (str2[j] === str1[i]) i++;
    if (i === str1.length) return true;
    j++;
  }
  return false;
}

console.log(isSubsequence('hello', 'hello world')); // true
console.log(isSubsequence('sing', 'sting')); // true
console.log(isSubsequence('abc', 'abracadabra')); // true
console.log(isSubsequence('abc', 'acb')); // false (order matters)
```



> Recursive but not O(1) Space

``` js
function isSubsequence(str1, str2) {
  if(str1.length === 0) return true
  if(str2.length === 0) return false
  if(str2[0] === str1[0]) return isSubsequence(str1.slice(1), str2.slice(1))  
  return isSubsequence(str1, str2.slice(1))
}

console.log(isSubsequence('hello', 'hello world')); // true
console.log(isSubsequence('sing', 'sting')); // true
console.log(isSubsequence('abc', 'abracadabra')); // true
console.log(isSubsequence('abc', 'acb')); // false (order matters)
```


> ## 3) Sliding Window Pattern: :wink: 
> Write a function called maxSubarraySum which accepts an array of integers and a number called n.
> The function should calculate the maximum sum of n consecutive elements in the array.

> naive, really inefficinet
``` js
function maxSubarraySum(arr, num) {
  if ( num > arr.length){
    return null;
  }
  var max = -Infinity;
  for (let i = 0; i < arr.length - num + 1; i ++){
    temp = 0;
    for (let j = 0; j < num; j++){
      temp += arr[i + j];
    }
    if (temp > max) {
      max = temp;
    }
  }
  return max;
}

console.log(maxSubarraySum([2,6,9,2,1,8,5,6,3],3)) // 19
```

> refactored
> time complexity: O(N)

``` js
function maxSubarraySum(arr, num){
  let maxSum = 0;
  let tempSum = 0;
  if (arr.length < num) return null;
  for (let i = 0; i < num; i++) {
    maxSum += arr[i];
  }
  tempSum = maxSum;
  for (let i = num; i < arr.length; i++) {
    tempSum = tempSum - arr[i - num] + arr[i];
    maxSum = Math.max(maxSum, tempSum);
  }
  return maxSum;
}

console.log(maxSubarraySum([2,6,9,2,1,8,5,6,3],3)) // 19
```


> Sliding Window - maxSubarraySum
> Given an array of integers and a number, write a function called maxSubarraySum,
> which finds the maximum sum of a subarray with the length of the number passed to the function.

> Note that a subarray must consist of consecutive elements from the original array.
> In the first example below, [100, 200, 300] is a subarray of the original array, but [100, 300] is not.

> maxSubarraySum([100,200,300,400], 2) // 700

> Constraints:
> Time Complexity - O(N)
> Space Complexity - O(1)

``` js
function maxSubarraySum(arr, num){
    if (arr.length < num) return null;
 
    let total = 0;
    for (let i=0; i<num; i++){
       total += arr[i];
    }
    let currentTotal = total;
    for (let i = num; i < arr.length; i++) {
       currentTotal += arr[i] - arr[i-num];
       total = Math.max(total, currentTotal);
    }
    return total;
}

console.log(maxSubarraySum([100,200,300,400], 2)) // 700
console.log(maxSubarraySum([1,4,2,10,23,3,1,0,20], 4))  // 39 
console.log(maxSubarraySum([-3,4,0,-2,6,-1], 2)) // 5
console.log(maxSubarraySum([3,-2,7,-4,1,-1,4,-2,1],2)) // 5
console.log(maxSubarraySum([2,3], 3)) // null
```


> Sliding Window - minSubArrayLen
> Write a function called minSubArrayLen which accepts two parameters - an array of positive integers and a positive integer.

> This function should return the minimal length of a contiguous subarray of which the sum is greater than or equal 
> to the integer passed to the function. If there isn't one, return 0 instead.

> Time Complexity - O(n)
> Space Complexity - O(1)

``` js
function minSubArrayLen(nums, sum) {
  let total = 0;
  let start = 0;
  let end = 0;
  let minLen = Infinity;
 
  while (start < nums.length) {
    // if current window doesn't add up to the given sum then 
    // move the window to right
    if(total < sum && end < nums.length){
      total += nums[end];
      end++;
    }
    // if current window adds up to at least the sum given then
    // we can shrink the window 
    else if(total >= sum){
      minLen = Math.min(minLen, end-start);
      total -= nums[start];
      start++;
    } 
    // current total less than required total but we reach the end, need this or else we'll be in an infinite loop 
    else {
      break;
    }
  }
 
  return minLen === Infinity ? 0 : minLen;
}


console.log(minSubArrayLen([2,3,1,2,4,3], 7)) // 2 -> because [4,3] is the smallest subarray
console.log(minSubArrayLen([2,1,6,5,4], 9)) // 2 -> because [5,4] is the smallest subarray
console.log(minSubArrayLen([3,1,7,11,2,9,8,21,62,33,19], 52)) // 1 -> because [62] is greater than 52
console.log(minSubArrayLen([1,4,16,22,5,7,8,9,10],39)) // 3
console.log(minSubArrayLen([1,4,16,22,5,7,8,9,10],55)) // 5
console.log(minSubArrayLen([4, 3, 3, 8, 1, 2, 3], 11)) // 2
console.log(minSubArrayLen([1,4,16,22,5,7,8,9,10],95)) // 0
```


> Sliding Window - findLongestSubstring
> Write a function called findLongestSubstring, which accepts a string and returns the length of the longest substring 
> with all distinct characters.

> Time Complexity - O(n)

``` js
function findLongestSubstring(str) {
  let longest = 0;
  let seen = {};
  let start = 0;
 
  for (let i = 0; i < str.length; i++) {
    let char = str[i];
    if (seen[char]) {
      start = Math.max(start, seen[char]);
    }
    // index - beginning of substring + 1 (to include current in count)
    longest = Math.max(longest, i - start + 1);
    // store the index of the next char so as to not double count
    seen[char] = i + 1;
  }
  return longest;
}

console.log(findLongestSubstring('')) // 0
console.log(findLongestSubstring('rithmschool')) // 7
console.log(findLongestSubstring('thisisawesome')) // 6
console.log(findLongestSubstring('thecatinthehat')) // 7
console.log(findLongestSubstring('bbbbbb')) // 1
console.log(findLongestSubstring('longestsubstring')) // 8
console.log(findLongestSubstring('thisishowwedoit')) // 6
```
