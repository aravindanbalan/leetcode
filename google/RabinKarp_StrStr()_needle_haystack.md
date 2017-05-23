 https://www.youtube.com/watch?v=H4VrKHVG5qI
 https://leetcode.com/problems/implement-strstr/#/description

```java
public class Solution {
    
    //O(M*N) time complexity solution - Very Naive solution
    // public int strStr(String haystack, String needle) {
    //     if(haystack == null || needle == null || needle.length() > haystack.length()) return -1;
        
    //     //implement a sliding window check
    //     for(int i = 0; ; i++){
    //         for(int j = 0; ; j++){
    //             if(j == needle.length()) return i; //first index is i
    //             if(i+j == haystack.length()) return -1; // we reached the end of the haystack string and we dont find a substring
                
    //             if(needle.charAt(j) != haystack.charAt(i+j)) break; //check from next i
    //         }
    //     }
    // }
   
    int prime = 101;
    
     public int strStr(String haystack, String needle) {
        if(haystack == null || needle == null || needle.length() > haystack.length()) return -1;
        
        //Using KMP algorithm  - O(M * N) worst case time and O(1) space
        return RabinKarp(haystack.toCharArray(), needle.toCharArray());
    }
    
    //Worst case complexity is O(M*N) - incase the hashing is bad and returns the same hash for every combination
    //O(1) - to compute hash
    //O(1) space
    private int RabinKarp(char[] text, char[] pattern){
        int m = pattern.length;
        int n = text.length;
        
        long patternHash = createHash(pattern, m);
        long textHash = createHash(text, m);
        
        for(int i = 1; i<= n-m+1 ;i++){
            if(patternHash == textHash && checkEquals(pattern, 0, m-1, text, i-1, i + m-2)){
                return i-1;
            }else{
                //provide the leaving old index (i-1) and entering index (i+m-1) and len = m
                if(i < n-m +1){ //boundary check
                    textHash = generateNewHash(text, textHash, i-1, i+m-1, m);
                }
            }
        }
        
        return -1;
    }
    
    //utility for Rabin Karp
    private long createHash(char[] pattern, int end){
        long hash = 0;
        
        for(int i = 0; i< end ;i++){
            hash+= pattern[i]*Math.pow(prime, i);
        }
        
        return hash;
    }
    
    private long generateNewHash(char[] str, long oldHash, int oldIndex, int newIndex, int len){
        long newHash = oldHash - str[oldIndex];
        newHash /= prime;
        newHash += str[newIndex]*Math.pow(prime, len-1);
        return newHash;
    }
    
    private boolean checkEquals(char[] str1, int start1, int end1, char[] str2, int start2, int end2){
        if(end1 - start1 != end2 - start2) return false;
        
        while(start1 <= end1 && start2 <= end2){
            if(str1[start1] != str2[start2]){
               return false;
            }
            start1++;
            start2++;
        }
        
        return true;
    }
}
```
