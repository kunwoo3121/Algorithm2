# BOARDCOVER

https://algospot.com/judge/problem/read/BOARDCOVER

# 구현 방법

가능한 모든 경우를 체크하여 가능한 경우의 수를 구한다.

ex) 3 7  
    #.....#  
    #.....#  
    ##..### 가 입력으로 들어오는 경우

    i)  보드판에 놓는 조각을 상대적인 좌표로 나타낸다.  가장 윗줄 왼쪽 칸을 (0,0)으로 두면 
        {(0,0), (1,-1), (1,0)} / {(0,0), (1,0), (1,1)} / {(0,0), (0,1), (1,1)} / {(0,0), (0,1), (1,0)}으로 조각을 표현할 수 있다.
    
    ii) 보드판 배열을 탐색하며 비어 있는 칸을 찾는다. 가장 윗줄, 가장 왼쪽칸부터 탐색. ( 위의 입력 예제에서는 (0,1)의 빈칸이 가장 먼저 찾아질 것이다.)  
        비어 있는 칸을 찾으면 그 빈칸에 조각을 넣을 수 있는지 체크한다. ( 이 빈칸을 (0,0)조각의 위치로 잡음 )
    
    iii) 조각을 넣을 수 있다면 보드판 배열을 채우고 보드판의 빈칸이 모두 없어질 때까지 위의 과정을 반복한다.
    
    재귀함수를 이용하여 위의 과정을 계속 반복하여 모든 경우의 수를 체크한다. ( 재귀함수 return 조건 = 보드판 배열의 빈 칸이 모두 없어진 경우 )

# 구현 코드
```java    
import java.util.Scanner;

public class BOARDCOVER {
	
	static int h,w;
	static int count;
	
	public static void main(String args[])
	{
	
		Scanner sc = new Scanner(System.in);
		
		int n;
		
		n = sc.nextInt();
		
		for(int i = 0; i < n; i++)
		{
			
			int[][] board = new int[20][20];
			int num = 0;
			String s;
			char c;
			
			h = sc.nextInt();
			w = sc.nextInt();
			
			for(int j = 0; j < h; j++)
			{
				s = sc.next();
				for(int k = 0; k < w; k++)
				{
					c = s.charAt(k);
					if(c == '.') 
					{
						board[j][k] = 0;
						num++;
					}
					else board[j][k] = 1;
				}
			}
			count = 0;
			B_cover(board,num);
			System.out.println(count);
		}
	}
	
	public static void B_cover(int[][] board, int num)
	{
		int i = 0, j = 0;
		
		if(num == 0)
		{
			count++;
			return;
		}
		
		for(i = 0; i < h; i++)
		{
			for(j = 0; j < w; j++)
			{
				if(board[i][j] == 0) break;
			}
			if(j != w) break;
		}
				
		if(i+1 < h && j-1 >= 0)
		{
			if(board[i+1][j] == 0 && board[i+1][j-1] == 0)
			{
				board[i][j] = 1;
				board[i+1][j] = 1;
				board[i+1][j-1] = 1;
				B_cover(board, num-3);
				board[i][j] = 0;
				board[i+1][j] = 0;
				board[i+1][j-1] = 0;
			}
		}
		
		if(i+1 < h && j+1 < w)
		{
			if(board[i+1][j] == 0 && board[i+1][j+1] == 0)
			{
				board[i][j] = 1;
				board[i+1][j] = 1;
				board[i+1][j+1] = 1;
				B_cover(board, num-3);
				board[i][j] = 0;
				board[i+1][j] = 0;
				board[i+1][j+1] = 0;
			}
			
			if(board[i][j+1]== 0 && board[i+1][j+1] == 0)
			{
				board[i][j] = 1;
				board[i][j+1] = 1;
				board[i+1][j+1] = 1;
				B_cover(board, num-3);
				board[i][j] = 0;
				board[i][j+1] = 0;
				board[i+1][j+1] = 0;
			}
			
			if(board[i+1][j] == 0 && board[i][j+1] == 0)
			{
				board[i][j] = 1;
				board[i+1][j] = 1;
				board[i][j+1] = 1;
				B_cover(board, num-3);
				board[i][j] = 0;
				board[i+1][j] = 0;
				board[i][j+1] = 0;
			}
		}
	}
}
```    
