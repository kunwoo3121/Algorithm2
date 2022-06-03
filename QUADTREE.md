# QUADTREE

https://algospot.com/judge/problem/read/QUADTREE

# 구현 방법

그림을 상하로 뒤집을 경우 항상 제 1사분면과 제 3사분면의 위치가 바뀌고 제 2사분면과 제 4사분면의 위치가 바뀐다는 것을 알면 재귀함수를 통해 간단하게 구현할 수 있다.
```  
  ex1) xbwxwbbwb 가 입력으로 들어오는 경우
  
  제 1사분면은 b, 제 2사분면은 w  
  
  제 3사분면은 다시 4개의 사분면으로 나누어지고 제 1사분면은 w, 제 2사분면은 b, 제 3사분면은 b, 제 4사분면은 w 이므로 상하로 뒤집을 경우 xbwwb 가 된다.  
  
  그리고 마지막으로 제 4사분면은 b 이므로 상하로 뒤집을 경우 xxbwwbbbw 가 된다.
  
  ex2) xxwwwbxwxwbbbwwxxxwwbbbwwwwbb 가 입력으로 들어오는 경우
  
  제 1사분면 -> 제 1사분면 = w, 제 2사분면 = w, 제 3사분면 = w, 제 4사분면 = b 따라서 상하로 뒤집으면 xwbww가 된다.  
  제 2사분면 -> 제 1사분면 = w, 제 2사분면 -> 제 1사분면 = w, 제 2사분면 = b, 제 3사분면 = b, 제 4사분면 = b => xbbwb    
               제 3사분면 = w, 제 4사분면 = w => xwwwxbbwb
  제 3사분면 -> 제 1사분면 -> 제 1사분면 -> 제 1사분면= w, 제 2사분면 = w, 제 3사분면 = b, 제 4사분면 = b => xbbww, 제 2사분면 = b, 제 3사분면 = w, 제 4사분면 = w =>  xwwxbbwwb
               제 2사분면 = w, 제 3사분면 = w, 제 4사분면 = b => xwbxwwxbbwwbw
  제 4사분면 -> b
  
  => xxwbxwwxbbwwbwbxwbwwxwwwxbbwb 가 된다.
```  

# 구현 코드
```java
import java.util.Scanner;

public class QUADTREE {
	static int iter;

	public static void main(String args[])
	{
		Scanner sc = new Scanner(System.in);
		int n;
		
		n = sc.nextInt();
		
		int i;
		
		for(i = 0; i < n; i++)
		{
			String s, result;
			
			s = sc.next();
			
			iter = -1;
			
			result = reverse_Q_tree(s);
			
			System.out.println(result);
		}
		
	}
	
	public static String reverse_Q_tree(String s)
	{
		String s1, s2, s3, s4;
		
		iter++;
		
		if(s.charAt(iter) == 'b')
		{
			return "b";
		}
		
		else if(s.charAt(iter) == 'w')
		{
			return "w";
		}
		
		else
		{
			s1 = reverse_Q_tree(s);
			s2 = reverse_Q_tree(s);
			s3 = reverse_Q_tree(s);
			s4 =reverse_Q_tree(s);
		}
		
		return "x"+s3+s4+s1+s2;
	}
}
```
