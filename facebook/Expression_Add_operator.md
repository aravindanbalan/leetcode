```
Given a string that contains only digits 0-9 and a target value, return all possibilities to add binary operators (not unary) +, -, or * between the digits so they evaluate to the target value.

Examples: 
"123", 6 -> ["1+2+3", "1*2*3"] 
"232", 8 -> ["2*3+2", "2+3*2"]
"105", 5 -> ["1*0+5","10-5"]
"00", 0 -> ["0+0", "0-0", "0*0"]
"3456237490", 9191 -> []
```

```java
public class Solution {
    public List<String> addOperators(String num, int target) {
        if(num == null || num.length() == 0) return new ArrayList<String>();
        
        List<String> result = new ArrayList<String>();
        addOperatorUtil(num, target, "", result, 0, 0, 0);
        return result;
    }
    
    private void addOperatorUtil(String num, int target, String path, List<String> result, int pos, long eval, long mul){
        if(pos == num.length()){
            if(target == eval){
                result.add(path);
            }
        }
        
        //now recurse from pos
        for(int i = pos ; i< num.length() ; i++){
            
            //for example num = "106" and target 6 and we are in curr = 1 and pos = 1 ----- 1 * 0 + 6 is same as 1 * 6, so no need to eval if char is 0
            if(i!=pos && num.charAt(pos) == '0') break; //no need to proceed
            long curr = Long.parseLong(num.substring(pos, i+1));
            
            //if pos == 0 then it means that in string num = "123" , we are creating recursion branches for 1, 12, 123 etc 
            if(pos == 0){
                addOperatorUtil(num, target, path + curr, result, i+1, curr, curr);
            }else{
                //if not we are in some children inside the recursion stack tree
                addOperatorUtil(num, target, path + "+" + curr, result, i+1, eval + curr, curr);
                                
                addOperatorUtil(num, target, path + "-" + curr, result, i+1, eval - curr, -curr);

                /**
                 * for example, if you have a sequence of 12345 and you have proceeded to 1 + 2 + 3, now your eval is 6 right? If you want to add a * between 3 and 4, you would take 3 as the digit to be multiplied, so you want to take it out from the existing eval. You have 1 + 2 + 3 * 4 and the eval now is (1 + 2 + 3) - 3 + (3 * 4)
                 * */
                 //curr = 4, mul = 3, eval = 6 (1+2+3)
                addOperatorUtil(num, target, path + "*" + curr, result, i+1, eval - mul + mul * curr , mul * curr);
            }
        }
    }
}
````
