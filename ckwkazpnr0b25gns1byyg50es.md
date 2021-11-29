## JavaScript Arrays 101 tips and tricks ft. LeetCode

# What is LeetCode?
 [LeetCode](https://leetcode.com/)  defines itself as
> LeetCode is the best platform to help you enhance your skills, expand your knowledge and prepare for technical interviews.

Is it truly the best? That's debatable (I will explain in another article) however it's very useful and it's been a standard for interviews - especially from FAANG companies (or MAANG now) - since the tech boom and the need to filter candidates. 
I personally like it because I generally enjoy challenging programming problems but most people use the platform just to prepare for interviews.

#  [JavaScript Arrays](https://github.com/bgdnvk/leetcode-arrays-101) 
LeetCode has something called "Explore Cards" so I decided to dive into Arrays
![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1638157836291/D8Alm_MZy.png)

Next you will find all the problems and its solutions with comments.  
[The full repository is here.](https://github.com/bgdnvk/leetcode-arrays-101) And you can find me on [Twitter @tekbog](https://twitter.com/tekbog)

###  [Max Consecutive Ones](https://leetcode.com/problems/max-consecutive-ones/) 
Given a binary array nums, return the maximum number of consecutive 1's in the array.

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1638165166569/e0UQUTwNm.png)

 [Solution:](https://github.com/bgdnvk/leetcode-arrays-101/blob/main/Max%20Consecutive%20Ones.js) 

``` 
var findMaxConsecutiveOnes = function(nums) {
     //initialize a variable to keep track of the max consecutive ones
    var contmax = 0;
    var cont = 0;
    for(let i = 0; i < nums.length; i++){
        // console.log("i is: "+nums[i]);
        if(nums[i]){
            //simple counter, if there's something in the array then add 1 to the counter
            cont++;
            // console.log("cont is "+cont);
        } else {
            console.log("it's a zero " +i)
            console.log("cont is "+cont)
            //check if the current consecutive ones is greater than the max consecutive ones we have already
            contmax = Math.max(cont, contmax);
            cont = 0;
        }
    }
    // console.log("contmax is "+contmax)
    // this is a ternary operator
    //https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Conditional_Operator
    // check which counter is higher and return it in case the last counter is higher
    return cont > contmax ? cont: contmax;
};
``` 
###   [Find Numbers with Even Number of Digits](https://leetcode.com/problems/find-numbers-with-even-number-of-digits/) 
Given an array nums of integers, return how many of them contain an even number of digits.

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1638165244970/fEVGg3p3M.png)

 [Solution: ](https://github.com/bgdnvk/leetcode-arrays-101/blob/main/Find%20Numbers%20with%20Even%20Number%20of%20Digits.js) 
```
 var findNumbers = function(nums) {
     //log for debugging
    console.log(...nums)
    //initialize a variable to keep track of the even numbers of digits
    let count = 0;
    //iterate through the array
    for (let num of nums){
        console.log(num.toString().split(''))
        //convert the number to a string to use string methods
        //we can clearly see the number of digits in every number now
        let innerNum = num.toString().split('')
        if (innerNum.length % 2 === 0){
            //if the number of digits is even, add one to the count
            count++
        }
    }
    return count;
};
``` 

###  [Squares of a Sorted Array](https://leetcode.com/problems/squares-of-a-sorted-array/) 

Given an integer array nums sorted in non-decreasing order, return an array of the squares of each number sorted in non-decreasing order.

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1638165274665/h-XiZZu-l.png)

 [Solution:](https://github.com/bgdnvk/leetcode-arrays-101/blob/main/Squares%20of%20a%20Sorted%20Array.js) 

```
 var sortedSquares = function(nums) {
    //create a new array to store the squares
    let arr = [];
    //push the squares of the numbers into the array
    for (let i of nums){
        arr.push(i*i)
    }
    console.log(arr)
    //sort the array in non-decreasing order
    arr.sort((a,b) => a-b)
    console.log(arr)
    return arr
};
``` 

###  [Duplicate Zeros](https://leetcode.com/problems/duplicate-zeros/) 

Given a fixed-length integer array arr, duplicate each occurrence of zero, shifting the remaining elements to the right.

Note that elements beyond the length of the original array are not written. Do the above modifications to the input array in place and do not return anything.

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1638165347271/vfc_jTWi_.png)


 [Solution:](https://github.com/bgdnvk/leetcode-arrays-101/blob/main/Duplicate%20Zeros.js) 

```
var duplicateZeros = function(arr) {
    for (var i=0; i<arr.length; i++) {
        if (arr[i] === 0) {
            //use the method splice to insert a new zero after the current zero
            arr.splice(i, 0, 0);
            //get rid of the last element since we just inserted a new zero so there's less space in the array
            arr.pop();
            //increment i to skip over the new zero we just inserted
            i+=1
        }
    }
};
``` 

### [Merge Sorted Array](https://github.com/bgdnvk/leetcode-arrays-101/blob/main/Merge%20Sorted%20Array.js)

You are given two integer arrays nums1 and nums2, sorted in non-decreasing order, and two integers m and n, representing the number of elements in nums1 and nums2 respectively.

Merge nums1 and nums2 into a single array sorted in non-decreasing order.

The final sorted array should not be returned by the function, but instead be stored inside the array nums1. To accommodate this, nums1 has a length of m + n, where the first m elements denote the elements that should be merged, and the last n elements are set to 0 and should be ignored. nums2 has a length of n.

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1638165468831/oqY4lIRoO.png)
[Solution:](https://github.com/bgdnvk/leetcode-arrays-101/blob/main/Merge%20Sorted%20Array.js)
```
 var merge = function(nums1, m, nums2, n) {
    // console.log(nums1.slice(0,m))
    for (let i = 0; i < n; i++){
        console.log(nums1[m])
        //since we know that from 'm' the array will be free we can start inserting elements there
        nums1[m] = nums2[i]
        console.log(nums1[m])
        //incremenet the index 'm' so we can insert the next element properly
        m++
    }
    //remember to sort the array in a non-decreasing order
    nums1.sort((a,b) => a - b);
    console.log(nums1)
};
```

### [Remove Element](https://leetcode.com/problems/remove-element/)
Given an integer array nums and an integer val, remove all occurrences of val in nums in-place. The relative order of the elements may be changed.

Since it is impossible to change the length of the array in some languages, you must instead have the result be placed in the first part of the array nums. More formally, if there are k elements after removing the duplicates, then the first k elements of nums should hold the final result. It does not matter what you leave beyond the first k elements.

Return k after placing the final result in the first k slots of nums.

Do not allocate extra space for another array. You must do this by modifying the input array in-place with O(1) extra memory.

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1638165593219/or9MrxDuz.png)
[Solution:](https://github.com/bgdnvk/leetcode-arrays-101/blob/main/Remove%20Element.js)
```
const removeElement = (nums, val) => {
    for (let i = 0; i < nums.length; i++) {
      if (nums[i] === val) {
        // use the method splice to remove the element that's equal to val
        nums.splice(i, 1);
        // decrement i by 1 to account for the splice
        i--;
      }
    }
    //since we removed elements from the array we just return the length of the array
    return nums.length;
  };
```

### [Remove Duplicates from Sorted Array](https://leetcode.com/problems/remove-duplicates-from-sorted-array/)

Given an integer array nums sorted in non-decreasing order, remove the duplicates in-place such that each unique element appears only once. The relative order of the elements should be kept the same.

Since it is impossible to change the length of the array in some languages, you must instead have the result be placed in the first part of the array nums. More formally, if there are k elements after removing the duplicates, then the first k elements of nums should hold the final result. It does not matter what you leave beyond the first k elements.

Return k after placing the final result in the first k slots of nums.

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1638165715220/zffyOFRey.png)

[Solution:](https://github.com/bgdnvk/leetcode-arrays-101/blob/main/Remove%20Duplicates%20from%20Sorted%20Array.js)
```
var removeDuplicates = function(nums) {
    // nums = [...new Set(nums)]
    // return nums.length
    // doesn't work cuz it has to be in place
    for (let i = 0; i < nums.length; i++) {
        //remove the next element if it's the same as the current element
        if (nums[i] === nums[i + 1]) {
            //use the method splice to remove the element
            nums.splice(i, 1)
            //decrement i to account for the splice
            i--
        }
    }
};
```

### [Check If N and Its Double Exist](https://leetcode.com/problems/check-if-n-and-its-double-exist/)

Given an array arr of integers, check if there exists two integers N and M such that N is the double of M ( i.e. N = 2 * M).

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1638165836366/HAlMXukPI.png)
[Solution:](https://github.com/bgdnvk/leetcode-arrays-101/blob/main/Check%20If%20N%20and%20Its%20Double%20Exist.js)

```
 var checkIfExist = function(arr) {
    //make a flag to check if there is a double
    //update it if it exists
    let res = false;
    console.log(`arr is ${arr}`);
    //use forEach to iterate through all the elements in the array
    arr.forEach( (e, i) => {
        //check if the double of e exists in the array with indexOf
        if(arr.indexOf(e*2) !== -1){
            //check we are not iterating over the same element
            if(arr.lastIndexOf(e*2) !== arr.indexOf(arr[i])){
                res = true
            }
            }
        }
    )
    return res
};
```

### [Valid Mountain Array](https://leetcode.com/problems/valid-mountain-array/)

Given an array of integers arr, return true if and only if it is a valid mountain array.

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1638165938571/eherID97E.png)
[Solution:](https://github.com/bgdnvk/leetcode-arrays-101/blob/main/Valid%20Mountain%20Array.js)
```
 var validMountainArray = function(arr) {
     //get the max of the array to know the "top" of the mountain
    let max = Math.max(...arr);
    //get its index as well
    let maxIndex = arr.indexOf(max);
    //debugging 101
    console.log(`max is ${max}`);
    console.log(`maxIndex is ${maxIndex}`);
    //check for edge cases
    if(maxIndex === 0 || maxIndex === arr.length-1){
        return false;
    }
    //iterate through the first half of the "mountain"
    for(let i = 0; i < maxIndex; i++){
        console.log('first half');
        console.log(`is is ${i} i+1 is ${i+1}`);
        //if the mountain isn't strictly increasing, return false
        if(arr[i] > arr[i+1] || arr[i] === arr[i+1]){
            return false;
        }
    }
    //iterate through the second half of the "mountain"
    for(let i = maxIndex; i < arr.length; i++){
        console.log('second half');
        console.log(`is is ${i} i+1 is ${i+1}`);
        //if the mountain isn't strictly decreasing, return false
        if(arr[i] < arr[i+1] || arr[i] === arr[i+1]){
            return false;
        }
    }
    //return true if the mountain is valid
    return true;
};
```

### [Replace Elements with Greatest Element on Right Side](https://leetcode.com/problems/replace-elements-with-greatest-element-on-right-side/)

Given an array arr, replace every element in that array with the greatest element among the elements to its right, and replace the last element with -1.

After doing so, return the array.

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1638166059954/wJt7ynnzM.png)
[Solution:](https://github.com/bgdnvk/leetcode-arrays-101/blob/main/Replace%20Elements%20with%20Greatest%20Element%20on%20Right%20Side.js)

```
 var replaceElements = function(arr) {
     console.log(arr);
    for(let i = 0; i < arr.length-1; i++){
        //assign max as the next element to check
        let max = arr[i+1];
        //iterate through the right side of the array
        for(let j = i+1; j<arr.length; j++){
            //check if there's an element that's greater than the current max
            if(arr[j] > max){
                max = arr[j];
            }
        }
        //put the max element as you finish the array
        arr[i] = max;
    }
    //put the last element as -1 since the problem asks for it
    arr[arr.length-1] = -1;
    return arr;
};
```

### [Remove Duplicates from Sorted Array](https://leetcode.com/problems/remove-duplicates-from-sorted-array/)

Given an integer array nums sorted in non-decreasing order, remove the duplicates in-place such that each unique element appears only once. The relative order of the elements should be kept the same.

Since it is impossible to change the length of the array in some languages, you must instead have the result be placed in the first part of the array nums. More formally, if there are k elements after removing the duplicates, then the first k elements of nums should hold the final result. It does not matter what you leave beyond the first k elements.

Return k after placing the final result in the first k slots of nums.

Do not allocate extra space for another array. You must do this by modifying the input array in-place with O(1) extra memory.

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1638166190740/y2mkWYFOb.png)
[Solution:](https://github.com/bgdnvk/leetcode-arrays-101/blob/main/Remove%20Duplicates%20from%20Sorted%20Array.js)
```
 var removeDuplicates = function(nums) {
    // nums = [...new Set(nums)]
    // return nums.length
    // doesn't work cuz it has to be in place
    for (let i = 0; i < nums.length; i++) {
        //remove the next element if it's the same as the current element
        if (nums[i] === nums[i + 1]) {
            //use the method splice to remove the element
            nums.splice(i, 1)
            //decrement i to account for the splice
            i--
        }
    }  
};
```

###[Move Zeroes](https://leetcode.com/problems/move-zeroes/)
Given an integer array nums, move all 0's to the end of it while maintaining the relative order of the non-zero elements.

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1638166313101/kNo8RTS14.png)
[Solution:](https://github.com/bgdnvk/leetcode-arrays-101/blob/main/Move%20Zeroes.js)
```
 var moveZeroes = function(nums) {
     console.log(nums);
     //edge case in case arr is empty
     if (nums.length === 0) return
     //make two pointers
     let positiveEleTracker = 0, j = 0
     //loop through array finding positive elements and filling the zeroes
     while (j < nums.length) {
         if (nums[j] !== 0) {
             //once we find a positive element swap it and keep count of positive elements
             nums[positiveEleTracker] = nums[j]
             positiveEleTracker++
         }
         //keep iterating through array
         j++
     }
     console.log(nums);
     //use the positiveEleTracker to fill the rest of the array with zeroes
     //fill the rest of the array with zeroes
     while (positiveEleTracker < nums.length) {
         nums[positiveEleTracker] = 0
         positiveEleTracker++
     }
     console.log(nums);
 }
```
### [Sort Array By Parity](https://leetcode.com/problems/sort-array-by-parity/)

Given an integer array nums, move all the even integers at the beginning of the array followed by all the odd integers.

Return any array that satisfies this condition.

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1638166415692/NsRP9sCM1.png)
[Solution:](https://github.com/bgdnvk/leetcode-arrays-101/blob/main/Sort%20Array%20By%20Parity.js)

```
 var sortArrayByParity = function(nums) {
     //edge case if arr length is 0
    if(nums.length === 0) return nums;
    //keep track where the even index is
    let evenIndex = 0;
    for(let i =0; i< nums.length; i++){
        //if even
        if(nums[i] % 2 == 0){
            console.log(nums[i]);
            //saving the val that's gonna get rewriten
            //this is the odd value
            let oddTempVal = nums[evenIndex];
            console.log("temp is "+oddTempVal);
            //if the value is even it should go at the beginning
            //there are no strict rules so any even value will do
            nums[evenIndex] = nums[i];
            //keep track of the even index
            evenIndex++;
            // place the odd value where the even value was
            nums[i] = oddTempVal;
        }
    }
    console.log(nums);
    return nums;
};
```

### [Remove Element](https://leetcode.com/problems/remove-element/)
Given an integer array nums and an integer val, remove all occurrences of val in nums in-place. The relative order of the elements may be changed.

Since it is impossible to change the length of the array in some languages, you must instead have the result be placed in the first part of the array nums. More formally, if there are k elements after removing the duplicates, then the first k elements of nums should hold the final result. It does not matter what you leave beyond the first k elements.

Return k after placing the final result in the first k slots of nums.

Do not allocate extra space for another array. You must do this by modifying the input array in-place with O(1) extra memory.

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1638166574328/MEHXw0Yke.png)
[Solution:](https://github.com/bgdnvk/leetcode-arrays-101/blob/main/Remove%20Element.js)
```
const removeElement = (nums, val) => {
    for (let i = 0; i < nums.length; i++) {
      if (nums[i] === val) {
        // use the method splice to remove the element that's equal to val
        nums.splice(i, 1);
        // decrement i by 1 to account for the splice
        i--;
      }
    }
    //since we removed elements from the array we just return the length of the array
    return nums.length;
  };
```

### [Height Checker](https://leetcode.com/problems/height-checker/)
A school is trying to take an annual photo of all the students. The students are asked to stand in a single file line in non-decreasing order by height. Let this ordering be represented by the integer array expected where expected[i] is the expected height of the ith student in line.

You are given an integer array heights representing the current order that the students are standing in. Each heights[i] is the height of the ith student in line (0-indexed).

Return the number of indices where heights[i] != expected[i].

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1638166670621/Ua4guUUyX.png)
[Solution:](https://github.com/bgdnvk/leetcode-arrays-101/blob/main/Height%20Checker.js)
```
 var heightChecker = function(heights) {

    //first copy the array using the spread operator
    //then sort the array to check the differences
    const sorted = [...heights].sort((a,b) => a - b)

    console.log(heights);
    console.log(sorted);
    //counter for the different elements
    let diffCount = 0;
    for(let i = 0; i<heights.length; i++){
        if(heights[i] !== sorted[i]){
            console.log("diff");
            diffCount++;
        }
    }
    console.log(diffCount);
    return diffCount;
};
```

### [Third Maximum Number](https://leetcode.com/problems/third-maximum-number/)
Given an integer array nums, return the third distinct maximum number in this array. If the third maximum does not exist, return the maximum number.

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1638166771816/cvUIPVqn0.png)
[Solution:](https://github.com/bgdnvk/leetcode-arrays-101/blob/main/Third%20Maximum%20Number.js)
```
 var thirdMax = function(nums) {
    //make a copy of the array without dupes
    const nonDupArr = [...new Set(nums)];
    //order the array from largest to smallest
    nonDupArr.sort((a,b) => b-a);
    console.log(nonDupArr);
    //get the third max number after sorting
    const thirdNum = nonDupArr[2];
    //if the array is less than 3 return the maximum number
    //if it's greater than 3 return the third maximum
    return nonDupArr.length < 3 ? Math.max(...nonDupArr) : thirdNum;
};
```

### [Find All Numbers Disappeared in an Array](https://leetcode.com/problems/find-all-numbers-disappeared-in-an-array/)
Given an array nums of n integers where nums[i] is in the range [1, n], return an array of all the integers in the range [1, n] that do not appear in nums.

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1638166872799/TbDOqDMfn.png)

[Solution:](https://github.com/bgdnvk/leetcode-arrays-101/blob/main/Find%20All%20Numbers%20Disappeared%20in%20an%20Array.js)
```
 var findDisappearedNumbers = function(nums) {
     //get the max range meaning it goes from [1,max]
    const maxRange = nums.length;
    console.log(maxRange);
    //array to store the missing numbers
    let res = [];
    //iterate from 1 to the range we need
    for(let i = 1; i <= maxRange; i++){
        //if the number is not in the array, push it to the array
        let found = false;
        //iterate through the array to see if the number is in the array
        for(let j = 0; j < nums.length; j++){
            if (i === nums[j]){
                //if the number is in the array, set found to true
                found = true;
            }
        }
        //only push the numbers that are not found
        if (!found){
            res.push(i);
        }
    }
    console.log(res);
    return res;
};
```

### [Squares of a Sorted Array](https://leetcode.com/problems/squares-of-a-sorted-array/)

Given an integer array nums sorted in non-decreasing order, return an array of the squares of each number sorted in non-decreasing order.

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1638166967014/9jKspMO0Q.png)

[Solution:](https://github.com/bgdnvk/leetcode-arrays-101/blob/main/Squares%20of%20a%20Sorted%20Array.js)
```
 var sortedSquares = function(nums) {
    //create a new array to store the squares
    let arr = [];
    //push the squares of the numbers into the array
    for (let i of nums){
        arr.push(i*i)
    }
    console.log(arr)
    //sort the array in non-decreasing order
    arr.sort((a,b) => a-b)
    console.log(arr)
    return arr
};
```