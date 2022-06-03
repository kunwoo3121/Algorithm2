# TRIANGLEPATH

https://algospot.com/judge/problem/read/TRIANGLEPATH

# 구현 방법

각 행 각 열에서의 최대값을 배열에 저장하여 최대값을 구한다.
```
ex) 6  
    1 2  
    3 7 4
    9 4 1 7
    2 7 5 9 4 의 입력이 들어왔을 경우
    
    바로 아래 또는 오른쪽 아래로만 내려갈 수 있다는 사실을 이용하여 계산을 진행한다.

    i)   0번째 행 계산 -> (0,0) 에서의 최대값은 6이다.
    
    ii)  1번째 행 계산 -> (1,0) 에서의 최대값은 (0,0) 에서 내려온 경우밖에 없으므로 7, 
                         (1,1) 에서의 최대값은 (0,0)에서 내려온 경우와 (0,1)에서 내려온 경우를 비교한다. 최대값은 8
    
    iii) 2번째 행 계산 -> (2,0) 에서의 최대값은 (1,0) 에서 내려온 경우밖에 없으므로 10
                         (2,1) 에서의 최대값은 (1,0) / (1,1)에서 내려온 경우를 비교하면 된다. 최대값은 15
                         (2,2) 에서의 최대값은 (1,1) / (1,2)에서 내려온 경우를 비교하면 된다. 최대값은 12
    
    iv)  3번째 행 계산 -> (3,0) 에서의 최대값은 (2,0) 에서 내려온 경우밖에 없으므로 19
                         (3,1) 에서의 최대값은 (2,0) / (2,1)에서 내려온 경우를 비교하면 된다. 최대값은 19
                         (3,2) 에서의 최대값은 (2,1) / (2,2)에서 내려온 경우를 비교하면 된다. 최대값은 16
                         (3,3) 에서의 최대값은 (2,2) / (2,3)에서 내려온 경우를 비교하면 된다. 최대값은 19
    
    v)   4번째 행 계산 -> (4,0) 에서의 최대값은 (3,0) 에서 내려온 경우밖에 없으므로 21
                         (4,1) 에서의 최대값은 (3,0) / (3,1)에서 내려온 경우를 비교하면 된다. 최대값은 26
                         (4,2) 에서의 최대값은 (3,1) / (3,2)에서 내려온 경우를 비교하면 된다. 최대값은 28
                         (4,3) 에서의 최대값은 (3,2) / (3,3)에서 내려온 경우를 비교하면 된다. 최대값은 24
                         (4,4) 에서의 최대값은 (3,3) / (3,4)에서 내려온 경우를 비교하면 된다. 최대값은 23
   
    => 마지막 행의 값 중 가장 큰 값을 출력하면 된다. 따라서 최대값은 28
```

# 구현 코드
```java
import java.util.Scanner;

public class TRIANGLEPATH {
	
	public static void main(String args[])
	{
		Scanner sc = new Scanner(System.in);
		
		int c;
		int n;
		
		c = sc.nextInt();
		
		for(int i = 0; i < c; i++)
		{
			n = sc.nextInt();
			
			int[] result = new int[n+1];
			int[] in = new int[n];
			int max = 0;
			
			for(int j = 0 ; j < n; j++)
			{
				for(int k = 0; k < j + 1; k++)
				{
					in[k] = sc.nextInt();
				}
				
				for(int k = j; k >= 0; k--)
				{
					if(k == 0) result[k] += in[k];
					else result[k] = Math.max(result[k] + in[k] , result[k-1] + in[k]);
				}
			}
			
			for(int j = 0; j < n + 1; j++)
			{
				max = Math.max(max, result[j]);
			}
			
			System.out.println(max);
		}
		
		sc.close();
	}
}
```