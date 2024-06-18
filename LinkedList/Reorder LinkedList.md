
# Method 1

```python
class Solution:
    def reorderList(self, head: Optional[ListNode]) -> None:
        """
        Do not return anything, modify head in-place instead.
        """

        trav, length = head, 0
        store = []

        while trav:
            store.append(trav)
            length += 1
            trav = trav.next

        i, j = 0, length - 1

        while j > i:
            temp = store[i].next
            store[i].next = store[j]
            store[j].next = temp

            i += 1
            j -= 1
            
        # For odd case i will be equal to j and will be the end
        # For even case i will exceed j and thus become the end
        # Thus for both cases we can point i to None
        store[i].next = None
```

# Method 2 

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def reorderList(self, head: Optional[ListNode]) -> None:

        # Finding Median
        median, fast = head, head
        before = head

        while fast != None and fast.next != None:
            fast = fast.next.next
            median = median.next
        
        # Reversing from the median

        prev,trav = None,median

        while trav!=None:
            temp = trav.next
            trav.next = prev
            prev = trav
            trav = temp
        # prev becomes head of the reversed list
        i,j = head,prev
        
       # This while condition makes sure that the last pointer 
       # will not self reference itself 
       # For odd case the j.next case will work as reversed ll 
       # will be of equal length to not reversed one
       # For even case the j will reach none before i 
       
        while j is not None and j.next is not None :
            t1,t2 = i.next,j.next
            i.next = j
            j.next = t1 

            i,j = t1,t2
```


``