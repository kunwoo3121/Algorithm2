# WILDCARD

https://algospot.com/judge/problem/read/WILDCARD

# 구현 방법
```
 i)   와일드 카드 문자열 w 의 위치를 나타내는 변수와 비교해야 하는 문자열 s의 위치를 나타내는 변수를 이용하여 각 위치별로 비교하면서 진행한다.
 
 ii)  각 위치에 있는 문자열이 같거나 w의 문자열이 '?' 일 경우에는 각 문자열의 위치를 나타내는 변수를 1 증가시키고 계속 진행한다.
 
 iii) 문제는 문자열 w에 와일드 카드 문자 '*'가 있을 때이다.
 
 iv)  *는 0개 이상의 문자를 포함할 수 있으므로 w의 위치를 나타내는 변수만 증가시켜서 비교를 진행해보고 ( '*'문자에 0개의 문자가 매칭되는 경우 ) 또는 s의 위치를 나타내는 변수만 증가시켜서   
      비교를 진행해보는 과정 ( '*'문자에 1개 이상의 문자가 매칭되는 경우 )을 재귀함수로 구현하여 비교를 진행한다.
      
 v)   w의 위치를 나타내는 변수가 끝까지 진행되었을 때 s의 위치를 나타내는 변수도 끝까지 진행되었다면 true를 리턴, 아니면 false를 리턴한다.
```

# 구현 코드
```java
import java.util.Scanner;
import java.util.Arrays;

public class WILDCARD {
	
	public static void main(String args[])
	{
		Scanner sc = new Scanner(System.in);
	
		int c;
		String w;
		
		c = sc.nextInt();
		
		for(int i = 0 ; i < c; i++)
		{
			boolean ret;
			
			w = sc.next();
			
			int n = sc.nextInt();
			
			String[] result = new String[n];
			
			int r_pos = 0;
			
			for(int j = 0; j < n; j++)
			{
				String s = sc.next();
				
				ret = match(w, s, 0, 0);
				
				if(ret)
				{
					result[r_pos++] = s;
				}
			}
			
			Arrays.sort(result, 0, r_pos);
			
			for(int j = 0; j < r_pos; j++)
			{
				System.out.println(result[j]);
			}
		}
	}
	
	public static boolean match(String w, String s, int w_pos, int s_pos)
	{
		if(w_pos < w.length() && s_pos < s.length() && ( w.charAt(w_pos) == '?' || w.charAt(w_pos) == s.charAt(s_pos) ) )
		{
			return match(w, s, w_pos + 1, s_pos + 1);
		}
		
		if(w_pos == w.length()) return ( s_pos == s.length() ); 
		
		if(w.charAt(w_pos) == '*')
		{
			if(match(w, s, w_pos + 1, s_pos) || ( s_pos < s.length() && match(w, s, w_pos, s_pos + 1) ) ) 
			{
				return true;				
			}
		}
		
		return false;
	}
}
```
