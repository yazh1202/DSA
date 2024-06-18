
Heap is a complete binary tree i.e every node except last level are filled up


It satisfies heaps properties - max or min
Max heap =  Children are always smaller than parent
Min heap =  Children are always greater than parent


Height  =  log n (where n is number of nodes).
Hepa sort

```java
//{ Driver Code Starts

class Solution
{
    //Function to build a Heap from array.
    void buildHeap(int arr[], int n)
    {
        for(int i = n/2;i>=0;i--){
            heapify(arr,n,i);
        }
    }
 
    //Heapify function to maintain heap property.
    void heapify(int arr[], int n, int i)
    {
        // this will be the main heapify method which will
        // creating the heap
        int larger = i;
        int left = 2*i+1;
        int right = 2*i+2;
        if(left<n&&arr[larger]<arr[left]) larger = left;
        
        if(right<n&&arr[larger]<arr[right]) larger = right;
        
        if(i!=larger){
            swap(i,larger,arr);
            heapify(arr,n,larger);
        }
        
    }
    
    static void swap(int i,int j,int[] arr){
        int temp = arr[i];
        arr[i] = arr[j];
        arr[j] = temp;
    }
    //Function to sort an array using Heap Sort.
    public void heapSort(int arr[], int n)
    {
       // This part will just poll and add the largest numbers
       // at the end of array after each call heapify will be called
      buildHeap(arr,n);
      
      for(int i = n-1;i>=0;i--){
      // Must pass i for some reason not i-1
          swap(i,0,arr);
          heapify(arr,i,0);
      }
       
    }
 }
 
 

```


