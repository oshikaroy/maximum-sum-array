# maximum-sum-array

PROBLEM STATEMENT:

Implement the solution for Maximum Sum Array by populating the array of size 14 with non-zero [positive/negative] random numbers.
Comment on sum, if first element is positive/negative and last element is positive/negative.

APPROACH:

Divide and Conquer: O(n log n)

Given- Size of the array (N) = 14
```
STEP 1- Divide the array into two parts, from the mid location of the array.
STEP 2- Find the maximum sum from both parts, the right sum from the right subarray and the left sum from the left subarray.
STEP 3- Compare the sums to get the maximum sum of the array.
STEP 4- Also find the maximum sum after the subarray crosses the midpoint.
```
CODE: 

```py
#function to divide array into two parts 
def sumOfarrays(array,low, high,mid):
    sum=0
    leftSum=-10000
    #loop to find max sum in the left array decrementing by 1 towards leftmost from mid
    for i in range(mid, low -1, -1):
        sum+=array[i]
        
        if(sum>leftSum):
            leftSum=sum

    #loop to find max sum of right array, incrementing by 1 from mid+1 to rightmost
    sum=0
    rightSum=-10000
    for j in range(mid+1, high+1):
        sum+=array[j]

        if(rightSum<sum):
            rightSum=sum

    return max(leftSum+rightSum,leftSum, rightSum)

def maxSumSubArray(array,low,high):
    #low is the first index of the array & high is last index of the array
    if(low>high):
        return False

    elif(high==low):
        #condition when the array has only one element, we can return with any index
        return array[high]

    else:
        mid=(low+high)//2 #returns integer
        a=maxSumSubArray(array,low,mid-1) #left sub array
        b=maxSumSubArray(array,mid+1,high) #right sub array
        c=sumOfarrays(array,low,high,mid)
        return max(a,b,c)


#declare the array
arr= [5, 8, -3, 9, 12, -8, 7, 11, -9, 1, -2, 4,-7,6]
maxSum=maxSumSubArray(arr,0,len(arr)-1)
print("Maximum sum of the given array: ", maxSum)
```

TEST CASES:

```
CASE 1- First element & last element are positive.
	Output: 
		Maximum sum of the given array:  41
      
CASE 2- First element & last element are negative.
	Output: 
		Maximum sum of the given array:  36
    
CASE 3- First element is positive & last element is negative.
	Output: 
		Maximum sum of the given array:  41
    
CASE 4- First element is negative & last element is positive.
	Output:
		Maximum sum of the given array:  36
```

CONCLUSION:

We observed through this algorithm that when the first element is positive & last element positive/negative then maximum sum is 41.
Whereas, when the first element is negative & last element is positive/negative the maximum sum is 36.
