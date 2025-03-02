[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/o-KsyuFI)
# AP-ASSIGNMENT-4-DAULAT-E13701
## Sorting and Searching
### https://leetcode.com/problems/merge-sorted-array/
```
class Solution {
public:
    void merge(vector<int>& nums1, int m, vector<int>& nums2, int n) {
        int i = m - 1; 
        int j = n - 1; 
        int k = m + n - 1; 

        while (j >= 0) {
            if (i >= 0 && nums1[i] > nums2[j]) {
                nums1[k--] = nums1[i--];
            } else {
                nums1[k--] = nums2[j--];
            }
        }
    }
};
```
![image](https://github.com/user-attachments/assets/68b9b6d9-0111-4513-b6a4-5e9ae7710c8b)

## https://leetcode.com/problems/first-bad-version/
```
// The API isBadVersion is defined for you.
// bool isBadVersion(int version);

class Solution {
public:
    int firstBadVersion(int n) {
        int left = 1;
        int right = n;

        while (left < right) {
            int mid = left + (right - left) / 2; 

            if (isBadVersion(mid)) {
                right = mid; 
            } else {
                left = mid + 1; 
            }
        }

        return left; 
    }
};
```
![image](https://github.com/user-attachments/assets/e3749d39-d4b7-45b2-8316-ae2e72acb16f)

## https://leetcode.com/problems/sort-colors/
```
class Solution {
public:
    void sortColors(vector<int>& nums) {
        int low = 0;
        int mid = 0;
        int high = nums.size() - 1;

        while (mid <= high) {
            if (nums[mid] == 0) {
               swap(nums[low], nums[mid]);
                low++;
                mid++;
            } else if (nums[mid] == 1) {
                mid++;
            } else { // nums[mid] == 2
               swap(nums[mid], nums[high]);
                high--;
            }
        }
    }
};
```
![image](https://github.com/user-attachments/assets/df58ae95-f916-4a4f-8a54-d62b66bcfc42)

## https://leetcode.com/problems/top-k-frequent-elements/
```
class Solution {
public:
    std::vector<int> topKFrequent(std::vector<int>& nums, int k) {
        // 1. Count the frequency of each element
        std::unordered_map<int, int> frequencyMap;
        for (int num : nums) {
            frequencyMap[num]++;
        }

        // 2. Create a min-heap (priority queue)
        std::priority_queue<std::pair<int, int>,
                            std::vector<std::pair<int, int>>,
                            std::greater<std::pair<int, int>>> minHeap;

        // 3. Populate the min-heap
        for (auto const& [num, frequency] : frequencyMap) {
            minHeap.push({frequency, num}); // Push {frequency, num}

            if (minHeap.size() > k) {
                minHeap.pop(); // Keep only the top k frequent elements
            }
        }

        // 4. Extract the top k elements from the min-heap
        std::vector<int> result;
        while (!minHeap.empty()) {
            result.push_back(minHeap.top().second); // Get the number (second element of pair)
            minHeap.pop();
        }

        // 5. Reverse the result to get the elements in descending order of frequency
        std::reverse(result.begin(), result.end());

        return result;
    }
};
```
![image](https://github.com/user-attachments/assets/033c74a1-62b9-461a-8768-1b257af8c9ff)

## https://leetcode.com/problems/kth-largest-element-in-an-array/
```
class Solution {
public:
    int findKthLargest(std::vector<int>& nums, int k) {
        std::priority_queue<int, std::vector<int>, std::greater<int>> minHeap; // Min-heap

        for (int num : nums) {
            minHeap.push(num);
            if (minHeap.size() > k) {
                minHeap.pop();
            }
        }

        return minHeap.top();
    }
};
```
![image](https://github.com/user-attachments/assets/08f97ee8-41be-4be2-9b7e-f017d476c5ef)

## https://leetcode.com/problems/find-peak-element/
```
class Solution {
public:
    int findPeakElement(std::vector<int>& nums) {
        int left = 0;
        int right = nums.size() - 1;

        while (left < right) {
            int mid = left + (right - left) / 2;

            if (nums[mid] < nums[mid + 1]) {
                // Peak is to the right
                left = mid + 1;
            } else {
                // Peak is at mid or to the left
                right = mid;
            }
        }

        return left; // left == right, which is the peak index
    }
};
```
![image](https://github.com/user-attachments/assets/504bd130-b5ea-48c5-a0c7-ade9f0c8b52e)

## https://leetcode.com/problems/merge-intervals/
```
class Solution {
public:
    std::vector<std::vector<int>> merge(std::vector<std::vector<int>>& intervals) {
        if (intervals.empty()) {
            return {};
        }

        // Sort intervals based on start times
        std::sort(intervals.begin(), intervals.end(), [](const std::vector<int>& a, const std::vector<int>& b) {
            return a[0] < b[0];
        });

        std::vector<std::vector<int>> merged;
        merged.push_back(intervals[0]);

        for (int i = 1; i < intervals.size(); ++i) {
            std::vector<int>& currentInterval = intervals[i];
            std::vector<int>& lastMergedInterval = merged.back();

            if (currentInterval[0] <= lastMergedInterval[1]) {
                // Overlapping intervals
                lastMergedInterval[1] = std::max(lastMergedInterval[1], currentInterval[1]);
            } else {
                // Non-overlapping intervals
                merged.push_back(currentInterval);
            }
        }

        return merged;
    }
};
```
![image](https://github.com/user-attachments/assets/a25c6b8d-2a0f-4b6c-b49c-b4f7128623af)

## https://leetcode.com/problems/search-in-rotated-sorted-array/
```
class Solution {
public:
    int search(vector<int>& nums, int target) {
        int s=0;
        int e=nums.size()-1;
        while(s<=e){
            int mid=s+(e-s)/2;
            if(nums[mid]==target){
                return mid;
            }
            if(nums[s]<=nums[mid]){
                if(nums[s]<=target&&target<=nums[mid]){
                    e=mid-1;
                }
                else{
                    s=mid+1;
                }
            }
            else{
            
                if(nums[mid]<=target&&target<=nums[e]){
                    s=mid+1;
                }
                else{
                    e=mid-1;
                }
            }
        }
        return -1;
    }
};
```
![image](https://github.com/user-attachments/assets/1d3f72d7-6bcf-4d0c-b0fc-effc55019d37)

## https://leetcode.com/problems/search-a-2d-matrix-ii/
```
class Solution {
public:
    bool searchMatrix(std::vector<std::vector<int>>& matrix, int target) {
        if (matrix.empty() || matrix[0].empty()) {
            return false;
        }

        int rows = matrix.size();
        int cols = matrix[0].size();

        int row = 0;
        int col = cols - 1; // Start from the top-right corner

        while (row < rows && col >= 0) {
            if (matrix[row][col] == target) {
                return true;
            } else if (matrix[row][col] < target) {
                // Target is greater, move down to the next row
                row++;
            } else {
                // Target is smaller, move left to the previous column
                col--;
            }
        }

        return false; // Target not found
    }
};
```
![image](https://github.com/user-attachments/assets/22f2ec62-d92a-4a8e-93fa-32257ef5eee6)

## https://leetcode.com/problems/kth-smallest-element-in-a-sorted-matrix/
```
class Solution {
public:
    int kthSmallest(std::vector<std::vector<int>>& matrix, int k) {
        int n = matrix.size();
        std::priority_queue<int> maxHeap; // Max-heap to store k smallest elements

        for (int i = 0; i < n; ++i) {
            for (int j = 0; j < n; ++j) {
                maxHeap.push(matrix[i][j]);
                if (maxHeap.size() > k) {
                    maxHeap.pop();
                }
            }
        }

        return maxHeap.top();
    }
};
```
![image](https://github.com/user-attachments/assets/a0b0115d-a79f-4892-a155-75facf352508)

## https://leetcode.com/problems/median-of-two-sorted-arrays/
```
class Solution {
public:
    double findMedianSortedArrays(std::vector<int>& nums1, std::vector<int>& nums2) {
        int m = nums1.size();
        int n = nums2.size();

        if (m > n) {
            // Ensure nums1 is the smaller array to optimize binary search
            return findMedianSortedArrays(nums2, nums1);
        }

        int low = 0;
        int high = m;
        int half = (m + n + 1) / 2; // Calculate half point

        while (low <= high) {
            int partitionX = (low + high) / 2;
            int partitionY = half - partitionX;

            int maxLeftX = (partitionX == 0) ? INT_MIN : nums1[partitionX - 1];
            int minRightX = (partitionX == m) ? INT_MAX : nums1[partitionX];

            int maxLeftY = (partitionY == 0) ? INT_MIN : nums2[partitionY - 1];
            int minRightY = (partitionY == n) ? INT_MAX : nums2[partitionY];

            if (maxLeftX <= minRightY && maxLeftY <= minRightX) {
                // Found the correct partition
                if ((m + n) % 2 == 0) {
                    // Even number of elements
                    return (std::max(maxLeftX, maxLeftY) + std::min(minRightX, minRightY)) / 2.0;
                } else {
                    // Odd number of elements
                    return std::max(maxLeftX, maxLeftY);
                }
            } else if (maxLeftX > minRightY) {
                // Move partitionX to the left
                high = partitionX - 1;
            } else {
                // Move partitionX to the right
                low = partitionX + 1;
            }
        }

        return 0.0; // Should not reach here
    }
};
```
![image](https://github.com/user-attachments/assets/5279efb2-a25c-4977-80dd-ce4a523a565b)

