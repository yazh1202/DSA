
## Precursor for an approach

## Merge 2 sorted Lists

```java
 public ListNode mergeTwoLists(ListNode list1, ListNode list2) {
        ListNode dummy = new ListNode(-1);
        ListNode trav = dummy;
        // Traversing and changing links
        while(list1!=null&&list2!=null){
            if(list1.val<list2.val){
                trav.next = list1;
                trav = trav.next;
                list1 = list1.next;
            }else{
                trav.next = list2;
                trav = trav.next;
                list2 = list2.next;
            }
        }
        // This makes the trav pointer mark to the leftover bit
        // and the leftover bits are already connected so no need 
        // for while loops
        trav.next = (list1==null)?list2:list1;
        return dummy.next;
    }
```
[23. Merge k Sorted Lists](https://leetcode.com/problems/merge-k-sorted-lists/)

You are given an array of `k` linked-lists `lists`, each linked-list is sorted in ascending order.

_Merge all the linked-lists into one sorted linked-list and return it._

**Example 1:**

**Input:** lists = [[1,4,5],[1,3,4],[2,6]]
**Output:** [1,1,2,3,4,4,5,6]
**Explanation:** The linked-lists are:
[
  1->4->5,
  1->3->4,
  2->6
]
merging them into one sorted list:
1->1->2->3->4->4->5->6
## K Sorted Better approach(Space wise)


```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public ListNode mergeKLists(ListNode[] lists) {
       int n = lists.length;
       if(n==0) return null;

       ListNode head = lists[0];
       ListNode temp = head;
       // Just using the mergetwo lists to sort all lists one by one 
       // While appending it each time
        for(int i = 1;i<n;i++){
            head =  mergeTwoLists(head,lists[i]);
        }
        return head;
    }
    public ListNode mergeTwoLists(ListNode list1, ListNode list2) {
        ListNode dummy = new ListNode(-1);
        ListNode trav = dummy;
        // Traversing and changing links
        
        while(list1!=null&&list2!=null){
            
            if(list1.val<list2.val){
                trav.next = list1;
                trav = trav.next;
                list1 = list1.next;
            }else{
                trav.next = list2;
                trav = trav.next;
                list2 = list2.next;
            }
        }
        trav.next = (list1==null)?list2:list1;
        return dummy.next;
    }
}
```

>[!S&C]
>**TIME** - O(N*(N*(N+1)/2)) as appending is occuring 
>**SPACE** -  O(1)


## Optimal Solution using Min Heap

>[!Intuition]
>The main intuition is that we can store the head of each node in a heap to get us the min of all heads and then move it by one for the next node for the head appended.
>


```java
	/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public ListNode mergeKLists(ListNode[] lists) {
        
        int n = lists.length;
        if(n==0) return null;
        // Sorting based on the value for the node
        PriorityQueue<ListNode> pq = new PriorityQueue<>((a,b)->a.val-b.val);

        for(ListNode temp:lists) {
            if(temp!=null) pq.add(temp);
        }
        // Now using dummy
        ListNode dummy = new ListNode(-1);
        ListNode trav = dummy;
        // The priorityqueue will return the min element 
        while(!pq.isEmpty()){
            ListNode nxt = pq.poll();
            trav.next = nxt;
            trav = trav.next;
            if(nxt.next!=null ) pq.add(nxt.next);
        }
        // The dummy.next will point to the head
        return dummy.next;
    }
}
```


>[!Complexity]
>k = numbers of node heads in lists
>n = average length of each node
>TIME - O(k log k + N* k *logk)
>SPACE - O(k)
>






