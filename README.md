# ooMia Dex Audit
## 유동성풀 비율 검사
### 설명
파일명: Dex.sol

함수명: addLiquidity

줄번호: 67

require(balanceX / amountX == balanceY / amountY);

여기서 유동성 풀의 비율이 일치하는지 확인하는데, 소수점 뒷자리가 버려지게 되어 정확한 연산을 하지 못할 수 있다.
### 파급력
Medium
### 해결방안
require(balanceX * amountY == balanceY * amountX, "Liquidity ratios do not match"); 이 코드를 추가하여 한먼 더 유동성 풀의 비율이 일치하는지 확인할 수 있다.

# hakid29’s Dex Audit
## 가스비 낭비
### 설명
파일명: Dex.sol

함수명: _sqrt

줄번호: 21-28

불필요한 함수 호출로 가스를 낭비한다.
### 파급력
Informational
### 해결방안
public에서 internal로 변경한다.

# rivercastleone’s Dex Audit
## 둘 다 0인 경우 처리
### 설명
파일명: Dex.sol

함수명: swap

줄번호: 67-76

amountX == 0 || amountY == 0이어야한다고 써두고 amountX ==0인 경우와 amountY가 0인 경우만 처리하고있다. 둘 다 0이될 경우 outputAmount가 초기화되지 않아서 문제를 일으킬 수 있다.
### 파급력
medium
### 해결방안
둘다 0일 경우를 처리한다

# GloomyDumber’s Dex Audit
## 권한 관리 필요
### 설명
파일명: Dex.sol

함수명: ming, burn

줄번호: 94, 114

소유자인지 확인하는 로직이 없는데 external로 정의되어있다. 따라서 누구나 mint와 burn을 할 수 있어 문제를 일으킬 수 있다.
### 파급력
high
### 해결방안
소유자인지 확인하는 로직을 추가한다.

# BOB’s Dex Audit
## 둘 다 0인 경우 처리 필요 
### 설명
파일명: Dex.sol

함수명: swap

줄번호: 75 

amountX == 0 || amountY == 0이어야한다고 써두고 amountX ==0인 경우와 amountY가 0인 경우만 처리하고있다. 둘 다 0이될 경우 outputAmount가 초기화되지 않아서 문제를 일으킬 수 있다.
### 파급력
medium
### 해결방안
둘다 0일 경우를 처리한다

# Muang’s Dex Audit
## 둘 다 0인 경우 처리 필요 
### 설명
파일명: Dex.sol

함수명: swap

줄번호: 121

amountX == 0 || amountY == 0이어야한다고 써두고 amountX ==0인 경우와 amountY가 0인 경우만 처리하고있다. 둘 다 0이될 경우 outputAmount가 초기화되지 않아서 문제를 일으킬 수 있다.
### 파급력
medium
### 해결방안
둘다 0일 경우를 처리한다

# Hakid’s Lending Audit
## reentrancy 공격 
### 설명
파일명: UpsideAcademyLending.sol

함수명: withdraw

줄번호: 166-167

사용자가 지정한 금액만큼 이더를 인출하고자 했으나, 공격자가 그 이상의 금액을 여러 번 인출할 수 있다.
### 파급력
Critical
플랫폼이 보유된 자산을 무제한으로 인출 가능하기 때문에, 시스템 전체의 유동성이 고갈될 수 있다.
### 해결방안
상태 업데이트를 먼저 하고 자산을 전송하며, nonReentrant modifier를 추가한다.
