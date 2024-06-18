
[846. Hand of Straights](https://leetcode.com/problems/hand-of-straights/)

Alice has some number of cards and she wants to rearrange the cards into groups so that each group is of size `groupSize`, and consists of `groupSize` consecutive cards.

Given an integer array `hand` where `hand[i]` is the value written on the `ith` card and an integer `groupSize`, return `true` if she can rearrange the cards, or `false` otherwise.

**Example 1:**

**Input:** hand = [1,2,3,6,2,3,4,7,8], groupSize = 3
**Output:** true
**Explanation:** Alice's hand can be rearranged as [1,2,3],[2,3,4],[6,7,8]

>[!Intuition]
>The consecutive nature needs sorting and the repetition of numbers will require keeping track of frequencies. Thus hashmap and a combination of priorityqueue can be use or treemap can be used.


```java
class Solution {
    public boolean isNStraightHand(int[] hand, int groupSize) {
        
        int n = hand.length;
        // Checking if groups can even be made
        if(n%groupSize!=0) return false;
        
        TreeMap<Integer,Integer> tm  = new TreeMap<Integer,Integer>();
        // Keepint track of frequencies
        for(int i:hand){
            tm.put(i,tm.getOrDefault(i,0)+1);
        }
		// Moving till its all empty
        while(!tm.isEmpty()){
        //Starting from the current lowest element
            int start = tm.firstKey();

            for (int i = start;i<start+groupSize;i++){
                if(!tm.containsKey(i)) {
                    return false;
                }
                tm.put(i,tm.get(i)-1);
                if(tm.get(i)==0) tm.remove(i);
            }
        }
        return true;
    }
}
```

>[!Success]
>Time Complexity:
>O(n)+O(nlogn) for access and iteration
>Space Complexity:
>O(n)

```python
class Solution:
    def isNStraightHand(self, hand: List[int], groupSize: int) -> bool:
        n = len(hand)
        
        if n%groupSize!=0:
            return False

        count = {}
        for num in hand:
            count[num]=count.get(num,0)+1
	    # This creates the heap
        mheap = list(count.keys())
        heapq.heapify(mheap)

        while mheap:
            first = mheap[0]

            for i in range(first,first+groupSize):
                if i not in count:
                    return False
                count[i]-=1
                if count[i]==0:
                    if i!=mheap[0]:
                        return False
                    heapq.heappop(mheap)
        return True
            

        
```








``