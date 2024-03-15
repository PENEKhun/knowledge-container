> Longest Common Subsequence

[여기](https://www.youtube.com/watch?v=EAXDUxVYquY) 설명이 진짜 GOAT,,,,

길이가 각각 $i, j$인 문자열 $X_i$와 $Y_j$ 가 있을 때,
$$
X_i = x_1, x_2, x_3 ... x_n
$$
$$
Y_j = y_1, y_2, y_3 ... y_j
$$
$LCS(X_i, Y_j)$를 정의해보자.



아래 처럼, 마지막 문자열이 같은 상황이 있을 수 있다.
$$
X_i = x_1, x_2, x_3 ... p
$$
$$
Y_j = y_1, y_2, y_3 ... p
$$

그런 경우엔 $LCS(X_i, Y_j) = LCS(X_{i-1}, Y_{j-1}) + 1$로 재 정의할 수 있다.


반대로, 마지막 문자열이 다를수도 있다.
$$
X_i = x_1, x_2, x_3 ... p
$$
$$
Y_j = y_1, y_2, y_3 ... k
$$
이런 경우엔 $LCS(X_i, Y_j) = \max (LCS(X_{i-1}, Y_{j}), LCS(X_{i}, Y_{j-1}))$ 로 재 정의할 수 있다.


# 구현

## 재귀 + 메모이제이션
재귀 + Memo 형태로 구현하는게 작성하기 쉽고, 이해하기도 쉽다.

```java
static String[] str;
static int[][] memo;

static int lcs(int i, int j) {
  if (i < 0 || j < 0) {
    return 0;
  }

  if (memo[i][j] != 0) {
    return memo[i][j];
  }

  if (str[0].charAt(i) == str[1].charAt(j)) {
    return memo[i][j] = lcs(i - 1, j - 1) + 1;
  } else {
    return memo[i][j] = Math.max(lcs(i, j - 1), lcs(i - 1, j));
  }
}
```


## 동적 계획법 (DP)

```java
String[] str = new String[2];  
for (int i = 0; i < 2; i++) {  
  str[i] = br.readLine();  
}  
  
int len0 = str[0].length();  
int len1 = str[1].length();  
int[][] dp = new int[len0 + 1][len1 + 1];  
  
for (int i = 1; i <= len0; i++) {  
  for (int k = 1; k <= len1; k++) {  
    if (str[0].charAt(i - 1) == str[1].charAt(k - 1)) {  
      dp[i][k] = dp[i - 1][k - 1] + 1;  
    } else {  
      dp[i][k] = Math.max(dp[i - 1][k], dp[i][k - 1]);  
    }  
  }  
}  
bw.write(dp[len0][len1] + "\n");  
```

