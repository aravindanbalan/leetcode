Implement strStr().

Returns the index of the first occurrence of needle in haystack, or -1 if needle is not part of haystack.


https://www.youtube.com/watch?v=GTJr8OvyEVQ
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
    
     public int strStr(String haystack, String needle) {
        if(haystack == null || needle == null || needle.length() > haystack.length()) return -1;
        
        //Using KMP algorithm  - O(M + N) time and O(N) space
        return KMP(haystack.toCharArray(), needle.toCharArray());
    }
    
    private int KMP(char[] text, char[] pattern){
        int j = 0, i = 0;
        int[] lps = computeLPSArray(pattern);
        
        while(i < text.length && j < pattern.length){
            if(text[i] == pattern[j]){
                i++;
                j++;
            }else{
                if(j!=0){
                    j = lps[j-1]; //move back to index of the pattern which is a suffix and a prefix. This is the optimization KMP does over Naive solution. Naive always goes to 0 and checks from first.
                }else{
                    i++;
                }
            }
        }
        
        if(j == pattern.length){ //then we have our solution
            // now i points to the char next to j+1
            //i - pattern.length will give the first index of j in text
            return i - pattern.length;  // in actual KMP we return true here
        }
        
        return -1; // in actual KMP we return false here
    }

    private int[] computeLPSArray(char[] pattern){
        int j = 0;
        int i = 1;
        int[] lps = new int[pattern.length]; //initially all zeros
        
        while(i < pattern.length){
            /**
             * Two cases 
             * 1. if char at index j and i match 
             * 2. doesnt match
             * */
            if(pattern[j] == pattern[i]){
                
                lps[i] = j+1;
                i++;
                j++;
                
            }else{
                /**
             * Two cases 
             * 1. if j is not zero, then reset j to lps[j-1]
             * 2. if j is zero, then lps[i] = 0 and i++;
             * */ 
                
                if(j!=0){
                    j = lps[j-1];
                }else{
                    lps[i] = 0;
                    i++;
                }
            }
        }
        
        return lps;
    }
}
```
