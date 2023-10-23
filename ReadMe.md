## Index

- [Arrays Part-I (6/6)](#arrays-part-i-66)
- [Arrays Part-III (1/6)](#arrays-part-iii-16)
- [Arrays Part-IV (0/6)](#arrays-part-iv-06)
- [Linked List (0/6)](#linked-list-06)
- [Linked List Part-II (0/6)](#linked-list-part-ii-06)
- [Linked List and Arrays (0/6)](#linked-list-and-arrays-06)
- [Greedy Algorithm (0/6)](#greedy-algorithm-06)
- [Recursion (0/6)](#recursion-06)
- [Recursion and Backtracking (0/6)](#recursion-and-backtracking-06)
- [Binary Search (0/8)](#binary-search-08)
- [Heaps (0/6)](#heaps-06)
- [Stack and Queue (0/7)](#stack-and-queue-07)
- [Stack and Queue Part-II (0/10)](#stack-and-queue-part-ii-010)
- [String (0/6)](#string-06)
- [String Part-II (0/6)](#string-part-ii-06)
- [Binary Tree (0/12)](#binary-tree-012)
- [Binary Tree Part-II (0/8)](#binary-tree-part-ii-08)
- [Binary Tree Part-III (0/7)](#binary-tree-part-iii-07)
- [Binary Search Tree (0/7)](#binary-search-tree-07)
- [Binary Search Tree Part-II (0/8)](#binary-search-tree-part-ii-08)
- [Binary Trees - Miscellaneous (0/6)](#binary-trees---miscellaneous-06)
- [Graph (0/12)](#graph-012)
- [Graph Part-II (0/6)](#graph-part-ii-06)
- [Dynamic Programming (0/7)](#dynamic-programming-07)
- [Dynamic Programming Part-II (0/8)](#dynamic-programming-part-ii-08)
- [Trie (0/7)](#trie-07)
- [Operating System](#operating-system)
- [DBMS](#dbms)
- [Computer Networks](#computer-networks)
- [Project Overview](#project-overview)

---

# Arrays Part-I (6/6)

1. [73. Set Matrix Zeroes](https://leetcode.com/problems/set-matrix-zeroes/solutions/4181247/o-1-space-solution-explanation/)
   ```c++
   // approach -> use the first row and column as hash to store whether that row require to be zero or not 
        class Solution {
        public:
            void setZeroes(vector<vector<int>>& matrix) {
                bool setZerothRow0 = false;
                bool setZerothCol0 = false;
                int row=matrix.size();
                int col=matrix[0].size();
                for(int i=0;i<col;i++){
                    if(matrix[0][i]==0)
                        setZerothRow0=true;
                }
                for(int i=0;i<row;i++){
                    if(matrix[i][0]==0)
                        setZerothCol0=true;
                }
                for(int i=1;i<row;i++){
                    for(int j=1;j<col;j++){
                        if(matrix[i][j]==0){
                            matrix[0][j]=0;
                            matrix[i][0]=0;
                        }
                    }
                }
                for(int i=1;i<col;i++){
                    if(matrix[0][i]==0){
                        for(int j=1;j<row;j++){
                            matrix[j][i]=0;
                        }
                    }
                }
                for(int i=1;i<row;i++){
                    if(matrix[i][0]==0){
                        for(int j=1;j<col;j++){
                            matrix[i][j]=0;
                        }
                    }
                }
                if(setZerothRow0){
                    for(int i=0;i<col;i++)
                        matrix[0][i]=0;
                }
                if(setZerothCol0){
                    for(int i=0;i<row;i++)
                        matrix[i][0]=0;
                }
            }
        };
    ```
2. [118. Pascal's Triangle](https://leetcode.com/problems/pascals-triangle/solutions/4181284/simple-solution-explanation/)
   ```c++
        class Solution {
        public:
            vector<vector<int>> generate(int numRows) {
                vector<vector<int>> ans;
                ans.push_back({1});
                for(int i = 2;i<=numRows;i++){
                    vector<int>curLevel;
                    curLevel.push_back(1);
                    if(i>2){
                        for(int j=0;j<ans.back().size()-1;j++){
                            curLevel.push_back(ans.back()[j]+ans.back()[j+1]);
                        }
                    }
                    curLevel.push_back(1);
                    ans.push_back(curLevel);
                }
                return ans;
            }
        };
    ```
3. [31. Next Permutation](https://leetcode.com/problems/next-permutation/solutions/4198541/simple-explanation/)
   ```python
    class Solution:
        def nextPermutation(self, nums: List[int]) -> None:
            # Find the first element from the right that is smaller than the next element.
            i = len(nums) - 2
            while i >= 0 and nums[i] >= nums[i + 1]:
                i -= 1

            if i == -1:
                # If no such element is found, the array is in descending order.
                # In this case, reverse the entire array to get the smallest permutation.
                nums[:] = nums[:][::-1]
            else:
                # Find the rightmost element greater than nums[i].
                j = len(nums) - 1
                while nums[j] <= nums[i]:
                    j -= 1

                # Swap nums[i] and nums[j].
                nums[i], nums[j] = nums[j], nums[i]

                # Reverse the subarray to the right of i to ensure the smallest permutation.
                nums[i + 1:] = nums[i + 1:][::-1]
   ```
4. [53. Maximum Subarray](https://leetcode.com/problems/maximum-subarray/solutions/4183897/o-n-kadane-s-algorithm-explanation/)
   ```c++
        class Solution {
        public:
            int maxSubArray(vector<int>& nums) {
                int maximal = nums[0];
                int curSum = 0;
                for (int i = 0; i < nums.size(); i++) {
                    curSum += nums[i];
                    maximal = max(maximal, curSum);
                    if (curSum < 0)
                        curSum = 0;
                }
                return maximal;
            }
        };
   ```
5. [75. Sort Colors](https://leetcode.com/problems/sort-colors/solutions/4183886/2-pointer-explanation/)
   ```c++
        // Two-pointer approach 
        // O(N) time

        class Solution {
        public:
            void sortColors(vector<int>& nums) {
                int i = 0; // Pointer for 0s
                int j = nums.size(); // Pointer for 2s
                
                for (int k = 0; k < nums.size(); k++) {
                    if (nums[k] == 0) {
                        i++;
                    }
                    if (nums[k] == 2) {
                        j--;
                    }
                }
                
                int k = 0; // Initialize a new pointer for iterating through the array.

                while (i) {
                    nums[k] = 0;
                    i--;
                    k++;
                }

                while (k < j) {
                    nums[k] = 1;
                    k++;
                }

                while (k < nums.size()) {
                    nums[k] = 2;
                    k++;
                }
            }
        };
    ```
6. [121. Best Time to Buy and Sell Stock](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/solutions/4188659/simple-solution/)
    ```c++
        class Solution {
        public:
            int maxProfit(vector<int>& prices) {
                if (prices.empty()) {
                    return 0;
                }

                int curMin = prices[0];
                int maxProfit = 0;

                for (int i = 1; i < prices.size(); i++) {
                    if (prices[i] < curMin) {
                        curMin = prices[i];
                    } else {
                        maxProfit = max(maxProfit, prices[i] - curMin);
                    }
                }

                return maxProfit;
            }
        };
    ```

# Arrays Part-II (6/6)

1. [48. Rotate Image](https://leetcode.com/problems/rotate-image/solutions/4188728/simple-explanation/)
    ```c++
        class Solution {
            public:
                void rotate(vector<vector<int>>& matrix) {
                    int n = matrix.size();

                    // Transpose the matrix (swap rows with columns)
                    for (int i = 0; i < n; i++) {
                        for (int j = 0; j < i; j++) {
                            swap(matrix[i][j], matrix[j][i]);
                        }
                    }

                    // Reverse each row
                    for (int i = 0; i < n; i++) {
                        reverse(matrix[i].begin(), matrix[i].end());
                    }
                }
        };
    ```
2. [56. Merge Intervals](https://leetcode.com/problems/merge-intervals/solutions/4189074/simply-explanation/)
    ```python
    class Solution:
        def merge(self, intervals: List[List[int]]) -> List[List[int]]:
            if not intervals:
                return []

            intervals.sort(key=lambda x: x[0])
            merged = [intervals[0]]

            for i in range(1, len(intervals)):
                current_interval = intervals[i]
                previous_interval = merged[-1]

                if current_interval[0] <= previous_interval[1]:
                    previous_interval[1] = max(previous_interval[1], current_interval[1])
                else:
                    merged.append(current_interval)

            return merged
    ```
3. [88. Merge Sorted Array](https://leetcode.com/problems/merge-sorted-array/solutions/4188999/simple-explanation/)
   ```python
   class Solution:
    def merge(self, nums1: List[int], m: int, nums2: List[int], n: int) -> None:
        temp = []
        i,j=0,0
        while i<m and j<n:
            if nums1[i]<nums2[j]:
                temp.append(nums1[i])
                i+=1
            else:
                temp.append(nums2[j])
                j+=1
        while i<m:
            temp.append(nums1[i])
            i+=1
        while j<n:
            temp.append(nums2[j])
            j+=1
        for i,x in enumerate(temp):
            nums1[i]=x

    ```
4. [287. Find the Duplicate Number](https://leetcode.com/problems/find-the-duplicate-number/solutions/4197873/worst-medium-best-approach-explained/)
   ```python
   class Solution:
    def findDuplicate(self, nums: List[int]) -> int:
        slow, fast = 0, 0
        # Find the loop
        while True:
            slow = nums[slow]
            fast = nums[nums[fast]]
            if slow == fast:
                break
        slow = 0
        # Find the start of the loop
        while True:
            slow = nums[slow]
            fast = nums[fast]
            if slow == fast:
                return slow
    ```
5. [Missing and Repeating Number](https://www.codingninjas.com/studio/problems/873366?topList=striver-sde-sheet-problems&utm_source=striver&utm_medium=website&leftPanelTab=0)
    ```python
    def missingAndRepeating(arr, n):
    repeating = -1
    for num in arr:
        if arr[abs(num) - 1] < 0:
            repeating = abs(num)
        else:
            arr[abs(num) - 1] = -arr[abs(num) - 1]

    missing = -1
    for i in range(n):
        if arr[i] > 0:
            missing = i + 1
            break

    print(missing, repeating)
    ```
6. [Count Inversions](https://practice.geeksforgeeks.org/problems/inversion-of-array-1587115620/1)
   ```python
   class Solution:
    # Function to count inversions in the array.
    def inversionCount(self, Main_arr, n):
        # Create a temporary array to store the sorted elements.
        temp = Main_arr
        
        # Define a function to merge two sorted subarrays and count inversions.
        def merge(arr, si, mid, ei):
            l = si
            r = mid + 1
            temp = [0] * (ei - si + 1)  # Temporary array to store merged values.
            k = 0  # Index for temporary array.
            count = 0  # Variable to count inversions.

            while l <= mid and r <= ei:
                if arr[l] <= arr[r]:
                    temp[k] = arr[l]
                    k += 1
                    l += 1
                else:
                    # If arr[l] > arr[r], it's at the wrong position, and the number
                    # of elements it's wrongly positioned relative to is (mid - l + 1).
                    count += (mid - l + 1)
                    temp[k] = arr[r]
                    k += 1
                    r += 1

            while l <= mid:
                temp[k] = arr[l]
                k += 1
                l += 1
            while r <= ei:
                temp[k] = arr[r]
                k += 1
                r += 1

            k = 0
            for i in range(si, ei + 1):
                arr[i] = temp[k]
                k += 1
            return count

        # Define a function to perform merge sort and count inversions.
        def mergeSort(arr, si, ei):
            if si >= ei:
                return 0
            mid = (si + ei) >> 1
            left = mergeSort(arr, si, mid)
            right = mergeSort(arr, mid + 1, ei)
            join = merge(arr, si, mid, ei)
            return left + right + join

        # Call the mergeSort function to count inversions and return the count.
        return mergeSort(temp, 0, n - 1)
   ```

# Arrays Part-III (1/6)

1. [74. Search a 2D Matrix]()
2. [50. Pow(x, n)]()
3. [169. Majority Element]()
4. [229. Majority Element II]()
5. [62. Unique Paths](https://leetcode.com/problems/unique-paths/solutions/4198946/detailed-explanation/)
   ```python
        class Solution:
            def uniquePaths(self, m: int, n: int) -> int:
                # Initialize a 2D dynamic programming array with -1 values
                dp = [[-1] * n for i in range(m)]

                # Define a recursive function to calculate unique paths
                def recursion(x, y):
                    # Base case: If we reach the bottom-right corner, return 1 (one unique path)
                    if x == m - 1 and y == n - 1:
                        return 1
                    # Base case: If we go out of bounds, return 0 (no valid paths)
                    elif x > m - 1 or y > n - 1:
                        return 0
                    # Check if the value for the current cell has been computed
                    if dp[x][y] != -1:
                        return dp[x][y]

                    # Recursive case: Calculate the number of unique paths by summing two possibilities
                    # 1. Moving right: recursion(x+1, y)
                    # 2. Moving down: recursion(x, y+1)
                    right = recursion(x + 1, y)
                    down = recursion(x, y + 1)

                    # Update the value of dp[x][y] with the sum of the above two possibilities
                    dp[x][y] = right + down

                    return dp[x][y]

                # Start the recursion from the top-left corner (0, 0)
                return recursion(0, 0)

        
   ```
6. [493. Reverse Pairs]()
# Arrays Part-IV (0/6)

# Linked List (0/6)

# Linked List Part-II (0/6)

# Linked List and Arrays (0/6)

# Greedy Algorithm (0/6)

# Recursion (0/6)

# Recursion and Backtracking (0/6)

# Binary Search (0/8)

# Heaps (0/6)

# Stack and Queue (0/7)

# Stack and Queue Part-II (0/10)

# String (0/6)

# String Part-II (0/6)

# Binary Tree (0/12)

# Binary Tree Part-II (0/8)

# Binary Tree Part-III (0/7)

# Binary Search Tree (0/7)

# Binary Search Tree Part-II (0/8)

# Binary Trees - Miscellaneous (0/6)

# Graph (0/12)

# Graph Part-II (0/6)

# Dynamic Programming (0/7)

# Dynamic Programming Part-II (0/8)

# Trie (0/7)

# Operating System

# DBMS

# Computer Networks

# Project Overview
