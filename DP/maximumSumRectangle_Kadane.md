```java
 
    class KadaneResult{
        int maxSum;
        int left;
        int right;
        public KadaneResult(int sum, int left, int right){
            this.maxSum = sum;
            this.left = left;
            this.right = right;
        }
    }
    
    private KadaneResult kadane(int[] nums){
        //works for all negative numbers too
        int max = nums[0];
        int max_so_far = nums[0];
        int start = 0, end = 0;
        int tempStart = 0, tempEnd = 0;
        
        for(int i =1 ; i< nums.length ; i++){
            if(nums[i] > max_so_far + nums[i]){
                //update both tempStart and tempEnd
                tempStart = i;
                tempEnd = i;
                max_so_far = nums[i];
            }else{
                max_so_far += nums[i];
                //update tempEnd alone to i
                tempEnd = i;
            }
            
            if(max_so_far > max){
                //if we pick up new max_so_far in result update start and end
                start = tempStart;
                end = tempEnd;
                max = max_so_far;
            }
        }
        
        return new KadaneResult(max, start, end);
    }
    
    private int maxSumRectangle(int[][] matrix){
        if(matrix.length == 0 || matrix[0].length == 0) return 0;
        
        int m = matrix.length;
        int n = matrix[0].length;
        int[] temp = new int[m];
        int max = 0;
        int maxLeft = 0, maxRight = 0, top = 0, bottom = 0;
        
        for(int left = 0; left < n ; left++){
            for(int i=0; i< m;i++){
                temp[i] = 0;
            }
            
            for(int right= left; right < n ; right++){
                for(int i = 0; i< m ;i++){
                    temp[i] += matrix[i][right];
                }
                
                KadaneResult result = kadane(temp);
                if(max < result.maxSum){
                    max = result.maxSum;
                    maxLeft = left;
                    maxRight = right;
                    top = result.left;
                    bottom = result.right;
                }
            }
        }
        
        return max;
    }
```
