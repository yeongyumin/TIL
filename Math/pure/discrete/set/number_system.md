# 수의 체계

- 참고
- 의문
- 개요
- 자연수
  - 자연수
  - 자연수의 연산
  - 자연수의 순서관계
- 정수와 유리수

## 참고

- 집합과 수의 체계 - 계승혁

## 의문

- *연산이 제대로 정의되어있다는 것이 무슨 의미인가?*

## 개요

- 자연수집합 생성
  - 자연수를 정의
  - 자연수의 연산 정의
  - 각종 법칙 증명
    - 교환 / 결합 / 분배
  - 임의의 자연수집합이 최솟값을 갖는것을 증명
- 정수집합 생성
  - 자연수의 순서쌍에 적절한 동치관계 부여해서 정수집합을 생성
- 유리수 집합생성
  - 정수의 집합에 입각해서 유리수집합 생성
- 실수 집합 생성
  - 데데킨트 절단
  - 코시 수열
- 임의의 완비 순서체는 항상 같음 증명

## 1. 자연수

### 자연수

자연수(0을 포함하지 않는)는 대수구조 상 반환(semiring)에 속함. 덧셈에 대한 가환 모노이드, 곱셈에 대한 모노이드, 분배 법칙이 성립

- 자연수 구성에 필요한 것들
  - 집합 A에 대한 새 집합A+
    - `A+ = A U {A}`
  - `0 = φ`
- 자연수
  - 정의
    - 페아노 공리계를 따르는 집합과 연산구조
      - 페아노 대수(Peano arithmetic)의 '약한' 조건으로 자연수를 구성할 경우, 자연수 구조는 더 이상 유일하지 않고, 여러가지 논스탠다드 모델이 등장한다. 게중에는 실수처럼 셀 수 없는 자연수 모델도 있다. >> 페아노 공리계만 만족하면 되므로
    - 다음 두 가지 성질을 가지는 집합 A들 전체의 교집합을 N으로 쓰고(왜 전체의 교집합일까? - e.g `A = {0, 1, ..., K} 원소 K는 K+ = K 가 되도록, +와 0을 정의`하면 이것은 0, 1, ... 이외의 특수한 원소가 들어가기 때문), 이 집합의 원소들을 자연수라 함
      - `φ∈F`
      - `A∈F => A+∈F`
  - 성질(페아노 공리계)
    - ① `0 ∈ N`
      - 0은 무정의 용어
    - ② `n ∈ N => n+ ∈ N`
    - ③ `∀n∈N, n+ ≠ 0`
      - **폰노이만의 자연수 구성을 취할 경우(`0 = φ, n+ = n U {n}`)** 자명
    - ④ `X ⊆ N, (0∈X ∧ n∈X => n+∈X) => X = N`
      - 귀납적 공리
      - 수학적 귀납법을 사용할 수 있는 근거
        - 자연수 `n∈N`에 관한 명제 `P(n)`이 있을 때, `P(n)`이 성립하는 자연수 `n∈N`들의 집합을 X라 두자.
        - `(P(0)≡t ∧ P(n) => P(n+1)) => X = N`
          - 왜냐하면 집합 X가 페아노 공리계의 ④ 성질을 만족하기 때문
    - ⑤ `m,n∈N, m+=n+ => m=n`
    - **공리계로 성질을 정해놓고 이 성질을 만족하면 자연수집합이라고 부를 수 있게 한 것?? >> 그렇다**
      - 자연수를 구성하기 위해 필요한 것
        - 0이 무엇인지 정의
        - n+가 무엇인지 정의
      - 자연수 구성 예시
        - 체르멜로: `0 = φ, n+(= n+1) = {n}`
        - 폰 노이만: `0 = φ, n+ = n U {n}`
        - 이걸 보면 마틴오더스키 선생님의 Functional Programming In Scala에서 자연수를 클래스로서 구성했던것이 생각남

### 자연수의 연산

> <참고> 자연수에서의 연산법칙을 비롯한 다양한 내용의 증명은 페아노공리계의 수학적귀납원리를 이용해서 증명하는 경우가 많다.

