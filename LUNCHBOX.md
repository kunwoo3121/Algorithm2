# LUNCHBOX

https://algospot.com/judge/problem/read/LUNCHBOX

# 구현 방법
```
 1) 먹는 시간이 긴 음식을 먼저 데운다. 그 다음 음식들을 데우는 동안 이 음식을 먹을 것이기 때문이다.
    이것은 최대한 시간을 효율적으로 사용할 수 있게 할 것이다.
    
 2) 먹는 시간이 같을 경우 데우는 시간이 짧은 쪽을 먼저 데운다. 
    이것은 더 적은 시간안에 더 많은 사람이 식사를 시작하게 할 것이다.
    
 ex) 데우는 시간 / 1  5  3  6  과 같은 입력이 들어왔을 경우
       먹는 시간 / 6  2  2 10
       
     위의 두가지 규칙에 따라 정렬을 하게 되면
     
     데우는 시간 / 6  1  3  5 가 되게 된다.
       먹는 시간 /10  6  2  2
       
     정렬된 자료를 순차적으로 따라가며 걸리는 시간을 측정하면 ( 6 + 1 + 3 + 5 + 2 ) = 17분이 걸리게 된다.
     첫 번째, 두 번째, 세 번째 도시락은 뒤의 도시락을 데우는 동안 다 먹게 되고, 네 번째 도시락을 데우고 먹는 시간을 합하면 된다.
```

# 구현 코드
```java
import java.util.Arrays;
import java.util.Scanner;
public class LUNCHBOX {
	
	public static void main(String args[])
	{
		Scanner sc = new Scanner(System.in);
		
		int t = sc.nextInt();
		int n;
		int[][] M_E;
		int eat;
		int time;
				
		for(int i = 0; i < t; i++)
		{
			n = sc.nextInt();
			
			M_E = new int[n][2];
			
			eat = 0;
			
			time = 0;
			
			for(int j = 0; j < n; j++)
			{
				M_E[j][0] = sc.nextInt();
			}
			for(int j = 0; j < n; j++)
			{
				M_E[j][1] = sc.nextInt();
			}
			
			Arrays.sort(M_E, (o1, o2) -> {
				if( o1[1] == o2[1] )
				{
					return Integer.compare(o1[0], o2[0]) * -1;
				}
				else
				{
					return Integer.compare(o1[1], o2[1]);
				}
			});
			
			for(int j = n - 1; j >= 0; j--)
			{
				time += M_E[j][0];
				
				eat -= M_E[j][0];
				
				if(eat < M_E[j][1]) eat = M_E[j][1];
			}
			
			time += eat;
			
			System.out.println(time);
		}
	}

}
```
