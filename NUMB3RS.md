# NUMB3RS

https://algospot.com/judge/problem/read/NUMB3RS

# 구현 방법
이차원 배열에 값을 저장하며 원하는 값을 얻어낸다.
```
 i)   입력되는 정보를 통해 마을 간의 연결 여부를 이차원 배열을 통해 나타낸다.
 
 ii)  확률을 저장할 이차원 배열을 만든다. 이 이차원 배열에서 i 행의 의미는 i 만큼의 날짜가 지났다는 의미이고 j 열의 의미는 j 마을에 있다는 의미이다.
      따라서 ( i, j )의 값은 i 만큼의 날짜가 지났을 때 j 마을에 두니발 박사가 있을 확률을 의미한다.
 
 iii) 이 이차원 배열 (i, j)의 값은 (i - 1) 행으로부터 구한다.
      (i - 1) 행을 0번 마을부터 n번 마을까지 체크하며 j 마을과 연결되어 있을 경우 
      (i - 1, k) 에 저장되어있는 값에 1 / (k마을과 연결되어있는 마을의 수) 를 곱한 값을 (i, j)에 더해준다. 
      여기서 k는 1 ~ n까지의 값을 가지며 (i - 1) 행의 각 열을 나타내는 수이다.
      
 iv)  위와 같은 방법으로 d일까지의 각 마을에 있을 확률을 계산하면 된다.
```

# 구현 코드
```java
import java.util.Scanner;
public class NUMB3RS {
	
	public static void main(String args[])
	{
		Scanner sc = new Scanner(System.in);
		
		int n,d,p,t;
		
		int c = sc.nextInt();
		
		for(int i = 0; i < c; i++)
		{
			n = sc.nextInt();
			d = sc.nextInt();
			p = sc.nextInt();
			
			int[][] map = new int[n][n];
			
			double[][] cache = new double[d + 1][n];	
			
			int[] total = new int[n];
			
			for(int j = 0; j < n; j++)
			{
				for(int k = 0; k < n; k++)
				{
					map[j][k] = sc.nextInt();
					total[j] += map[j][k];
				}
			}
			
			t = sc.nextInt();
			
			int[] q = new int[t];
			
			for(int j = 0; j < t; j++)
			{
				q[j] = sc.nextInt();
			}
			
			for(int j = 0; j < n; j++)
			{
				if(map[p][j] == 1) cache[1][j] = 1.0/total[p];
			}
			
			for(int j = 2; j < d + 1; j++)
			{
				for(int k = 0; k < n; k++)
				{
					for(int l = 0; l < n; l++)
					{
						if(map[k][l] == 1) cache[j][k] += cache[j-1][l] * (1.0 / total[l]);  
					}
				}
			}
			
			for(int j = 0; j < t; j++)
			{
				System.out.println(String.format("%.8f", cache[d][q[j]]));
			}
		}
		
		sc.close();
		
	}

}
```
