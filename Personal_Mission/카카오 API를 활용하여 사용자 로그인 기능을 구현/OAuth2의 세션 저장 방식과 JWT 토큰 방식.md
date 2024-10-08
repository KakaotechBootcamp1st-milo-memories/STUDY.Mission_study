OAuth2 인증 방식에서 사용자 인증 정보를 저장하는 방법 중 대표적인 방법인 세션 저장 방식과 JWT(JSON Web Token) 토큰 방식에 대해 알아보겠습니다.

## 1. OAuth2 세션 저장 방식

### 작동

사용자가 OAuth2 Provider(예: 카카오, 구글)를 통해 인증을 완료하면, 서버는 사용자 정보를 세션에 저장하고 클라이언트에게 세션 ID를 쿠키로 전달합니다. 이후 클라이언트는 이 쿠키를 사용해 서버와 통신할 때마다 인증 정보를 포함하게 됩니다.

### 특징

- 서버 측에 세션 정보를 저장
- 클라이언트에는 세션 ID만 제공
- 각 요청마다 서버에서 세션 정보를 조회

### 장점

1. 중요 정보가 서버에 안전하게 저장됨
2. 서버에서 세션을 쉽게 무효화하거나 수정 가능
3. 클라이언트-서버 간 세션 ID만 주고받음

### 단점

1. 많은 사용자 동시 접속 시 서버 부담
2. 다중 서버 환경에서 세션 공유 필요
3. CORS(Cross-Origin Resource Sharing) 이슈: 다른 도메인 간 세션 공유가 어려움

## 2. JWT 토큰 방식

### 작동

사용자가 OAuth2 프로바이더(예: 카카오, 구글)를 통해 인증을 완료하면, 서버는 사용자 정보를 세션에 저장하고 클라이언트에게 세션 ID를 쿠키로 전달합니다. 이후 클라이언트는 이 쿠키를 사용해 서버와 통신할 때마다 인증 정보를 포함하게 됩니다.

### 특징

- 클라이언트에 모든 정보를 토큰으로 저장
- 서버는 무상태(Stateless) 방식으로 동작
- 토큰에 사용자 정보와 만료 시간 등을 포함

### 장점

1. 여러 서버 간 사용자 정보 공유가 필요 없음
2. 데이터베이스 조회 없이 인증 가능
3. 다양한 클라이언트에서 사용 용이
4. CORS 문제 해결: 토큰 기반이라 도메인 간 공유 쉬움

### 단점

1. 저장 정보가 많을수록 토큰 크기 증가
2. 토큰 탈취 시 정보 노출 위험, 발급된 토큰의 즉시 무효화가 어려움

## 3. 비교 분석

### 보안성

- 세션 방식이 더 안전할 수 있으나, JWT도 적절히 구현 시 충분히 안전해보임
- 세션: 서버에 정보 저장으로 직접적인 노출 방지
- JWT: 토큰 자체에 정보 포함, 암호화 필요

### 확장성

- 세션: 다중 서버 환경에서 세션 공유 메커니즘 필요
- JWT: 서버 간 사용자 정보 공유 불필요

### 성능

- 세션: 매 요청마다 세션 저장소 조회 필요
- JWT: 토큰 검증만으로 인증 가능, DB 조회 불필요

## 결론

두 방식의 장단점이 있는 만큼 잘 골라서 사용해야할 것 같습니다!

저의 경우 예전 모바일 앱을 개발할 때 세션 저장 방식으로 구현했다가 jwt 토큰 방식으로 변환한 경험이 있습니다!

각 앱의 목적이나 용도를 잘 고려하여 사용해야 할 것 같습니다!!
