**Solution 2: Slow and Fast Pointer Method**

**Approach:**

The following steps are required:

- Initially take two pointers, fast and slow. The fast pointer takes two steps ahead while the slow pointer will take a single step ahead for each iteration.
- We know that if a cycle exists, fast and slow pointers will collide.
- If the cycle does not exist, the fast pointer will move to NULL
- Else, when both slow and fast pointer collides, it [detects a cycle](https://takeuforward.org/data-structure/detect-a-cycle-in-a-linked-list/) exists.
- Take another pointer, say entry. Point to the very first of the linked list.
- Move the slow and the entry pointer ahead by single steps until they collide. 
- Once they collide we get the starting node of the linked list.

But why use another pointer, or xentry?

Let’s say a slow pointer covers the L2 distance from the starting node of the cycle until it collides with a fast pointer. L1 is the distance traveled by the entry pointer to the starting node of the cycle. So, in total, the slow pointer covers the L1+L2 distance. We know that a fast pointer covers some steps more than a slow pointer. Therefore, we can say that a fast pointer will surely cover the L1+L2 distance. Plus, a fast pointer will cover more steps which will accumulate to nC length where cC is the length of the cycle and n is the number of turns. Thus, the fast pointer covers the total length of L1+L2+nC. 

We know that the slow pointer travels twice the fast pointer. So this makes the equation to

2(L1+L2) = L1+L2+nC. This makes the equation to

L1+L2 = nC. Moving L2 to the right side

L1 = nC-L2 and this shows why the entry pointer and the slow pointer would collide.

**Dry Run:**

We initialize fast and slow pointers to the head of the list. Fast moves two steps ahead and slowly takes a single step ahead.

![](https://takeuforward.org/wp-content/uploads/2022/01/image-13.png)

![](https://takeuforward.org/wp-content/uploads/2022/01/image-14.png)

![](https://takeuforward.org/wp-content/uploads/2022/01/image-15.png)

We can see that the fast and slow pointer collides which shows the cycle exists. The entry pointer is pointed to the head of the list. And move them forward until it collides with the slow pointer.

![](https://takeuforward.org/wp-content/uploads/2022/01/image-16.png)

![](https://takeuforward.org/wp-content/uploads/2022/01/image-17.png)

We see that both collide and hence, we get the starting node of the list.
```java
/**
 * Definition for singly-linked list.
 * class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
public class Solution {
    public ListNode detectCycle(ListNode head) {
        if(head==null) return head;
        ListNode fast = head;
        ListNode slow = head;
        // Finding if loop there or not
        while(fast!=null&&fast.next!=null){
            slow = slow.next;
            fast = fast.next.next;
            if(slow==fast){
                ListNode tm = head;
                // Fron the proof we know that
                // the distance between collision 
                // point and the loop start 
                // is equal to the distance between 
                // head and loop start
                while(tm!=slow){
                    tm = tm.next;
                    slow = slow.next;
                }
                return slow;
            }
        }
        return null;
    }   
}**Solution 2: Slow and Fast Pointer Method**

**Approach:**

The following steps are required:

- Initially take two pointers, fast and slow. The fast pointer takes two steps ahead while the slow pointer will take a single step ahead for each iteration.
- We know that if a cycle exists, fast and slow pointers will collide.
- If the cycle does not exist, the fast pointer will move to NULL
- Else, when both slow and fast pointer collides, it [detects a cycle](https://takeuforward.org/data-structure/detect-a-cycle-in-a-linked-list/) exists.
- Take another pointer, say entry. Point to the very first of the linked list.
- Move the slow and the entry pointer ahead by single steps until they collide. 
- Once they collide we get the starting node of the linked list.

But why use another pointer, or xentry?

Let’s say a slow pointer covers the L2 distance from the starting node of the cycle until it collides with a fast pointer. L1 is the distance traveled by the entry pointer to the starting node of the cycle. So, in total, the slow pointer covers the L1+L2 distance. We know that a fast pointer covers some steps more than a slow pointer. Therefore, we can say that a fast pointer will surely cover the L1+L2 distance. Plus, a fast pointer will cover more steps which will accumulate to nC length where cC is the length of the cycle and n is the number of turns. Thus, the fast pointer covers the total length of L1+L2+nC. 

We know that the slow pointer travels twice the fast pointer. So this makes the equation to

2(L1+L2) = L1+L2+nC. This makes the equation to

L1+L2 = nC. Moving L2 to the right side

L1 = nC-L2 and this shows why the entry pointer and the slow pointer would collide.

**Dry Run:**

We initialize fast and slow pointers to the head of the list. Fast moves two steps ahead and slowly takes a single step ahead.

![](https://takeuforward.org/wp-content/uploads/2022/01/image-13.png)

![](https://takeuforward.org/wp-content/uploads/2022/01/image-14.png)

![](https://takeuforward.org/wp-content/uploads/2022/01/image-15.png)

We can see that the fast and slow pointer collides which shows the cycle exists. The entry pointer is pointed to the head of the list. And move them forward until it collides with the slow pointer.

![](https://takeuforward.org/wp-content/uploads/2022/01/image-16.png)

![](https://takeuforward.org/wp-content/uploads/2022/01/image-17.png)

We see that both collide and hence, we get the starting node of the list.
```