- 집합 X의 한 원소 `a∈X`과 함수 `f: X -> X`에 대하여, 다음성질을 만족하는 함수 `r : N -> X`가 유일하게 존재한다.(집합 X의 원소 r(0), r(1), ... 가 특정 점화식을 만족하도록 귀납적으로 정의할 수 있음을 보여줌)
  - `r(0) = a`
  - `∀n∈N, r(n+) = f(r(n))`

#### 더하기와 곱하기의 정의

더하기 곱하기 지수승을 recursive한 함수를 정의해서 정의함(recursion theorem)

- 더하기
  - 정의
    - 위의 정리를 적용하면, 각 자연수 `m∈N`에 대하여 다음을 만족하는 함수 `rm: N -> N`이 유일하게 존재함
      - `rm(0) = m, n∈N => rm(n+) = [rm(n)]+`
    - `m+n = rm(n), m,n∈N`
  - 자연수 집합에서 성립하는 연산법칙
    - `n+0 = 0+n = n`
    - `(m+n)+k = m+(n+k)`
    - `m+n = n+m`
- 곱하기
  - 정의
    - 마찬가지로 위의 정리를 적용하여 유일한 δ함수를 정의
      - `δm : N -> N, δm(0) = 0, n∈N => δm(n+) = δm(n)+m`
    - `m,n∈N, mn = δm(n)`
  - 자연수 집합에서 성립하는 연산법칙
    - `n0 = 0n = 0`
    - `n1 = 1n = n`
    - `(mn)k = m(nk)`
    - `mn = nm`
- 더하기와 곱하기의 분배법칙
  - `m(n+k) = mn+mk`
  - `(n+k)m = nm+km`
- 지수 연산
  - `m^(n+k) = m^n m^k`
  - `(mn)^k = m^k n^k`
  - `(m^n)^k = m^(nk)`

---

참고

a,b,c의 곱셈 `abc`라고 표현이 가능한 이유는 `(ab)c = a(bc)`가 성립하기 때문

### 자연수의 순서관계

순서관계를 정의하는 것 부터

- 순서관계 정의
  - `m,n∈N, m<=n <=> m∈n ∨ m=n`
    - 이것이 동치관계임을 증명
  - `m,n∈N, m<=n ∧ m≠n <=> m∈n`
    - `∵ ∀n∈N, n!∈n`
      - 잘 이해가 안됨
- 정리
  - 공집합이 아닌 자연수의 집합에는 최소 원소가 있음
    - 비어 있지 않은 자연수들의 집합은 최소 원소를 가짐
      - 임의의 두 자연수 `m,n∈N`에 대하여 `m<=n`혹은 `n<=m`이 성립한다.
  - 공집합이 아닌 자연수의 집합에는 최대 원소가 있음
    - 위로 유계이며 비어 있지 않은 자연수들의 집합 `A⊆N`는 최대 원소를 가짐
  - 자연수는 큰 수에서 작은수로 뺄셈이 가능
    - `m,n∈N, n>=m <=> ∃k∈N, n=m+k ∧ (m+k=m+l => k=l)`
    - `m+k <= m+l <=> k<=l`
    - `mk <= ml <=> k<=l (단, m≠0)`
  - 자연수의 나머지 정리
    - `m,l∈N, 0<m<=l, ∃n,r∈N, l = mn+r, (0<=r<m) ∧ (mn+r = mk+s => n=k ∧ r=s)`

## 2. 정수와 유리수

### 정수

- 정수
  - 접근
    - `m,n∈N, n<=m => m=n+k인 k가 유일하게 존재`
      - 그러한 `k`를 `m-n`으로 씀
    - `m<n`인 경우에도 `m-n`이 뜻을 가지게끔 수의 범위를 넓히자
      - `m-n = (m,n)`
    - `N x N = {(m,n) | m,n∈N}`
      - `m>=n`제한 없앰
      - 관계정의
        - `(m,n) ~ (m',n') <=> m+n' = n+m'`
          - `~`는 동치관계
          - `m>k,n>=k => (m,n) ~ (m-k, n-k)`
  - 정의
    - `Z = N x N/~`
      - Z의 원소를 정수라 부름
      - `Z = {[n,0], [0,0], [0,n] | n∈N}`
        - `[1,0]`은 정수 1
        - `[0,5]`는 정수 -5에 대응(왜냐면 (0,5) = 0-5)
  - 관계정의
    - `[m,n] >= [k,l] <=> m+l >= n+k`
      - `>=`는 순서관계
    - 관계에 관한 정리
      - `비어있지 않은 Z의 부분집합 A가 위로 유계 => A는 최대원소 가짐`
      - `비어있지 않은 Z의 부분집합 A가 아래로 유계 => A는 최소원소 가짐`
