# POLY

https://algospot.com/judge/problem/read/POLY

# 구현 방법
```
 i)  2차원 배열 하나를 이용하여 값을 저장해간다. 이때 행 i의 의미는 총 i개의 정사각형이 쓰인 세로 단조 폴리오미노를 나타내고 열 j의 의미는 맨 윗줄에 j개의 정사각형이 놓였다는 의미이다.
 
 ii) 이 2차원 배열을 채우는 방법은 다음과 같다. 
     
     (i,j)의 값을 구하는 방법은  (i - j,1) ~ (i - j,i - j)칸에 각각 (j + k - 1)를 곱해서 나온 값을 모두 더하는 것이다. ( k는 열을 나타내는 수 , 범위는 1 ~ (i - j) )
     
     이러한 방법으로 구하는 이유는 가장 윗줄에 j 만큼의 정사각형을 놓으면 놓을 수 있는 남은 정사각형의 수는 ( i- j )개가 된다.
     
     ( i - j ) 개의 정사각형으로 만들 수 있는 세로 단조 폴리노미오의 수는 ( i - j )의 행에 저장되어있고 ( i - j )행의 각 열 k의 값은 두번째 열에 놓인 정사각형의 수와 같으므로
     
     ( j + k - 1 ) 을 곱하면 모든 경우의 수를 체크할 수 있다. ( 위치를 옮기는 경우를 체크해주는 것이다. )
     
 iii) 이 2차원 배열은 아래와 같은 형태로 나오게 된다.
 
      1
      1 1
      3 2 1
      10 5 3 1
      33 16 7 4 1 . . .
      .
      .
      .
 
 iv)  각 행의 모든 값을 더하면 가능한 세로 단조 폴리노미오의 수가 나오게 된다.
      예를 들어 4개의 정사각형을 사용한 모든 세로 단조 폴리노미오의 수는 (10 + 5 + 3 + 1) = 19개가 된다.   
```

# 구현 코드
```java
import java.util.Scanner;
public class POLY {
	static int mdr = 10000000;
	public static void main(String args[])
	{
		Scanner sc = new Scanner(System.in);
		
		int[][] cache = new int[101][101];
		int[] result = new int[101];
		
		
		cache[1][1] = 1;
		result[1] = 1;
		
		for(int i = 2; i < 101; i++)
		{
			for(int j = 1; j <= i; j++)
			{
				if(i == j)
				{
					cache[i][j] = 1;
					result[i] += cache[i][j];
					result[i] %= mdr;
					continue;
				}
				for(int k = 1; k <= i-j; k++)
				{
					cache[i][j] += cache[i - j][k] * (j + k - 1);
					cache[i][j] %= mdr;
				}
				result[i] += cache[i][j];
				result[i] %= mdr;
			}
		}
		
		int c = sc.nextInt();
		
		for(int i = 0; i < c; i++)
		{
			int n = sc.nextInt();
			
			System.out.println(result[n]);
		}
	}

}
```
