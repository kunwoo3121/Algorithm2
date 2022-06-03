# JOSEPHUS

https://algospot.com/judge/problem/read/JOSEPHUS

# 구현 방법
Linked List를 이용한다.
```
 i)   Linked List에 1 ~ N 까지 저장한다.
 
 ii)  처음 0번 방을 제거하고 그 후 K-1 만큼 제거해야 하는 방을 가리키는 index를 증가시킨다. ( K-1 만큼 증가시키는 이유는 제거된 방 이후의 방들의 index가 1씩 줄어들기 때문이다. )
 
 iii) index를 증가시켰을 때 Linked List의 크기보다 index가 커졌을 때 Linked List의 크기로 모듈러 연산을 취한다.
 
 iv)  위의 과정을 Linked List의 크기가 2가 될 때까지 반복한다.
 
  ex) N = 6, K = 3
  
  Num   1 2 3 4 5 6   ->  2 3 4 5 6  ->  2 3 5 6  ->  3 5 6  -> 3 5     => 3, 5 두 개만 남게 되고 이 곳이 살 수 있는 위치이다.
  index 0 1 2 3 4 5       0 1 2 3 4      0 1 2 3      0 1 2     0 1 
  kill index ( 0 )           ( 2 )        ( 0 )       ( 2 )
 ```
 
 # 구현 코드
 ```java
 import java.util.Scanner;
import java.util.LinkedList;
public class JOSEPHUS {
	
	public static void main(String args[])
	{
		Scanner sc = new Scanner(System.in);
		LinkedList<Integer> q = new LinkedList<Integer>();
		
		int C = sc.nextInt();
		for(int i = 0; i < C; i++)
		{
			int N = sc.nextInt();
			int K = sc.nextInt();
			
			q = josephus(N, K);
			
			System.out.printf("%d %d\n", q.get(0),q.get(1));
		}
		
		sc.close();
	}
	
	public static LinkedList<Integer> josephus(int N, int K)
	{
		LinkedList<Integer> q = new LinkedList<Integer>();
		
		for(int i = 1; i <= N ; i++)
			q.add(i);
		
		int kill = 0;
		
		while(q.size() > 2)
		{
			q.remove(kill);
			kill += K-1;
			kill %= q.size();
		}
		
		return q;
	}

}
```
