import java.util.Arrays;
import java.util.HashMap;
import java.util.Map;

public class Solutions {

    public static void main(String[] args) {
        



        System.out.println("Answer 2 - "); 

        /*<aside>
💡 **Question 2**

You are given an m x n integer matrix matrix with the following two properties:

- Each row is sorted in non-decreasing order.
- The first integer of each row is greater than the last integer of the previous row.

Given an integer target, return true *if* target *is in* matrix *or* false *otherwise*.

You must write a solution in O(log(m * n)) time complexity.

**Example 1:**


**Input:** matrix = [[1,3,5,7],[10,11,16,20],[23,30,34,60]], target = 3

**Output:** true

</aside> */ 
 
 int matrix2[][] = {{1,3,4,7},
                    {10,11,16,20},
                    {23,30,34,60}}; 
int target = 3; 
 
 
 System.out.println(searchMatrix(matrix2, target)); 




       /*<aside>
💡 **Question 3**

Given an array of integers arr, return *true if and only if it is a valid mountain array*.

Recall that arr is a mountain array if and only if:

- arr.length >= 3
- There exists some i with 0 < i < arr.length - 1 such that:
    - arr[0] < arr[1] < ... < arr[i - 1] < arr[i]
    - arr[i] > arr[i + 1] > ... > arr[arr.length - 1]

**Example 1:**

**Input:** arr = [2,1]

**Output:**

false

</aside> */ 


 int nms[] = { 2,1};
 
 System.out.println(checkMountainArray(nms));






       
        /*<aside>
💡 **Question 4**

Given a binary array nums, return *the maximum length of a contiguous subarray with an equal number of* 0 *and* 1.

**Example 1:**

**Input:** nums = [0,1]

**Output:** 2

**Explanation:**

[0, 1] is the longest contiguous subarray with an equal number of 0 and 1.

</aside> */ 
   
       int nums4[] = {0,1}; 

       int res4 = maxSubArray(nums4);
       System.out.println("The lengeth of MaxsubArray when the sum of zeros and ones are equal : " + res4);
  




          /*   <aside>
💡 **Question 5**

The **product sum** of two equal-length arrays a and b is equal to the sum of a[i] * b[i] for all 0 <= i < a.length (**0-indexed**).

- For example, if a = [1,2,3,4] and b = [5,2,3,1], the **product sum** would be 1*5 + 2*2 + 3*3 + 4*1 = 22.

Given two arrays nums1 and nums2 of length n, return *the **minimum product sum** if you are allowed to **rearrange** the **order** of the elements in* nums1.

**Example 1:**

**Input:** nums1 = [5,3,4,2], nums2 = [4,2,2,5]

**Output:** 40

</aside> */  

    int nums5[] = {5,3,4,2}; 
    int nums52[] = {4,2,2,5};

    int res5 = minProduct(nums5, nums52);
    System.out.println(res5);




    
        /*<aside>
💡 **Question 7**

Given a positive integer n, generate an n x n matrix filled with elements from 1 to n2 in spiral order. 
Return a 2D matrix

**Input:** n = 3

**Output:** [[1,2,3],[8,9,4],[7,6,5]]

</aside> */
        int n = 3;
        int[][] matrix = generateMatrix(n);
        for (int[] row : matrix) {
            for (int num : row) {
                System.out.print(num + " ");
            }
            System.out.println();
        }

    
    }


    // Function Defenition for Question 2 

     public static boolean searchMatrix(int[][] matrix, int target) {

     // number of rows - n
     // number of cols - m 

      int n = matrix.length; 
      int m = matrix[0].length; 

      // BaseCase 
      if(m == 0) {
          return false; 
      }

       int low = 0; 
       int high = (m*n)-1; 

       while(low<=high) {
           
           int midIdx = low + (high-low)/2; 
           int rowIdx = midIdx/m; 
           int cols = midIdx%m; 
           int midElement = matrix[rowIdx][cols];

           if(matrix[rowIdx][cols] == target) {
               return true; 
           } else if(matrix[rowIdx][cols] > target) {
               high = midIdx-1;
           } else {
               low = midIdx+1;
           }
       } 
       return false; 
    }


       // Function Defenition for question 3 

         public static boolean checkMountainArray(int nums[]) {

        if(nums.length < 3 ) { return false; } 

         int i = 0; 

         while(i< nums.length-1 && nums[i] < nums[i+1]) {
            i++; 
         } 

         // check if i reached to peak 
         if(i == 0 && i == nums.length-1) {
            return false; 
         } 
        //check the decreasing sequence 

        while(i < nums.length-1 && nums[i] > nums[i+1]) {
            i++;
        } 

        return i == nums.length-1; 

    }



   // Function Defention for Question 4 

    public static int maxSubArray(int nums[] ) {
        
        Map<Integer,Integer> map = new HashMap<>(); 

        int sum = 0; 
        int maxSubArrayLength = 0 ; 

        for(int i = 0; i< nums.length; i++) {

            if(nums[i] == 0) {
                sum -= 1; 
            } else {
                sum += 1; 
            } 

            if( sum == 0 ) {
                maxSubArrayLength = i+1;  
            } else if(!map.containsKey(sum)) {
               // sum is stored as key and index is a value in HashMap
                map.put(sum,i);
            } else {
                // When map contains key 
               int index = map.get(sum); // fectching the index of older when the sum repeated

               int tempLength = i - index; 

               maxSubArrayLength = Math.max(maxSubArrayLength, tempLength);
            } 
        }
            return maxSubArrayLength; 
        }
    


        // Function Defenition for question 5 

        
 public static int  minProduct(int nums1[] , int nums2[]) {

    Arrays.sort(nums1);
   
    int minProductSum = 0; 
    for(int i = 0; i<nums1.length; i++) {
         
         minProductSum += nums1[i] * findLargestRemaining(nums2);
    } 
     return minProductSum; 
 } 

   private static int findLargestRemaining(int nums[]) {
     int largest = Integer.MIN_VALUE;
    int largestIndex = -1; 
    
    for(int i = 0; i<nums.length; i++) {
        if(nums[i] != -1 && nums[i] > largest) {
           largest = nums[i]; 
           largestIndex = i; 
        }
    } 
        nums[largestIndex] = -1; 
        return largest; 
   }
   
// Function Defenition for question 6 

 public static int[][] generateMatrix(int n ) {

        int matrix[][] = new int[n][n];

        int startRow = 0; 
        int endRow = n-1; 
        int startCol = 0; 
        int endCol = n-1;  
        int num = 1; 

        while(startRow<= endRow && startCol <= endCol) {
            // Tansverse Right 

            for(int i = startCol; i<=endCol; i++) {
               matrix[startRow][i] = num; 
               num++; 
            } 
            startRow++; 

            // moveDownWards 

            for(int i = startRow; i<=endRow; i++) {
                matrix[i][endCol] = num++;

            } 
            endCol--;

            // move left in the last row 

            for(int i = endCol; i>=startCol; i--) {
                matrix[endRow][i] = num; 
                num++;
            } 
            endRow--;
            
            // travel left to right to fill the middle rows 

            
                for(int i = endRow; i>=startRow; i--) {
                    matrix[i][startCol] = num;
                    num++;
                } 
                startCol++;
            

        } 
        return matrix; 
    }    






}