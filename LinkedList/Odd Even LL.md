[328. Odd Even Linked List](https://leetcode.com/problems/odd-even-linked-list/)

Given the `head` of a singly linked list, group all the nodes with odd indices together followed by the nodes with even indices, and return _the reordered list_.

The **first** node is considered **odd**, and the **second** node is **even**, and so on.

Note that the relative order inside both the even and odd groups should remain as it was in the input.

You must solve the problem in `O(1)` extra space complexity and `O(n)` time complexity.

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/03/10/oddeven-linked-list.jpg)

**Input:** head = [1,2,3,4,5]
**Output:** [1,3,5,2,4]


- Bruteforce will be to store all values at odd and even and then assign them to each

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
    public ListNode oddEvenList(ListNode head) {
        
    if(head==null||head.next==null||head.next.next==null) return head;

    ListNode oh = head;
    ListNode eh = head.next;
    ListNode temp = eh;
    // Checking for only the even pointer 
    // as it is always ahead of odd pointer
        while(eh!=null&&eh.next!=null){
            // Pointing next for each
            oh.next = oh.next.next;
            eh.next = eh.next.next;

            // Going to next 
            oh = oh.next;
            eh = eh.next;
            
        }
        oh.next = temp;
        return head; 
    }
}

```