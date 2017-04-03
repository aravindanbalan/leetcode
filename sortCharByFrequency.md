Given a string, sort it in decreasing order based on the frequency of characters

Input:
"tree"

Output:
"eert"

```java
public class Solution {
    public String frequencySort(String s) {
        
        //We can use Bucket sorting, which is O(n+k)  here it is O(n+n) = O(n)
        //Or we can use max heap to keep the character count and then poll() each character from heap and print it accordingly
        //O(nlogn)
        Map<Character, Integer> characterCount = new HashMap<Character, Integer>();
        
        //Now we have the character count
        for(char c : s.toCharArray()){
            if(characterCount.containsKey(c)){
                characterCount.put(c, characterCount.get(c) + 1);
            }else{
                characterCount.put(c, 1);
            }
        }
        
        //create buckets
        List<Character>[] bucket = new List[s.length() + 1];

        //iterate through the key set and populate buckets
        for(char key : characterCount.keySet()){
            int frequency = characterCount.get(key);
            if(bucket[frequency] == null){
                bucket[frequency] = new ArrayList<Character>();
            }
            bucket[frequency].add(key);
        }
        
        StringBuilder sb = new StringBuilder();
        
        for(int pos = bucket.length -1 ; pos >=0 ;pos--){
            if(bucket[pos] !=null){
                for(char c: bucket[pos]){
                    for(int i =0;i< characterCount.get(c);i++)
                     sb.append(c);
                }
            }
        }
        
        return sb.toString();
        
    }
}
```
