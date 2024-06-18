[GFG Article Link](https://www.geeksforgeeks.org/convert-min-heap-to-max-heap/)

>[!Intuition]
>The main intuition is to forget that the heap is min heap as it does not help,
>simply use heapify on the array to build the max heap.


```java
public class Solution {
    public static int[] MinToMaxHeap(int n, int[] arr){
    // Starting from last node to the end;
        for(int i = (n/2);i>=0;i--){
            heapifyMax(arr,i,n);
        }
        return arr;
    }
    // Max heap heapify method
    static void heapifyMax(int[] arr,int i,int n){

        int left = 2*i+1;
        int right = 2*i+2;
        int larger = i;
        
        if(left<n&&arr[left]>arr[larger]) larger=left;
        if(right<n&&arr[right]>arr[larger]) larger=right;

        if(i!=larger){
            swap(i,larger,arr);
            heapifyMax(arr,larger,n);
        }
        
    }
    static void swap(int i,int j,int[] arr){
        int temp = arr[i];
        arr[i] = arr[j];
        arr[j] = temp;
    }
}
```