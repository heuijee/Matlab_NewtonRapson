# Matlab_NewtonRapson
## 1. newton rapson
newton rapson법: 방정식 f(x)=0의 해를 근사적으로 찾을때 유용한 방법

x=a를 넣고 f(a)>0이고 f'(a)>0이면 f(x)의 근은 a보다 작을 것이다라고 추정할 수 있다. 따라서 x=a일때의 접선을 그릴때 접선의 x절편에서 다시 추정하고 반복한다.

### 2. matlab코드 짜기
 함수 선언하기
 
    function [x, ea, it] = NewtonRaphson(f, df, x0, es, maxit)
입력값

f : 함수  
df : f의 미분  
x0 : 초기 추정값  
es : approximate error  
maxit: iterations의 최대값  

결과값 
x : f의 근의 추정값 
it : iterations의 수  
ea : approximate error 값 

if nargin<4, es = 0.01; end
if nargin<5, maxit = 100; end
err0 = Inf; % initialization for the loop
i = 0;
fprintf('i  ,   x_{i},        ea\n');
fprintf('%d  ,   %.6f\n', i, x0);

while err0>es && i<maxit
  if df(x0) 
    x1 = x0-f(x0)/df(x0);
  else 
     error('Diverged! Division by zero!');
  end
   
  err1 = 100*abs((x1-x0)/x1);
  i = i+1;
  fprintf('%d   ,  %.6f,     %.2f%%\n', i, x1, err1);
  err0 = err1;
  x0 = x1;
end

x = x0;
it = i;
ea = err0;


end
