https://www.careercup.com/question?id=5693819250016256

Given an ODD number, print diamond pattern of stars recursively.


n = 5, Diamond shape is as follows:
  *
 ***
*****
 ***
  *
void print(int n){ 
}

```java

/**
 * Created by arbalan on 5/30/17.
 */
public class diamondShapeStars {

    public static void printStarUtil(int n, int diff, int i){
        if(i == n) diff = -diff;
        if(i<1) return;

        int space = (n-i)/2;
        for(int x = 0 ; x < space; x++) System.out.print(" ");
        for(int x = 0 ; x < i; x++) System.out.print("*");
        for(int x = 0 ; x < space; x++) System.out.print(" ");

        System.out.println("");
        printStarUtil(n, diff, i+diff);
    }
    
    public static void print(int n){
      printStarUtil(n, 2, 1);
    }

    public static void main(String args[]){
        print(5);
    }
}

```
