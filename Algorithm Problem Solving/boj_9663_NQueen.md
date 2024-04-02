# 문제 정보
난이도: Gold IV
분류 : 백트래킹
url: https://www.acmicpc.net/problem/9663

# 고찰
재귀와 백트래킹을 이용한 대표적 문제

행을 기준으로 모든 열에 대해서 퀸을 놓을 수 있는지 탐색하고,
퀸을 놓은 뒤에 체스판 visited로 퀸의 공격 경로에 대해 +1을 한 뒤,
다음 행으로 옮겨서 다시 열을 탐색하며 visited이면 return 하고,
마지막 행에 도달해서 visited를 만족하면 count + 1 을 하고
return 했을 때 visited를 다시 -1 하여 해당 퀸에 대해 공격 범위를 없애려 하였지만..

이렇게 하니 매번 퀸을 놓을 때 마다 모든 범위에 대해 visit 처리를 해야하므로 시간 초과가 발생했다.

**해결한 방법**은, 퀸을 놓을 때 visit 배열의 공격 경로를 업데이트 하는 것이 아니라, 놓은 퀸을 기준으로 탐색을 하며 해당 퀸의 범위 내에 다른 퀸이 있는지 검사하는것.
왼쪽 위, 수직 위, 오른쪽 위를 탐색하며 퀸이 있는지 검사하고, 퀸이 있으면 return,
퀸이 없으면 visit 배열에 해당 퀸 위치 추가
다음 행에 대해서도 반복을 하다 마지막 행에서 퀸을 놓으면 count +1 을 하여 해결하였다. 


# Java Code
```java
package boj_9663_NQueen;
/*
 * 백트랙킹과 재귀 연습
 * visited 배열을 통해 가능 불가능 판단해보자
 * 
 * 각 행 기준으로 열을 돌아가면서 퀸을 놓고 8방으로 visit 처리 후
 * 다음 행으로 넘어가서 방문 안한 것들
 */

import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

public class Main {

	static int[][] visited; // visited를 처음에 0으로 해놓고 방문하면 +1
	static int N;
	static int[] dr = { -1, -1, -1 };
	static int[] dc = { 0, 1, -1 };
	static int count;

	public static void main(String[] args) throws IOException {
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

		N = Integer.parseInt(br.readLine());

		visited = new int[N][N];

		for (int r = 0; r < N; r++) {
			backtracking(0, r);
		}

		System.out.println(count);
	}

	public static void backtracking(int r, int c) {


		// 같은 열에 퀸이 있으면 리턴
		for (int row = 0; row < r; row++) {
			if (visited[row][c] == 1) {
				return;
			}
		}

		int nr = r;
		int nc = c;
		// 왼쪽 대각선에 퀸이 있으면 리턴
		while (true) {
			nr = nr - 1;
			nc = nc - 1;
			if (nr < 0 || nc < 0) {
				break;
			}
			if (visited[nr][nc] == 1) {
				return;
			}
		}

		
		nr = r;
		nc = c;
		//오른쪽 대각선에 퀸이 있으면 리턴
		while (true) {
			nr = nr - 1;
			nc = nc + 1;
			if (nr < 0 || nc >= N) {
				break;
			}
			if (visited[nr][nc] == 1) {
				return;
			}
		}


		//경로에 퀸이 없고 r이 마지막 행 까지 왔으면 카운트 +1 후 리턴
		if (r == N - 1) {
			count++;
			return;
		}
				
		visited[r][c] = 1;

		for (int i = 0; i < N; i++) {
//			System.out.println("backtracking go" +r + i);
			backtracking(r + 1, i);
		}
		
		visited[r][c] = 0;
	}
}


```