```
The API: int read4(char *buf) reads 4 characters at a time from a file.

The return value is the actual number of characters read. For example, it returns 3 if there is only 3 characters left in the file.

By using the read4 API, implement the function int read(char *buf, int n) that reads n characters from the file.

Note:
The read function may be called multiple times
```

```java
/* The read4 API is defined in the parent class Reader4.
      int read4(char[] buf); */

public class Solution extends Reader4 {
    /**
     * @param buf Destination buffer
     * @param n   Maximum number of characters to read
     * @return    The number of characters read
     */
     
    //Since this might be called multiple times, we need global variables to read the data
    int buffPtr = 0;
    int buffCount = 0;
    char[] buff = new char[4];
     
    public int read(char[] buf, int n) {
        int ptr = 0;
        
        while(ptr < n){
            if(buffPtr == 0){
                //then we havent started reading data yet, so read it
                buffCount = read4(buff);
            }
            
            //we do not have anything to read as it might be eof or reached n
            if(buffCount == 0) break;
            
            //whichever reaches first, if buffPtr wasnt zero if any other thread calls it will continue with while loop
            while(ptr < n && buffPtr < buffCount){
                buf[ptr++] = buff[buffPtr++];
            }
            
            if(buffPtr >= buffCount) buffPtr = 0; // reset to read fresh data
        }
        
        return ptr;
    }
}
```
