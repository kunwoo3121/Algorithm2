# STRJOIN

https://algospot.com/judge/problem/read/STRJOIN

# 구현 방법
항상 가장 짧은 문자열 두 개를 합쳐서 긴 문자열을 여러 번 합쳐지지 않게 한다.
```
 ex)  5
      3 1 3 4 1 과 같은 입력이 들어온 경우
      
      일단 오름차순으로 정렬한다. -> 1 1 3 3 4
      1) 가장 짧은 문자열은 1과 1 -> 합쳐져서  2가 되고 총 비용 =  2 / 다시 오름차순 정렬 진행 -> 2 3 3 4 
      
      2) 가장 짧은 문자열은 2와 3 -> 합쳐져서  5가 되고 총 비용 =  7 / 다시 오름차순 정렬 진행 -> 3 4 5  
      
      3) 가장 짧은 문자열은 3과 4 -> 합쳐져서  7이 되고 총 비용 = 14 / 다시 오름차순 정렬 진행 -> 5 7
      
      4) 가장 짧은 문자열은 5와 7 -> 합쳐져서 12가 되고 총 비용 = 26 / 문자열이 하나만 남았으므로 종료
```

# 구현 코드
```java
import java.util.Arrays;
import java.util.Scanner;

public class STRJOIN {
	
	public static void main(String args[])
	{
		Scanner sc = new Scanner(System.in);
		
		int c = sc.nextInt();
		
		int n;
		
		int hap;
		
		int len;
		
		int[] StringSet; 
		
		for(int i = 0; i < c; i++)
		{
			hap = 0;
			
			n = sc.nextInt();
			
			StringSet = new int[n];
			
			len = n;
			
			for(int j = 0; j < n; j++)
			{
				StringSet[j] = sc.nextInt();
			}
			
			Arrays.sort(StringSet);
			
			while(len > 1)
			{
				StringSet[0] = StringSet[0] + StringSet[1];
				
				hap += StringSet[0];
				
				for(int j = 1; j < len - 1; j++)
				{
					StringSet[j] = StringSet[j+1];
				}
				
				len--;
				
				Arrays.sort(StringSet,0,len);
			}
			
			System.out.println(hap);
		}
	}

}
```
