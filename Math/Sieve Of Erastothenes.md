[Wiki Link](https://en.wikipedia.org/wiki/Sieve_of_Eratosthenes)

Given an integer `n`, return _the number of prime numbers that are strictly less than_ `n`
## Algorithm
1. Make a list of numbers from 2 to n
2. For each prime number starting with 2 mark their multiples as 'composite' 
3. Move to the next unmarked number
4. Repeat step 2 for each
5. All the unmarked numbers after 4 will be the prime numbers till n
## Optimisations
1. In step 2 it is better to start from the square of the prime number as numbers before it are already marked by smaller prime numbers
2. The algorithm should be halted if the square of the prime number exceeds the number till which prime numbers are to be found as prime factors are always less than square root of the number.


```java
    static int[] SieveOfErastothenes(int n){
        int[] sieve = new int[n+1];
        // Going from 2 to n-1 as less than n is needed 

        for(int j = 2;j<n;j++){
            // Moving j to unmarked position
            while(j<n&&sieve[j]==-1) j++;
            // returning if exceeding square of the number
            if(j*j>n) return sieve;
            // Marking multipes of the prime number
            for(int i = j*j;i<n;i+=j){
                sieve[i] = -1;
            }
        }
        return sieve;
    }
}
```

# Bitwise Sieve
[GFG LINK](https://www.geeksforgeeks.org/bitwise-sieve/)

