

>[Intuition]
>The main intuition is thinking about two sorted arrays and how you can always be sure that if any element of the left is greater than any element of the right then all other elements of left will also be greater than that 
>This comes from [[Merge Sort]]


```java
public class Solution {
    public static int numberOfInversions(int []a, int n) {

        return mergeSort(a,0,n-1);
        
    }
	// Was using a count variable in the method params but that just
	// Adds multiple function calls return values and gives wrong answer
    static int mergeSort(int[] arr,int i,int j){
        if(j<=i) return 0;
        int mid = (i+j)/2;
        int count = 0;
        // This is done as each function call will return a count
        count+=mergeSort(arr,i,mid);
        count+=mergeSort(arr,mid+1,j);
        count+=merge(arr,i,j,mid);
        return count;
    }

    static int merge(int[] arr,int i,int j,int mid){

        int[] temp = new int[j-i+1];

        int l = i,r = mid+1;

        int ind = 0;
        int cnt = 0;
        while(l<=mid&&r<=j){

            if(arr[l]>arr[r]){
	            // The main change in code
                cnt+=(mid-l+1);
                temp[ind++] = arr[r]; 
                r++;
            }
            else{
                temp[ind++] = arr[l]; 
                l++;
            }
        }

        while(l<=mid){
            temp[ind++] = arr[l++]; 
        }

        
        while(r<=j){
            temp[ind++] = arr[r++]; 
        }

        ind = 0;
        for(int a = i;a<=j;a++){
            arr[a] = temp[ind++];
        }

        return cnt;
        
    }
}
```


```python
class Solution:
    #User function Template for python3
    
    # arr[]: Input Array
    # N : Size of the Array arr[]
    #Function to count inversions in the array.
    def inversionCount(self, arr, n):
        # Copy creation as we don't want to change input data
        temp = list(arr)
        ans  = self.sort([0],temp,0,len(arr)-1)
        return ans[0]

    def sort(self,count,arr,low,high):
        # Merge sort steps
        if low<high:
            mid = (low+high)//2
            self.sort(count,arr,low,mid)
            self.sort(count,arr,mid+1,high)
            # This is used to store the count of inversions
            # single array for persistence during recursions
            count[0]+=self.merge(arr,low,high,mid)
        return count
    
    def merge(self,arr,low,high,mid):
        i,j,k = low,mid+1,0
        temp = [0]*(high-low+1)
        count  = 0
        
        while i<=mid and j<=high:
            if arr[i]<=arr[j]:    
                temp[k] = arr[i]
                k,i = k+1,i+1
            else:
                # The only change where we count inversion when the 
                # number with lower index is greater than numbers with larger index
                # We count for all the numbers with lower indexes (till mid) as both the sides
                # of arrays sorted in themselves
                count+=(mid-i+1)
                temp[k] = arr[j]
                k,j = k+1,j+1
        
        while i<=mid:
            temp[k] = arr[i]
            k,i = k+1,i+1
        
        while j<=high:
            temp[k] = arr[j]
            k,j = k+1,j+1
        
        k = 0
        for ind in range(low,high+1):
            arr[ind] = temp[k]
            k+=1
    
        return count
```