Given a n x n matrix where each of the rows and columns are sorted in ascending order, find the kth smallest element in the matrix.

Note that it is the kth smallest element in the sorted order, not the kth distinct element.

Example:

matrix = [
   [ 1,  5,  9],
   [10, 11, 13],
   [12, 13, 15]
],
k = 8,

return 13.


```java
public class Solution {
    
    class MatrixElement implements Comparable<MatrixElement>{
        int row;
        int next;
        int val;
        MatrixElement(int i, int j, int val){
            row = i;
            next = j+1; //store the next pointer
            this.val = val;
        }
        
        @Override
        public int compareTo(MatrixElement ele){
            return ((Integer)(this.val)).compareTo(ele.val);
        }
    }
    
    public int kthSmallest(int[][] matrix, int k) {
        
        if(k == 0) return 0;
        if(matrix.length == 0 || matrix[0].length == 0) return 0;
        
        //Use a min heap to store the elements. Store MatrixElement in heap
        PriorityQueue<MatrixElement> minHeap = new PriorityQueue<MatrixElement>();
        
        int n = matrix.length;
        //insert only first col
        for(int i = 0; i< n ;i++){
            MatrixElement ele = new MatrixElement(i, 0, matrix[i][0]);
            minHeap.add(ele);
        }
        
        //remove k-1 elements to get kth min in peek of Minheap
        for(int i = 0; i< k-1;i++){
            MatrixElement ele = minHeap.poll();
            if(ele.next < n) minHeap.offer(new MatrixElement(ele.row, ele.next, matrix[ele.row][ele.next]));
        }
        
        return minHeap.peek().val;
    }
}
```
