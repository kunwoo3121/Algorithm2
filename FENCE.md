# FENCE

https://algospot.com/judge/problem/read/FENCE

# 구현 방법
분할 정복으로 문제를 해결한다.
```
 i)   판자를 절반으로 나눠 두 개의 부분 문제를 만든다.
    
    1) 가장 큰 직사각형을 왼쪽 부분 문제에서만 만들 수 있다.
    2) 가장 큰 직사각형을 오른쪽 부분 문제에서만 만들 수 있다.
    3) 가장 큰 직사각형이 왼쪽 부분 문제와 오른쪽 부분 문제에 걸쳐 있다.
 
 ii)  1) 2)는 반으로 나눈 문제를 재귀호출로 해결할 수 있다.
      3)을 해결하는 방법은 아래와 같다.
      
 iii) 일단 3)의 경우 직사각형이 절반으로 나눈 경계에 있는 두 판자를 무조건 포함하고 있다.
      이제 왼쪽, 오른쪽 중 높이가 더 높은 쪽으로 확장해가며 최대 넓이의 직사각형을 구한다.
      
 iv)  위의 과정을 반복하며 답을 구한다.
```

# 구현 코드
```java
import java.util.Scanner;

public class FENCE {

	public static void main(String args[])
	{
		Scanner sc = new Scanner(System.in);
		
		int c; 
		
		c = sc.nextInt();
		
		for(int i = 0; i < c; i++)
		{
			int n, max;
			
			n = sc.nextInt();
			
			int[] fence = new int[n];
			
			for(int j = 0; j < n; j++)
			{
				fence[j] = sc.nextInt();
			}
			
			max = Fence(fence, 0, n-1);
			
			System.out.println(max);
			
		}
	}
	
	public static int Fence(int[] fence, int left, int right)
	{
		int tmp;
		
		if(left == right) return fence[left];
		
		int mid = (left + right) / 2;
		
		tmp = Math.max(Fence(fence, left, mid), Fence(fence, mid + 1, right));
		
		int low = mid, high = mid + 1;
		
		int height = Math.min(fence[low], fence[high]);
		
		tmp = Math.max(tmp, height * 2);
		
		while (left < low || high < right)
		{
			if(high < right && (low == left || fence[low - 1] < fence[high + 1]))
			{
				high++;
				height = Math.min(height, fence[high]);
			}
			
			else
			{
				low--;
				height = Math.min(height, fence[low]);
			}
			
			tmp = Math.max(tmp, height * (high - low +1));
		}
		
		return tmp;
	}
	
}
```
