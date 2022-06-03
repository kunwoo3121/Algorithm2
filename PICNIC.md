# PICNIC

https://algospot.com/judge/problem/read/PICNIC

# 구현 방법

모든 경우의 수를 체크하여 가능한 경우의 수를 구하는 방법으로 구현하였다.

ex) 4 6  
    0 1 1 2 2 3 3 0 0 2 1 3 과 같은 입력이 들어오는 경우
    
    i)   배열을 두 개 생성한다. 배열 1은 이미 짝이 지어진 사람인지 체크하는 배열이고 배열 2는 친구 관계를 나타내는 배열이다.  
    
    ii)  예제와 같은 입력이 들어오면 배열 2는  
    
         X O O O  
         O X O O  
         O O X O  
         O O O X 와 같은 상태가 되고.
         
         배열 1 은  
         X X X X 와 같은 상태가 된다.
     
    iii) 그 후 배열 1의 0번 방부터 체크하며 값이 X일 경우 배열 2의 값을 확인하여 가능한 친구관계를 찾는다.
    
    iv)  친구관계를 하나 선택하면 배열 1의 값을 바꾼다. 예를 들어 0번, 1번을 짝을 지어 준다면 배열 1의 값이 O O X X 로 바뀐다.
    
    v)   이 과정을 반복하며 가능한 짝의 경우의 수를 모두 체크한다.
    
    배열 2를 체크할 때 중복 체크를 방지하기 위해 배열 2를 대각선으로 나누었을 때 오른쪽 상단 부분만 체크한다.

# 구현 코드

```java
import java.util.Scanner;

public class PICNIC {
	
	static int count;
	
	public static void main(String[] args)
	{
		Scanner sc = new Scanner(System.in);
		
		int n;
		
		n = sc.nextInt();
		
		for(int i = 0; i < n; i++)
		{
			int num, pair_num;
			
			num = sc.nextInt();
			pair_num = sc.nextInt();
			
			int[] check = new int[num];
			int[][] matrix = new int[num][num];
			
			for(int j = 0; j < pair_num; j++)
			{
				int a, b;
				
				a = sc.nextInt();
				b = sc.nextInt();
				
				matrix[a][b] = 1;
				matrix[b][a] = 1;
			}
			
			PICNIC.count = 0;
			
			Count_Num(0, num, matrix, check);
			
			System.out.println(PICNIC.count);
		}
		
	}
	
	static void Count_Num(int i, int num, int[][] matrix, int[] check)
	{
		if(i >= num) 
		{
			int k;
			
			for(k = 0; k < num; k++)
			{
				if(check[k] == 0) break;
			}
			
			if(k == num) PICNIC.count++;
			
			return;
		}
		
		if(check[i] == 1) Count_Num(i+1, num, matrix, check);
		
		if(check[i] == 1) return;
		
		check[i] = 1;
		
		for(int j = i+1; j < num; j++)
		{
			if(matrix[i][j] == 1 && check[j] == 0)
			{
				check[j] = 1;
				Count_Num(i+1, num, matrix, check);
				check[j] = 0;
			}
		}
		
		check[i] = 0;
	}
}
```
