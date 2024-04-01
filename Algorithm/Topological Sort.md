# 위상 정렬

### 위상 정렬 이란
**유향 비사이클 그래프**을 선행 순서대로 나열(탐색) 하는 알고리즘
**DAG(Directional Acyclic Graph)**

### 선행노드의 유무 판단
**진입 차수**가 0이면 선행하는 노드가 없다!! 

### 정렬 방법
**Queue를 활용한 정렬 방법**
0. 인접 그래프와, 차수를 저장하기 위한 degree배열 생성
1. 전체 탐색을 하며 진행 차수가 0인 노드를 Queue에 삽입
2. Queue가 빌 때 까지, 다음을 반복 수행
    a. Queue에서 하나의 노드 poll
    b. 해당 노드와 인접한 노드를 탐색하며 진입 차수 감소
    c. 그 인접 노드의 진입 차수가 0이 되면, Queue에 삽입

### Java 코드
**SWEA_1267_작업순서**
```java

import java.util.LinkedList;
import java.util.Queue;
import java.util.Scanner;
import java.util.StringTokenizer;
 
public class Solution {
    public static void main(String[] args) {
 
        Scanner sc = new Scanner(System.in);
        StringTokenizer st;
        StringBuilder sb;
         
        for (int test = 1; test <= 10; test++) {
             
            sb = new StringBuilder();
            sb.append("#"+test);
            st = new StringTokenizer(sc.nextLine());
            int V = Integer.parseInt(st.nextToken());
            int E = Integer.parseInt(st.nextToken());
 
            int[][] adj = new int[V + 1][V + 1];
            int[] degree = new int[V + 1];
 
            st = new StringTokenizer(sc.nextLine());
            int a, b;
            for (int i = 0; i < E; i++) {
                a = Integer.parseInt(st.nextToken());
                b = Integer.parseInt(st.nextToken());
                adj[a][b] = 1;
 
                degree[b]++; // 진입차수 증가
            }
 
            Queue<Integer> queue = new LinkedList<>();
 
            for (int i = 1; i < V + 1; i++) {
                if (degree[i] == 0) {
                    queue.offer(i);
                }
            }
 
            // 위상정렬 시작
            while (!queue.isEmpty()) {
 
                int temp = queue.poll();
                sb.append(" " + temp);
                for (int i = 1; i < V + 1; i++) {
                    if (adj[temp][i] == 1) {
                        degree[i]--;
                        if (degree[i] == 0) {
                            queue.offer(i);
                        }
                    }
                }
            }
 
            System.out.println(sb.toString());
        }
    }
}


```

