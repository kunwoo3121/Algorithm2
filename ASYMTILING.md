# ASYMTILING

https://algospot.com/judge/problem/read/ASYMTILING

# 구현 방법
모든 타일링 경우의 수를 구하고 거기서 대칭 타일링의 경우를 빼서 비대칭 타일링 경우의 수를 구한다.
```
 i)   일단 모든 타일링 경우의 수를 구한다. 2 * n의 크기를 채우는 방법은 2 * (n - 1)을 채운 방법에서 ㅣ모양 타일을 놓은 경우 또는 
      2 * (n - 2)를 채운 방법에서 ㅡ모양 타일을 두 개 놓은 경우이다. 따라서 그 두 개의 경우의 수를 더하면 2 * n 의 크기를 채우는 경우의 수를 구할 수 있다.
    
 ii)  이제 여기서 대칭 타일링의 경우의 수를 뺀다. 대칭 타일링이 되는 경우는  
      1) n이 홀수일때는 중간 부분이 ㅣ모양 타일이 놓여 있고 이것을 경계로 양쪽 타일링이 대칭인 경우와
      2) n이 짝수일때는 중간을 경계로 양쪽 타일링이 대칭인 경우와 중간에 = 모양으로 타일이 놓여 있고 이것을 경계로 양쪽 타일링이 대칭인 경우이다.
 
 iii) ii)에서 1)의 경우의 수는 2 * (( n - 1 ) / 2)의 경우의 수와 같다. 2 * (( n - 1 ) / 2) 의 상태에서 ㅣ 타일을 놓고 반대쪽이 대칭되게 놓인 경우이기 때문이다.
      ii)에서 2)의 경우의 수는 2 * (n / 2)의 경우의 수와 2 * (n/2 - 1)의 경우의 수를 합한 것과 같다. 이유는 위에 적힌 것과 같다.
      
 iv)  i)에서 구한 경우의 수에서 iii)에서 구한 경우의 수를 빼주면 비대칭 타일링 경우의 수만 남게 된다.
```

# 구현 코드
```java
import java.util.Scanner;

public class ASYMTILING {
	
	public static void main(String args[])
	{
		Scanner sc = new Scanner(System.in);
		long[] a = new long[101];
		long modular = 1000000007;
		
		a[1] = 1;
		a[2] = 2;
		
		for(int i= 3; i <= 100; i++)
		{
			a[i] = ( a[i-1]   + a[i-2] ) % modular;
		}
		
		int c, n;
		
		c = sc.nextInt();
		
		for(int i = 0; i < c; i++)
		{
			n = sc.nextInt();
			
			long result;
			
			if(n == 2) result = 0; 
			else if(n % 2 == 1) result = ( a[n] - a[n/2] + modular ) % modular;
			else
			{
				result = a[n];
				result = ( result - a[n/2] + modular ) % modular;
				result = ( result - a[n/2-1] + modular ) % modular;
			}
			
			System.out.println(result);
		}	
	}
}
```
