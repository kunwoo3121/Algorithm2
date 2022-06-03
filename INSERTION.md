# INSERTION

https://algospot.com/judge/problem/read/INSERTION

# 구현 방법
```
Ex) 0 1 1 2 3 이 입력으로 들어오는 경우
 
    가장 뒤에서부터 체크를 시작한다.
    1) 가장 뒤의 값이 3
	     5번째 위치에 있는 수보다 큰 수가 3개 있다는 의미이다.
       따라서 5번째에 위치해야 할 수는 1 2 3 4 5 중에서 2가 된다.

    2) 가장 뒤의 값이 2
       4번째 위치에 있는 수보다 큰 수가 2개 있다는 의미이다.
       따라서 4번째에 위치해야 할 수는 1 3 4 5 중에서 3이 된다.                

    3) 가장 뒤의 값이 1
       3번째 위치에 있는 수보다 큰 수가 1개 있다는 의미이다.
       따라서 3번째에 위치해야 할 수는 1 4 5 중에서 4가 된다.

    4) 가장 뒤의 값이 1
       2번째 위치에 있는 수보다 큰 수가 1개 있다는 의미이다.
       따라서 2번째에 위치해야 할 수 는 1 5 중에서 1이 된다.

    5) 가장 뒤의 값이 0
       1번째 위치에 있는 수보다 큰 수가 0개 있다는 의미이다.
       따라서 1번째에 위치해야 할 수는 5가 된다.
       
위와 같이 구현을 하려면 계속해서 뽑힌 수를 삭제해주어야 한다.

Arraylist의 사이즈를 n이라고 할 때 k번 옮겼다는 정보가 들어오면 (n - k - 1)번째 index에 있는 수를

삭제하며 진행하면 문제를 해결할 수 있다.
```

# 구현 코드
```java
import java.util.Scanner;
import java.util.ArrayList;
public class INSERTION {
	
	public static void main(String args[])
	{
		Scanner sc = new Scanner(System.in);
		
		int C = sc.nextInt();
		
		for(int i = 0; i < C; i++)
		{
			int N = sc.nextInt();
			
			int[] a = new int[N];
			
			int[] result = new int[N];
			
			ArrayList<Integer> arr = new ArrayList<Integer>();
			
			for(int j = 0; j < N; j++)
			{
				a[j] = sc.nextInt();
				arr.add(j + 1);
			}
			
			result = make_arr(arr, a, N);
			
			for(int j = 0; j < N; j++)
			{
				System.out.printf("%d ", result[j]);
			}
			System.out.println();
			
		}
	}
	
	public static int[] make_arr(ArrayList<Integer> arr, int[] a, int N)
	{
		int[] result = new int[N];
		int n;
		
		for(int i = N - 1; i >= 0; i--)
		{
			n = arr.size();
			
			result[i] = arr.get(n - a[i] - 1);
			
			arr.remove(n - a[i] - 1);
		}
		
		return result;
	}

}
```