- 정수의 연산
  - 덧셈
    - `[m,n]+[k,l] = [m+k,n+l]`
    - 결합법칙, 항등원, 역원, 교환법칙 존재 / 성립
  - 곱셈
    - `[m,n]・[k,l] = [mk+nl,ml+nk]`
    - 결합법칙, 항등원, 교환법칙 존재 / 성립
- 정수의 표기
  - `f: N -> Z, f(n) = [n,0]`
    - f는 단사함수
    - `m,n∈N`
      - `f(m+n) = f(n)+f(m)`
      - `f(mn) = f(n)f(m)`
      - `m>=n <=> f(m) >= f(n)`
  - f가 성립하므로, `[n,0], [0,0], [0,n]`표기 대신 `n, 0, -n`으로 쓸 수 있음

### 유리수

- 체
  - 정의
    - 더하기 연산법칙
      - ① `∀a,b,c∈F, a+(b+c) = (a+b)+c`
      - ② `∃e∈F, ∀a∈F, a+e = e+a = a ∧ (a+e' = e'a = a => e' = e)`
        - 이를 0이라고 하고, 더하기의 항등원이라 함
      - ③ `∀a∈F, ∃x∈F, a+x = x+a = 0 ∧ (a+x' = x'+a = 0 => x' = x)`
        - `x = -a`라 쓰고, a의 역원이라고 함
      - ④ `∀a,b∈F, a+b = b+a`
    - 곱하기 연산법칙
      - ⑤ `∀a,b,c∈F, a(bc) = (ab)c`
      - ⑥ `∃1∈F, ∀a∈F, a・1 = 1・a = a ∧ (a・1' = 1'・a = a => 1' = 1) ∧ 1 ≠ 0`
      - ⑦ `∀a∈F \ {0}, ∃x∈F, ax = xa = 1`
        - `a^-1` 혹은 `1/a`이라 쓰고 곱하기에 관한 a의 역원이라 함
      - ⑧ `∀a,b∈F, ab = ba`
    - 더하기 연산과 곱하기 연산의 관계
      - ⑨ `∀a,b,c∈F, a(b+c) = ab+ac`
- 순서체(체 위의 순서 도입)
  - 양수 개념 도입
    - `S∈F, -S = {-a | a∈S}`
  - 정의
    - `∃P∈F, P≠φ`
      - ① `a,b∈P => a+b, ab∈P`
      - ② `F = P U {0} U (-P)`
      - ③ `P∩{0} = φ ∧ P∩-P = φ ∧ {0}∩-P = φ`
    - **체 F에 비어있지 않은 부분집합 P가 존재하여 위의 조건을 만족하면 그러한 F를 순서체라 함**
    - **P의 원소를 양수라 함**
  - 순서관계 정의
    - `a,b∈F, a-b∈P => a가 b보다 크다 ≡ a>b ≡ b<a`
    - `a<=b <=> b-a∈P ∨ a=b`
  - 관찰
    - 정수의 집합은 체1 - 체6 과 체8 - 체9 가 성립
    - 0을 제외한 자연수 전체의 집합을 `PZ ⊆ Z`라 두면, 체순의 정의 요건 1-3이 성립한다.
  - 정리
    - `∀a,b,c∈F(순서체)`
      - `a>=b, a<=b => a=b`
      - `a<=b, b<=c => a<=c`
      - `a+b < a+c => b<c`
      - `a>0, b<c => ab < ac`
      - `a<0, b<c => ab > ac`
      - `a^2 >= 0, 특히 1 > 0`
      - `0 < a < b => 0 < 1/b < 1/a`
      - `a,b > 0 => (a^2<b^2 <=> a<b)`