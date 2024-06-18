[Video Link](https://www.youtube.com/watch?v=-tgVpUgsQ5k)


```java
    public ArrayList<Integer> bfsOfGraph(int V, ArrayList<ArrayList<Integer>> adj) {
        
        int n = adj.size();
        LinkedList<Integer> ll = new LinkedList<>();
        int[] visited =  new int[n];
        visited[0] = 1;
        ll.add(0);
        
        ArrayList<Integer> ans = new ArrayList<Integer>();
        // Moving levelwise using LinkedList's FIFO capabilities
        
        while(!ll.isEmpty()){
            int curr = ll.removeFirst();
            ans.add(curr);    
            
            if(adj.get(curr).size()==0) continue;
            
            for(int nxt:adj.get(curr)){
                if(visited[nxt]==1) continue;
                visited[nxt] = 1;
                ll.add(nxt);      
                
            }
        }
        
        return ans;
        
        
    }
```