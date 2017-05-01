```java
public class Solution {
    //This is very slow
    // public int countPrimes(int n) {
    //     if(n <= 1) return 0;
        
    //     int count = 0;
    //     for(int i = 2; i< n ;i++){
    //         if(isPrime(i)){
    //             count++;
    //         }
    //     }
    //     return count;
    // }
    
    // private boolean isPrime(int n){
    //     //A number is prime if its not divisible by any of the numbers from 2 to n/2
    //     for(int j = 2 ; j <= n/2 ;j ++){
    //         if(n%j == 0)
    //             return false;
    //     }
        
    //     return true;
    // }
    
    
    //Algorithm : http://www.geeksforgeeks.org/sieve-of-eratosthenes/
    //https://en.wikipedia.org/wiki/Sieve_of_Eratosthenes
      public int countPrimes(int n) {
        if(n <= 2) return 0;
        int count = 0;
        boolean[] primes = new boolean[n];
        
        //init everything to true
        for(int i = 2; i< n ;i++){
            primes[i] = true;
        }
        
        for(int i = 2 ; i*i< n; i++){
            //if true then process
            if(primes[i]){
                //for all multiples of i, and we start from i*i because for all i* (i-1) it would have been addressed when processing i-1, eg : 7*2 will be processed when processing 2 itself.
                for(int j = i*i ; j < n ; j+=i){
                    primes[j] = false;
                }
            }
        }
        
        for(int i = 2; i< n ;i++){
            if(primes[i]) count++;
        }
        
        return count;
    }
}
```
