
>[!Intuition]
>For k sorted array we can always be sure that the smallest element is in the index range of i to i+k and we only need those elements sorted.
>**Time Complexity:** O(K) + O(m * log(k)) ,  where M = N – K  since we only sort 
>**Auxiliary Space:** O(K)
>


```java

class Solution
{
    //Function to return the sorted array.
    ArrayList <Integer> nearlySorted(int arr[], int num, int k)
    {
        PriorityQueue<Integer> pq = new PriorityQueue<>();
        ArrayList<Integer> ans = new ArrayList<>();
        int n = arr.length;
        
        for(int i=0;i<n;i++){
            // This assures us that the sorted array size is always 
            // smaller than k assuring O(n logk) time complexity
            if(i>k) {
                ans.add(pq.poll());
            }
            pq.add(arr[i]);
        }
        while(!pq.isEmpty()) ans.add(pq.poll());
        return ans;
    }
}

```