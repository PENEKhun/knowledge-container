> 소수란 1보다 큰 자연수 중, 1과 자신만을 약수로 가지는 수이다.

# 알고리즘
### 간단한 것 - O($\sqrt n$)
> 소수를 판별할 때는 2부터 $\sqrt n$ 만큼만 확인하면 된다는 전재하에 생겨난 알고리즘

```java
public boolean isPrime(int n){
	if (n == 1)
		return false;

	for (int i = 2; i <= Math.sqrt(n); i++) {
		if (n % i == 0){
			return false;
		}
	}

	return true;
}
```

### 에라토스테네스의 체 - O($n \log \log n$)
> $2 \sim N$ 까지 , 자신을 제외한 모든 배수를 다 지워버리면 되는 알고리즘

![에라토스테네스의 체](https://upload.wikimedia.org/wikipedia/commons/b/b9/Sieve_of_Eratosthenes_animation.gif)

> **$2 \sim \sqrt N$ 의 배수를 다 지워버려도 된다.**

```java
boolean[] isPrime = new boolean[n + 1];  
Arrays.fill(isPrime, true);  
  
for (int i = 2; i <= Math.sqrt(n); i++) {  
  for (int k = i * 2; k <= n; k += i) {  
    isPrime[k] = false;  
  }  
}
```


![[1644-compare.png]]
> 범위에 따라 시간차이가 꽤 나니깐, 꼭 $2 \sim \sqrt N$을 이용하자.
> 위(324ms)가 $2 \sim \sqrt N$

### 시간 복잡도 비교 그래프

![[0ecc5626-b169-4580-b046-d4957d9b5434.jpg]]

**결론 : 에라토스테네스의 체를 쓰자.**