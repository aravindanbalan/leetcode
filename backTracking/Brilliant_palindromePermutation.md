Given a string s, return all the palindromic permutations (without duplicates) of it. Return an empty list if no palindromic permutation could be form.

For example:

Given s = "aabb", return ["abba", "baab"].

Given s = "abc", return [].

```
public class Solution {
    List<String> result;
    int[] map;
    public List<String> generatePalindromes(String s) {
        result = new ArrayList<String>();
        if(s == null || s.length() == 0){
            result.add("");
           return result;
        } 
        
        //one character
        if(s.length() == 1){
          result.add(s);
          return result;
        } 
        
        map = new int[256];
        
        //count the number of characters
        for(char c : s.toCharArray()){
            map[c]++;
        }
        
        //check how many odd characters are there, if there more than 1 odd chars then palindrome is not possible
        int oddCharIndex = -1; 
        int count = 0;
        for(int i = 0 ; i< 256 ;i++){
            if(map[i]%2 == 1){
                //odd character
                if(count == 0){
                    count++;
                    oddCharIndex = i;
                }else{
                    //palidromes cant be formed
                    return new ArrayList<String>();
                }
            }
        }
        
        String curr = "";
        
        //Idea is to build around the middle element (add same characters on both sides)
        if(oddCharIndex!=-1){
            //then we have a middle element
            curr += (char)oddCharIndex;
            //reduce map since we already used in the result
            map[oddCharIndex]--;
        }
        
        permuteUtil(curr, s.length(), result);
        return result;
    }
    
    private void permuteUtil(String curr, int len, List<String> result){
        if(curr.length() == len){
            result.add(curr);
        }
        
        for(int i = 0 ; i < 256 ; i++){
            if(map[i]< 1) continue; //there shudnt be any 1s by now
            
            map[i] -= 2; //since we are gonna add two same characters to curr
            curr  = (char)i + curr + (char)i;
            
            permuteUtil(curr, len, result);
            
            curr = curr.substring(1, curr.length()-1);
            map[i] += 2; //backtracking
        }
    }
    
    
    //This will definitely give TLE exception for large strings
    // private void permuteUtil(String s, int l, int r, Set<String> set, List<String> result){
    //     if(l==r){
    //         if(!set.contains(s) && isPalindrome(s)){
    //             set.add(s);
    //             result.add(s);
    //         }
    //         return;
    //     }
        
    //     for(int i = l ;i< r; i++){
    //         s = swap(s, l, i);
    //         permuteUtil(s, l+1, r, set, result);
    //         s = swap(s, l, i);
    //     }
    // }
    
    // private boolean isPalindrome(String s){
    //     char[] str = s.toCharArray();
    //     int left = 0; int right = s.length()-1;
    //     while(left < right){
    //         if(str[left++] != str[right--]) return false;
    //     }
    //     return true;
    // }
    
    // private String swap(String s, int x, int y){
    //     if(s == null) return s;
    //     char[] array = s.toCharArray();
    //     char temp = array[x];
    //     array[x] = array[y];
    //     array[y] = temp;
    //     return new String(array);
    // }
}
```
