# 단방향 해쉬 함수 (one-way hash function)
수학적 연산으로 원본메시지를 변환하여 암호화된 메시지(다이제스트)를 생성.

비슷한 글자라도 완전히 다른 결과를 얻을 수 있음.

## 공격에 대한 보완책 필요
 - 솔팅 (salting) - 임의로 특정값을 추가하여 해쉬된 다이제스트를 더 복잡하게 만듬
 - 키 스트레칭 - 다이제스트를 생성하고 생성된 다이제스트로 다시 다이제스트를 생
  
## Adaptive Key Derivation Functions 
 솔팅과 키 스트레칭을 이용하여 보안을 제공 

### PBKDF2
솔트를 적용한 후 해시 함수의 반복 횟수를 임의로 선택할 수 있다. PBKDF2는 아주 가볍고 구현하기 쉬우며, SHA와 같이 검증된 해시 함수만을 사용한다.

```javascript
DIGEST = PBKDF2(PRF, Password, Salt, c, DLen)  

```

### bcrypt
패스워드 저장을 목적으로 설계. 

`work factor` 를 조정하는 것만으로 간단하게 시스템의 보안성을 높일 수 있다.

```
String hashed = BCrypt.hashpw(password, BCrypt.gensalt(11));
```
## 참고
* https://d2.naver.com/helloworld/318732