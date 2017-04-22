```java
import java.lang.reflect.Array;
import java.util.*;

/**
 * Created by arbalan on 4/21/17.
 */
public class Djikstra {
    class Graph{
        List<GraphNode> vertices;

        Graph(){
            vertices = new ArrayList<GraphNode>();
        }

        public void addVertex(GraphNode node){
            vertices.add(node);
        }
    }

    class GraphNode{
        int label;
        int distance; //distance from src
        List<GraphNode> neighbors;

        GraphNode(int x){
            label = x;
            distance = -1;
            neighbors = new ArrayList<GraphNode>();
        }
    }

    public void shortestPath(Graph graph, GraphNode src, int[][] weight){

        //min heap based on distance from src
        PriorityQueue<GraphNode> minHeap = new PriorityQueue<GraphNode>(graph.vertices.size() ,new Comparator<GraphNode>(){
            @Override
            public int compare(GraphNode o1, GraphNode o2) {
                return ((Integer)o1.distance).compareTo((Integer)o2.distance);
            }
        });

        minHeap.add(src);

        while(!minHeap.isEmpty()){
            GraphNode vertex = minHeap.poll();

            for(GraphNode neighbor: vertex.neighbors){
                int new_distance = vertex.distance + weight[vertex.label][neighbor.label];

                if(neighbor.distance == -1){
                    neighbor.distance = new_distance;
                    minHeap.add(neighbor);
                }

                if(neighbor.distance > new_distance){
                    minHeap.remove(neighbor); //remove existing neighbor node from heap
                    neighbor.distance = new_distance;
                    minHeap.add(neighbor); //add with new distance
                }
            }
        }

    }
}

```
