Related: [부분수열](부분수열.md)

**수열 :** {20, 8, 12, 16, 10, 9, 18, 7}

# 감소하는 수열의 예시
- {20, 8, 7}
- {20, 12 ,10, 9, 7}
- {20, 16, 10, 9, 7}
- {20, 10, 9, 7}
- ... 

여기서 길이가 긴 부분 수열을 찾는것이 최대 감소 부분수열 (LDS) 이다.
# LDS 구하기 
- 첫번째 요소 20은 1로 시작한다. $dp[0] = 1$
- 그 다음요소들 부터 수열 값을 매긴다.
	- 다음 요소 8은 20보다 작으므로 $dp[1] = dp[0] + 1 = 2$ 
	- 그 다음 요소 12는 20보다 작지만 8보단 크므로 이전 LDS를 가진다. $dp[2] = dp[1] = 2$
	- 그 다다음 요소 16은 12보다 작으므로 $dp[3] = dp[2] + 1 = 3$
...

![](LSD%20sample.png)
# Java Code Example
```java
import java.io.BufferedReader;  
import java.io.IOException;  
import java.io.InputStreamReader;  
import java.util.Arrays;  
  
/*  
  BAEKJOON 11722 가장 긴 감소하는 부분 수열  
  https://www.acmicpc.net/problem/11722*/  
  
public class Main {  
  
  public static void main(String[] args) throws IOException {  
    BufferedReader br = new BufferedReader(new InputStreamReader(System.in));  
    int n = Integer.parseInt(br.readLine());  
    int[] dp = new int[n];  
    int[] nums = Arrays.stream(br.readLine().split(" ")).mapToInt(Integer::parseInt).toArray();  
  
    dp[0] = 1;  
    for (int i = 1; i < n; i++) {  
      dp[i] = 1;  
      for (int k = 0; k < i; k++) {  
        // 앞 숫자가 큰게 있으면  
        if (nums[i] < nums[k]) {  
          dp[i] = Math.max(dp[i], dp[k] + 1);  
        }  
      }  
    }  
  
    System.out.println(Arrays.stream(dp).max().getAsInt());  
  }  
}
```

- Reference
https://www.youtube.com/watch?v=q_tPIxNNneY