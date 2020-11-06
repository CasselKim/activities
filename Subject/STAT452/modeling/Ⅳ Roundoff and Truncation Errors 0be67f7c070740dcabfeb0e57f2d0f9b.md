# Ⅳ. Roundoff and Truncation Errors


# Contents

1. Accuracy
2. Error
3. Roundoff error
4. Truncation error
5. Numerical Differentiation
6. Total Numerical Error

# 1. Accuracy

# 2. Error

# 3. Roundoff Error

표현할 수 있는 범위가 작아서 생기는 오차

# 4. Truncation Error

계산상의 한계로 (continuos 한 공간을 discrete한 공간에서 계산하기때문에) 근사(Approximation)를 할 때 생기는 오차

## 4-1) 미분

![%E2%85%A3%20Roundoff%20and%20Truncation%20Errors%200be67f7c070740dcabfeb0e57f2d0f9b/Untitled.png](%E2%85%A3%20Roundoff%20and%20Truncation%20Errors%200be67f7c070740dcabfeb0e57f2d0f9b/Untitled.png)

## 4-2) 테일러 급수

![%E2%85%A3%20Roundoff%20and%20Truncation%20Errors%200be67f7c070740dcabfeb0e57f2d0f9b/Untitled%201.png](%E2%85%A3%20Roundoff%20and%20Truncation%20Errors%200be67f7c070740dcabfeb0e57f2d0f9b/Untitled%201.png)

# 5. Numerical Differentiation

H가 너무 작아질수록 round off는 증가함 (제대로 표시를 못하니까)

근데 truncation erro는 작아짐

$$f(x_{i+1})=f(x_{i})+f'(x_{i})h+\frac{f''(x_{i})h^{2}}{2!}+\frac{f'''(x_{i})h^{3}}{3!}+\infty$$

$$then\ f'(x_{i})=\frac{f(x_{i+1})-f(x_{i})}{h}-O(h)$$

$\ O(h)=R_{0}=Truncation\ Error$ 입니다. 

뒷 부분은 너무 작으니까 무시하고 계산하는 거죠.  

# 6. Total Numerical Error