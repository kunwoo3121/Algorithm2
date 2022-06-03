# RUNNINGMEDIAN

https://algospot.com/judge/problem/read/RUNNINGMEDIAN

# 구현 방법
```
Max heap과 Min heap을 이용한다.

자료가 들어올 때 홀수 번째 자료이면 Max Heap에 자료를 넣고 짝수 번째이면 Min Heap에 자료를 넣는다.

그 후 만약 Max Heap의 root 값이 Min Heap의 root값보다 클 경우 그 두개의 값을 바꾼다.

이것은 Max Heap에 있는 모든 자료가 항상 Min Heap에 있는 모든 자료보다 작게 하기 위함이다.

이 상태를 유지하면 Max Heap의 root 값이 항상 중간값이 될 수 있다.

Max Heap과 Min heap의 구현은 java에 이미 구현되어 있는 Priority Queue를 이용하였다.
```

## Max Heap / Min Heap
```
Max Heap : 완전 이진 트리에서 부모 노드의 값이 항상 자식 노드의 값보다 큰 구조
Min Heap : 완전 이진 트리에서 부모 노드의 값이 항상 자식 노드의 값보다 작은 구조
```

# 구현 코드
```java
import java.util.Scanner;
import java.util.PriorityQueue;
import java.util.Collections;
public class RUNNINGMEDIAN {
	
	static long seed;
	
	public static void main(String args[])
	{
		Scanner sc = new Scanner(System.in);
		
		int C = sc.nextInt();
		
		for(int i = 0; i < C; i++)
		{
			seed = 1983;
			
			int N = sc.nextInt();
			int a = sc.nextInt();
			int b = sc.nextInt();
			
			PriorityQueue<Integer> minHeap = new PriorityQueue<>();
			PriorityQueue<Integer> maxHeap = new PriorityQueue<>(Collections.reverseOrder());
			
			System.out.println(median(minHeap, maxHeap, N, a, b));
		}
		
		sc.close();
	}
	
	public static int median(PriorityQueue<Integer> minHeap, PriorityQueue<Integer> maxHeap, int N, int a, int b)
	{
		int A = 1983;
		int result = 0;
		
		for(int i = 0; i < N; i++)
		{
			if(minHeap.size() == maxHeap.size())
			{
				maxHeap.add(A);
			}
			else minHeap.add(A);
			
			if(!minHeap.isEmpty() && !maxHeap.isEmpty() && minHeap.peek() < maxHeap.peek())
			{
				int tmp1 = maxHeap.poll();
				int tmp2 = minHeap.poll();
				
				minHeap.add(tmp1);
				maxHeap.add(tmp2);
			}
			
			result = ( result + maxHeap.peek() ) % 20090711;
		
			A = RNG(a,b);
		}
		
		return result;
	}
	
	public static int RNG(int a, int b)
	{
		long tmp = ( seed * a + b );
		
		seed = tmp % 20090711;
		
		return (int)seed;
	}
}
```
