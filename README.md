# 📍 Account Project
## ⚙ Tech Stack
- Language : Java
- Build : Gradle 
- Framework : Spring Boot 2.7.11
- JDK : JDK 11
- Database : H2 Database

## 🔌 Dependencies
- Spring JPA
- Spring validation
- Spring Web
- H2 Database
- Lombok
- Redisson
- Embedded redis

## 🛠 Function
**Function**                 | **구현 완료** | 
:--------------------------  | :----------------: |  
**계좌 생성/해지/확인 기능**  | :heavy_check_mark: | 
**잔액 사용/취소 기능**       | :heavy_check_mark: | 
**거래 확인 기능**            | :heavy_check_mark: | 

## 🔻 RestAPI EndPoint
### ◻ 계좌 API
- 계좌 생성 기능
```
- Method Type : POST
- URI : /account
- Parameter : 사용자 아이디, 초기 잔액
- Policy : 사용자가 없는 경우, 
           계좌가 10개(사용자당 최대 보유 가능 계좌 수)인 경우 
           실패 응답
- Success Response : 사용자 아이디, 계좌번호, 등록일시
```
- 계좌 해지 기능
```
- Method Type : DELETE
- URI : /account
- Parameter : 사용자 아이디, 계좌 번호
- Policy : 사용자 또는 계좌가 없는 경우, 
           사용자 아이디와 계좌 소유주가 다른 경우, 
           계좌가 이미 해지 상태인 경우, 
           잔액이 있는 경우 
           실패 응답
- Success Response : 사용자 아이디, 계좌번호, 해지일시
```
- 계좌 확인 기능
```
- Method Type : GET
- URI : /account?user_id={userId}
- Parameter : 사용자 아이디
- Policy : 사용자 없는 경우 
           실패 응답
- Success Response : 계좌번호, 잔액
```
### ◻ 거래 API
- 잔액 사용 기능
```
- Method Type : POST
- URI : /transaction/use
- Parameter : 사용자 아이디, 계좌 번호, 거래 금액
- Policy :  사용자 없는 경우, 
            사용자 아이디와 계좌 소유주가 다른 경우, 
            계좌가 이미 해지 상태인 경우, 
            거래금액이 잔액보다 큰 경우, 
            거래금액이 너무 작거나 큰 경우,
            해당 계좌에서 이미 거래가 진행 중인 경우
            실패 응답
- Success Response : 계좌번호, 거래 결과 코드(성공/실패), 거래 아이디, 거래금액, 거래일시
```
- 잔액 사용 취소 기능
```
- Method Type : POST
- URI : /transaction/cancel
- Parameter : 거래 아이디, 취소 요청 금액
- Policy : 거래 아이디에 해당하는 거래가 없는 경우, 
           거래금액과 거래 취소 금액이 다른경우(부분 취소 불가능),
           1년이 넘은 거래인 경우
           실패 응답
- Success Response : 계좌번호, 거래 결과 코드(성공/실패), 거래 아이디, 거래금액, 거래일시
```
- 거래 확인 기능
```
- Method Type : GET
- URI : /transaction/{transactionId}
- Parameter : 거래 아이디
- Policy : 해당 거래 아이디의 거래가 없는 경우 
           실패 응답
- Success Response : 계좌번호, 거래종류(잔액 사용, 잔액 사용 취소), 
                     거래 결과 코드(성공/실패), 거래 아이디, 거래금액, 거래일시
```
## ❗ Impression
지난 프로젝트와는 달리 세팅 부분은 비교적 쉽게 할 수 있었지만 Redis가 자꾸 말썽을 피워서 조금 힘들었다. JPA 와 Lombok 의 편리함을 느꼈고, 
이전에 진행한 Spring Boot 프로젝트에서는 테스트코드로 샘플데이터를 만드는 곳에만 활용했었는데 이번 프로젝트에서는 테스트 코드의 작성법과 중요성을 느낄 수 있는 프로젝트였다. 또한 다양한 어노테이션을 활용해봐서 좋았다. 이번에 얻은 경험을 바탕으로 다음 프로젝트에서 더 잘 진행할 수 있도록 해야겠다.  

