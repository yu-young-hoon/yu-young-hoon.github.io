## todo

## 커링과 언커링이란?
![](/docs/attach/currying-uncurrying.png)
- 커링은 Haskell Brooks Curry에서 이름을 따온 수학적 기법입니다
- 커링(currying): 다중인수의 함수를 단일인수의 함수들로 바꾸는 것 f(a,b,c) -> h(a)(b)(c) 
- 언커링(uncurrying): 단일인수의 함수들을 다중인수의 함수로 되돌리는 것 h(a)(b)(c) -> f(a)(b)(c)

## 커링의 장점?
- const squares = [1, 2, 3].map(x => power(2, x));
- const squares = [1, 2, 3].map(powerCurried(2));

## 참고
- https://medium.com/hannah-lin/fp-currying-3de006469b14