Given a set of N jobs where each jobi has a deadline and profit associated with it.

Each job takes 1 unit of time to complete and only one job can be scheduled at a time. We earn the profit associated with job if and only if the job is completed by its deadline.

Find the number of jobs done and the maximum profit.

Note: Jobs will be given in the form (Jobid, Deadline, Profit) associated with that Job. Deadline of the job is the time before which job needs to be completed to earn the profit.

[GFG Link](https://www.geeksforgeeks.org/problems/job-sequencing-problem-1587115620/1)

>[!Intuition]
>The main intuition is that we must sort by profit and to make sure that we are doing each job we can we should delay the job as much as possible to do more jobs in the meantime.



```python
class Solution:
    
    #Function to find the maximum profit and the number of jobs done.
    def JobScheduling(self,Jobs,n):
        
        # The greedy way is to maximise the profits by sorting by profits
        # and delaying the job to get more jobs done in the meantime.
        Jobs.sort(key = lambda x:(x.profit),reverse=True)
        
        cd = 0
        count,profit = 0,0
        store = [-1]*(max(job.profit for job in Jobs)+1)
        
        for job in Jobs:
            for i in range((job.deadline),0,-1):
                if store[i]==-1:
                    store[i] = job.profit
                    profit+=job.profit
                    count+=1
                    break
                
                
        return (count,profit)

```