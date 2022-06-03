# CLOCKSYNC

https://algospot.com/judge/problem/read/CLOCKSYNC

# 구현 방법

스위치를 누르는 모든 경우의 수를 고려하여 시계들이 12시로 맞추어지는 경우가 있는지 체크하고 그 중 가장 적게 누른 경우를 출력한다.  

 
    i)   스위치를 한 번 누를 때마다 3시간씩 바뀌기 때문에 4번 누를 경우 처음 시간으로 돌아간다.   
  
         따라서 스위치를 3번보다 많이 누를 경우 스위치를 누르는 횟수만 늘어나기만 하고 똑같은 경우가 반복이 될 뿐이다.
    
         이를 이용하여 모든 경우를 체크한다.
       
    ii)  각 스위치를 10자리의 4진수의 각 자리수라고 생각을 한다.   
         
         그렇게 되면 0000000000(4) ~ 3333333333(4) 까지 반복을 하며 모든 시계가 12시로 맞춰지는 경우가 있는지 체크를 해보면 된다.
    
    iii) 만약 모든 시계가 12시로 맞추어질 경우 각 자리의 자리수를 더한 것이 버튼을 누른 횟수가 된다.
    
         모든 경우를 체크해보았지만 12시로 맞추어지는 경우가 없을 경우 -1을 출력하면 된다.
         
 # 구현 코드
 ```java
 import java.util.Scanner;

public class CLOCKSYNC {
	
	static int min;
	
	public static void main(String args[])
	{
		Scanner sc = new Scanner(System.in);
		
		int n;
		
		int[][] clk = {{0,1,2},{3,7,9,11},{4,10,14,15},{0,4,5,6,7},{6,7,8,10,12},{0,2,14,15},{3,14,15},{4,5,7,14,15},{1,2,3,4,5},{3,4,5,9,13}};
		
		
		n = sc.nextInt();
		
		for(int i = 0; i < n; i++)
		{
			int[] clock_time = new int[16];
			int[] clock_time_2 = new int[16];
			int[] button_cnt = new int[10];
			int cnt = 0;
			
			for(int j = 0; j < 16; j++)
			{
				clock_time[j] = sc.nextInt();
				clock_time[j] /= 4;
			}
			
			min = 31;
			
			while(true)
			{
				cnt = 0;
				
				for(int j = 0; j < 16; j++)
				{
					clock_time_2[j] = clock_time[j];
				}
				
				for(int j = 0; j < 10; j++)
				{
					cnt += button_cnt[j];
					if(button_cnt[j] == 0) continue;
					for(int k = 0; k < clk[j].length; k++)
					{
						clock_time_2[clk[j][k]] = (clock_time_2[clk[j][k]] + button_cnt[j]) % 4;
					}
				}
				
				int k;
				
				for(k = 0; k < 16; k++)
				{
					if(clock_time_2[k] != 3) break;
				}
				
				if(k == 16)
				{
					if(min > cnt) min = cnt;
				}
				
				if(cnt == 30) break;
				
				button_cnt[9]++;
					
				for(int j = 9; j >= 0; j--)
				{
					if(button_cnt[j] >= 4)
					{
						button_cnt[j-1]++;
						button_cnt[j] %= 4;
					}
					else break;
				}
				
			}

			if(min != 31) System.out.println(min);
			
			else System.out.println("-1");
		}
	}
}
```
