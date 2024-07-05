# Task 4. 카카오 개발자 사이트에서 애플리케이션 등록
- [카카오 내 어플리케이션](https://developers.kakao.com/console/app)으로 들어가서 애플리케이션 추가하기 후 정보 등록!
![image](https://github.com/KakaotechBootcamp1st-milo-memories/STUDY.Mission_study/assets/102672547/319b1287-2f5a-4e1b-840c-dcc8c7e9f900)
- 등록 완료!!(SweeTODO는 저번에 한 프로젝트입니다!)
![image](https://github.com/KakaotechBootcamp1st-milo-memories/STUDY.Mission_study/assets/102672547/d8366d21-142a-44a6-9a5a-6fff29bf4f84)

# Task 5. 발급된 CLient ID와 Secret Key를 사용하여 API 설정
- 저는 Spring을 사용하기 때문에 Client ID는 앱 키 메뉴의 REST API 키이고 Secret Key는 따로 코드를 생성해야합니다.
- 앱 키 메뉴
  ![image](https://github.com/KakaotechBootcamp1st-milo-memories/STUDY.Mission_study/assets/102672547/0924c112-2385-4af8-801b-cfb29b397b36)
- Client Secret 생성
  - 카카오 로그인 - 보안 - Client Secret - 코드 생성
    ![image](https://github.com/KakaotechBootcamp1st-milo-memories/STUDY.Mission_study/assets/102672547/75dec591-b103-4004-b374-1cc1015b57b5)
- [위 단계에서 참고했던 카카오 공식 문서](https://developers.kakao.com/docs/latest/ko/kakaologin/rest-api#request-code-request)
## API 설정
```
spring.security.oauth2.client.registration.kakao.client-id={클라이언트 ID(REST API 키)}
spring.security.oauth2.client.registration.kakao.client-secret={클라이언트 비밀번호}
spring.security.oauth2.client.registration.kakao.scope=profile_nickname
spring.security.oauth2.client.registration.kakao.authorization-grant-type=authorization_code
spring.security.oauth2.client.registration.kakao.redirect-uri=http://localhost:8080/login/oauth2/code/kakao
spring.security.oauth2.client.registration.kakao.client-name=Kakao
spring.security.oauth2.client.provider.kakao.authorization-uri=https://kauth.kakao.com/oauth/authorize
spring.security.oauth2.client.provider.kakao.token-uri=https://kauth.kakao.com/oauth/token
spring.security.oauth2.client.provider.kakao.user-info-uri=https://kapi.kakao.com/v2/user/me
spring.security.oauth2.client.provider.kakao.user-name-attribute=id
```

# Task 6. OAuth 2.0 인증을 위한 리다이렉트 URI 설정
- [Redirect URI 등록 공식 문서](https://developers.kakao.com/docs/latest/ko/kakaologin/prerequisite#kakao-login-redirect-uri)
- 카카오 로그인은 서비스 로그인 과정에서 Redirect URI를 통해 서비스에서 요청한 인가 코드와 토큰을 전달합니다. 저는 우선 로컬 환경에서 테스트해보기 위해 "http://localhost:8080/login/oauth2/code/kakao"로 등록하였습니다.
- 카카오 로그인-Redirect URI
  ![image](https://github.com/KakaotechBootcamp1st-milo-memories/STUDY.Mission_study/assets/102672547/0cc5736a-b826-4515-88e0-e8bebbca386d)
