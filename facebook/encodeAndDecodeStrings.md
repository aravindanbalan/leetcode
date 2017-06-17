```
Design an algorithm to encode a list of strings to a string. The encoded string is then sent over the network and is decoded back to the original list of strings.
```

```java
public class Codec {

    // Encodes a list of strings to a single string.
    private static final String HASH = "#";
    public String encode(List<String> strs) {
        if(strs.size() == 0) return "";
        StringBuilder sb = new StringBuilder();
        
        for(String str : strs){
            sb.append(str.length()).append(HASH).append(str);
        }
        
        return sb.toString();
    }

    // Decodes a single string to a list of strings.
    public List<String> decode(String s) {
        List<String> result = new ArrayList<String>();
        if(s == null || s.length() == 0) return result;

        int i = 0;
        while(i < s.length()){
            int hash = s.indexOf(HASH, i); //from i
            int len = Integer.valueOf(s.substring(i, hash)); //from i to hash index
            result.add(s.substring(hash+1, hash+len+1));
            i = hash+len+1;
        }
        
        return result;
    }
}

// Your Codec object will be instantiated and called as such:
// Codec codec = new Codec();
// codec.decode(codec.encode(strs));
```
