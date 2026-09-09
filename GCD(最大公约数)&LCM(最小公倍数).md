
###### 欧几里得算法（Euclidean algorithm）求GCD:
```cpp
int gcd(int a, int b) {
  while (b != 0) {
    int tmp = a;
    a = b;
    b = tmp % b;
  }
  return a;
}
```

###### LCM: 
# $\frac{a * b}{gcd(a, b)}$
