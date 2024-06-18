```java

public class Solution {
	
	public static void quickSort(int[] input,int si, int ei) {
		
		if(ei>si){
			System.out.println(si+" " +ei);
			int piv = getPos(input,si,ei);
			quickSort(input,si,piv-1);
			quickSort(input,piv+1,ei);
		}
		
	}
	static int getPos(int[] arr,int low,int high){
			int pivot = arr[low];
			int i = low,j=high;
			int n = arr.length;
			while(i<j){	
				while(i<n&&arr[i]<=pivot) i++;
				// This is important because 
				// if we put j>i then does not go
				// beyond i, which will result in
				// wrong pivot point being reutrned 
				while(j>=i&&arr[j]>pivot) j--;
				if(i<j) swap(arr,i,j);
			}
			swap(arr,j,low);
			show(arr);
			return j;
	}
}
```