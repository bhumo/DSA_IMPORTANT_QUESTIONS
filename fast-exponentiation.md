# Fast Exponentiation

Find $$2^n$$ of a given number n;

#### Approach 1

&#x20;$$2^n = 2 *2*2 ---- n$$ ​ times

Base Case: the least power of $$2^n$$ is $$2^0$$  which is equal to 1&#x20;

Multiply 2 \* the result of (n-1) th power; to get power of 2^n;

TC: O(n)

```

int exponentiation(int n){
    if(n==0) return 1;
    return 2* exponentiation(n-1);
}
```

#### Approach 2

if n is odd 2^n = 2^n/2 \* 2^n/2 \* 2

if n is even 2^n = 2^n/2 \* 2^n/2;

TC: O(logn) as we are reducing the power by half every time we call the function

```
int fastExponentiation(int n){
    if(n==0) return 1;
    int exponentiation = fastExponentiation(n/2);
    if(n&1){
        // if n is odd  2^n = 2^(n/2) * 2^(n/2) * 2
        exponentiation = exponentiation * exponentiation * 2;
    }else{
        // if n is   2^n = 2^(n/2) * 2^(n/2)
        exponentiation = exponentiation * exponentiation;
    }
    return exponentiation;
}
```
