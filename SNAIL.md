# SNAIL

https://algospot.com/judge/problem/read/SNAIL

# 구현 방법
이차원 배열을 통해 값을 저장해가며 해결한다.
```
 i)   이차원 배열의 i행은 날짜를 나타내고 j열은 올라간 높이를 나타낸다. 즉 i날에 j만큼 올라갈 확률을 저장하는 배열이다.
 
 ii)  이차원 배열의 (i, j)의 값은 (i - 1, j - 1) * 0.25 + (i - 1, j - 2) * 0.75 이다.
      왜냐하면 그 전날에 올라온 j - 1만큼 올라왔을 때 비가 오지 않으면 j 높이에 도달할 것이고 그 전날에 j - 2만큼 올라왔을 때 비가 오면 j 높이에 도달할 것이기 때문이다.
 
 iii) 따라서 우물의 깊이 n 과 장마 기간의 길이 m 이 주어질 때 달팽이가 우물을 탈출할 확률은
      (m, n)부터 (m, m * 2) 까지의 값을 모두 더한 값이 된다. 
      n 만큼의 높이보다 높게 가면 우물을 탈출한 것이기 때문이다. ( m 만큼의 날짜 동안 올라갈 수 있는 최대 높이는 m * 2 이기 때문에 m * 2까지의 값만 구하면 된다.)

```

# 구현 코드
```java
import java.util.Scanner;
public class SNAIL {
	static double[][] climb = new double[1001][2001];
	public static void main(String args[])
	{
		Scanner sc= new Scanner(System.in);
		
		climb[1][1] = 0.25;
		climb[1][2] = 0.75;
		
		for(int i = 2; i < 1001; i++)
		{
			for(int j = i; j < i*2+1; j++)
			{
				climb[i][j] = climb[i-1][j-1] * 0.25 + climb[i-1][j-2] * 0.75;
			}
		}
		
		int c = sc.nextInt();
		
		for(int i = 0; i < c; i++)
		{
			int n, m ;
			double result = 0;
			
			n = sc.nextInt();
			m = sc.nextInt();
			
			if(n <= m) System.out.println(1);
			else 
			{
				for(int j = n; j < m*2+1; j++)
				{
					result += climb[m][j];
				}
				System.out.println(String.format("%.10f", result));
			}
		}
		
		sc.close();
	}

}
```
