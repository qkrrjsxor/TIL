
# Sorting 


 Source code of BubbleSort, SelectingSort, InsertingSort

 ref : swea_1966

```java
import java.util.Arrays;
import java.util.Scanner;

public class Solution {
	public static void main(String[] args) {
		Scanner sc = new Scanner(System.in);

		int T = Integer.parseInt(sc.nextLine());

		for (int test = 1; test <= T; test++) {
			int length = sc.nextInt();
			int[] arr = new int[length];

			for (int i = 0; i < length; i++) {
				arr[i] = sc.nextInt();
			}

//			System.out.println("bubbleSort : " + Arrays.toString(bubbleSort(arr)));
//			System.out.println("selectSort : " + Arrays.toString(selectSort(arr)));
//			System.out.println("insertSort : " + Arrays.toString(insertSort(arr)));
			
			arr = selectSort(arr);
			
			System.out.print("#"+test);
			for(int i =0; i< length; i++) {
				System.out.print(" "+arr[i]);
			}
			System.out.println();
		}

	}

	// 버블 정렬
	public static int[] bubbleSort(int[] arr) {
		int len = arr.length;

		for (int i = 0; i < len; i++) {
			for (int t = 1; t < len - i; t++) {
				if (arr[t - 1] > arr[t]) {
					int temp = arr[t - 1];
					arr[t - 1] = arr[t];
					arr[t] = temp;
				}
			}
		}

		return arr;
	}

	// 선택 정렬
	public static int[] selectSort(int[] arr) {
		int len = arr.length;

		for (int i = 0; i < len - 1; i++) {

			int minIdx = i;

			for (int t = i + 1; t < len; t++) {
				if (arr[t] < arr[minIdx]) {
					minIdx = t;
				}
			}
			int temp = arr[i];
			arr[i] = arr[minIdx];
			arr[minIdx] = temp;

		}

		return arr;
	}

	// 삽입 정렬
	public static int[] insertSort(int[] arr) {
		int len = arr.length;

		for (int i = 0; i < len-1; i++) {
			int temp = arr[i+1];
			int t;
			
			for (t = i + 1; t > 0; t--) {
				
				if(temp > arr[t-1]) {	
					break;
				}
				arr[t] = arr[t-1];
			}
			arr[t] = temp;
		}
		return arr;
	}
	
}
```