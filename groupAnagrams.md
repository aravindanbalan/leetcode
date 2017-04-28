Idea is that if we sort each string , all anagrams becomes the same string and can be used as a key in hashmap.
We use a hashmap with string as key and value as arraylist to store all same string anagrams.

```java
public class Solution {
    public List<List<String>> groupAnagrams(String[] strs) {
        if(strs == null || strs.length == 0){
            return new ArrayList<>();
        }
        
        Map<String, List<String>> map = new HashMap<String, List<String>>();
        
        Arrays.sort(strs); //looks like we need an output which is sorted
        for(String s : strs){
            char[] c = s.toCharArray();
            //you can also use counting sort or bucket sort to reduce the complexity 
            Arrays.sort(c); //sort all the characters, now same anagrams will become same string.
            String str = String.valueOf(c);
            if(!map.containsKey(str)) map.put(str, new ArrayList<String>());
            map.get(str).add(s); //add the original string to the hash map
        }
        
        return new ArrayList<List<String>>(map.values());
        
    }
}
```
