# PASS486

https://algospot.com/judge/problem/read/PASS486

# 구현 방법
```
 i)   최대 1000만까지의 숫자가 들어오므로 1부터 1000만까지 몇 개의 약수를 가지고 있는지 저장하는 배열을 생성한다.
 
 ii)  1부터 1000만까지 반복문을 진행하며 각 숫자의 배수들의 위치에 해당하는 배열의 값을 1씩 증가시켜준다.
      ex) 2의 경우 배열[2], 배열[4], 배열[6], 배열[8]...의 값을 1씩 증가시켜준다.
      
 iii) 위의 반복문의 진행이 끝이 나게 되면 배열에는 각 숫자가 몇 개의 약수를 가지고 있는지 모두 저장하게 된다.

 iv)  이제 lo부터 hi 까지의 숫자중에 n개의 약수를 가진 숫자가 몇 개 있는지 확인하면 된다.
```

# 구현 코드
```java
import java.util.Scanner;
public class PASS486 {

	static int[] divisor = new int[10000001];
	static int C;
	static int n;
	static int lo;
	static int hi;
	static int TM = 10000000;
	static int cnt;
	
	public static void main(String args[])
	{
		Scanner sc = new Scanner(System.in);
		
		C = sc.nextInt();
		
		getFactor();
		
		for(int i = 0; i < C; i++)
		{
			
			cnt = 0;
			
			n = sc.nextInt();
			lo = sc.nextInt();
			hi = sc.nextInt();
			
			for(int j = lo; j <= hi; j++)
			{
				if(divisor[j] == n) cnt++;
			}
			
			System.out.println(cnt);
			
		}
	}
	
	public static void getFactor()
	{
		for(int i = 1; i <= TM; i++)
		{
			for(int j = i; j <= TM; j += i )
			{
				divisor[j]++;
			}
		}
	}
}
```
