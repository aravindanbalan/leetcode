https://www.youtube.com/watch?v=RORuwHiblPc

```java
  
    private static final int INF = -999;
    private List<String> dynamicProgrammingJustify(String[] words, int maxWidth){
        //cost matrix is calculated by the square of number of spaces to fit word i to j 
        
       List<String> lines = new ArrayList<String>();
        if(words.length == 0 || maxWidth == 0){
            lines.add("");
            return lines;
        }
        
        int m = words.length;
        int[][] cost = new int[m][m];
        
        for(int i = 0; i< m ; i++){
            cost[i][i] = maxWidth - words[i].length();
            for(int j = i+1; j< m ;j++){
                //number of spaces required to accomodate words i to j 
                cost[i][j] = cost[i][j-1] - words[j].length() - 1;
            }
        }
        
        for(int i = 0; i< m ; i++){
            for(int j = i; j< m ;j++){
                if(cost[i][j] < 0){
                    cost[i][j] = INF;
                }else{
                    cost[i][j] = (int)Math.pow(cost[i][j], 2); //cost squared
                }
            }
        }
        
        //represents which word starts from current line index (0...m-1)
        int[] result = new int[m];
        //represents min cost of placing words i till end
        int[] minCost = new int[m];
        
        for(int i = m-1; i>=0; i--){
            minCost[i] = cost[i][m-1];
            result[i] = m-1; //last word
            
            for(int j=m-1; j>i; j--){
                if(cost[i][j] == INF) continue;
                
                //min cost of placing j till end + cost of placing i till j-1 is minimum update it.
                if(minCost[i] > minCost[j] + cost[i][j-1]){
                    minCost[i] = minCost[j] + cost[i][j-1];
                    result[i] = j;
                }
            }
        }
        
        //now iterate thru result to find the words
        //minCost[0] will give min cost
        int i = 0;
        int j;
        do{
            j = result[i];
            StringBuilder sb = new StringBuilder();

            for(int k=i; k < j; k++){
                sb.append(words[k] + " ");
            }
            lines.add(sb.toString());
            i = j;
        }while(j < words.length);
        
        return lines;
    }
```
