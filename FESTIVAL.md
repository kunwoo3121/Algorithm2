# FESTIVAL

https://algospot.com/judge/problem/read/FESTIVAL


# 구현 방법

모든 경우의 수를 구하여 그 중에 최소값을 구하는 방식으로 구현

ex) 6 3    
    1 2 3 1 2 3  과 같은 입력이 들어올 경우
    
    i)   3일을 대여하는 경우 (1 2 3) -> 평균 2 / (2 3 1) -> 평균 2 / (3 1 2) -> 평균 2 / (1 2 3) -> 평균 2
    ii)  4일을 대여하는 경우 (1 2 3 1) -> 평균 1.75 / (2 3 1 2) -> 평균 2 / (3 1 2 3) -> 평균 2.25
    iii) 5일을 대여하는 경우 (1 2 3 1 2) -> 평균 1.8 / (2 3 1 2 3) -> 평균 2.2
    iv)  6일을 대여하는 겨우 (1 2 3 1 2 3) -> 평균 2
    
    => 최소값은 1.75가 된다.
    
위와 같은 방법으로 모든 가능성을 체크하고 그 중 가장 작은 값을 찾아서 문제를 해결하였다.

# 구현 코드
```java
import java.util.Scanner;

public class Festival {
	public static void main(String args[])
	{
		int n;
		Scanner sc = new Scanner(System.in);
		n = sc.nextInt();
		
		for(int i = 0; i < n; i++)
		{
			int day, team;
			int[] cost = new int[1000];
			double hap, min = Double.MAX_VALUE;
			
			day = sc.nextInt();
			team = sc.nextInt();
			
			for(int j = 0; j < day; j++)
			{
				cost[j] = sc.nextInt();
			}
			
			for(int k1 = team; k1 <= day; k1++)
			{
				for(int k2 = 0; k2 <= day - k1; k2++)
				{
					hap = 0;
					for(int k3 = k2; k3 < k2 + k1; k3++)
					{
						hap += cost[k3];
					}
					
					if(min>hap/k1) min = hap/k1;
				}
			}
			
			System.out.format("%.8f%n", min);
		}
		
		sc.close();
	}
}
```
