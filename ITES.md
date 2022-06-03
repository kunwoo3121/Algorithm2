# ITES

https://algospot.com/judge/problem/read/ITES

# 구현 방법
Queue를 이용하여 문제를 푼다.
```
 i)   연속된 특정 수열을 구하는 것이기 때문에 수열의 모든 정보를 저장하고 있을 필요는 없다.
 
 ii)  그때그때 값이 들어오면 Queue에 값을 넣고 Queue에 들어 있는 값의 합이 K를 넘어서면 K보다 작아질 때까지 Queue의 값을 빼낸다.
 
 iii) 위의 과정을 끝까지 반복하며 Queue에 들어 있는 값의 합이 딱 K가 되는 횟수를 구한다.
 
```

# 구현 코드
```java
import java.util.Scanner;
import java.util.LinkedList;
import java.util.Queue;
public class ITES {
	static long seed;
	static long limit = ( (long)1 << 32 );
	
	public static void main(String args[])
	{
		Scanner sc = new Scanner(System.in);
		
 		int C = sc.nextInt();
		int A;
		int count;
		int sum;
		int a;
		
		for(int i = 0; i < C; i++)
		{
			int K = sc.nextInt();
			int N = sc.nextInt();
			
			Queue<Integer> list = new LinkedList<Integer>();
			sum = count = 0;
			seed = 1983;
			
			for(int j = 0; j < N; j++)
			{
				A = RNG();
				
				list.add(A);
				
				sum += A;
				
				if(sum > K)
				{		
					while(sum > K)
					{
						a = list.poll();
						sum -= a;
					}
				}
				
				if(sum == K) count++;
			}
			
			System.out.println(count);
		}
		
		sc.close();
	}
	
	public static int RNG ()
	{
		long ret = seed % 10000 + 1;
		
		seed = ( ( seed * 214013 ) + 2531011 ) % limit;
		
		return (int)ret;
	}
}
```
