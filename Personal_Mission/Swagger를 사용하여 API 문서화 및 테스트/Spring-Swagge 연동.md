
## SpringFox vs SpringDoc OpenAPI
우선 Spring에 Swagger를 추가하려는데 방법이 2가지가 있었습니다. 바로 SpringFox와 SpringDoc OpenAPI입니다. 둘은 의존성을 추가하는 방식부터 설정 클래스를 구현하는 방법까지 달랐습니다!

**SpringFox 의존성 추가**

**build.gradle**
```groovy
dependencies {
    implementation 'io.springfox:springfox-boot-starter:3.0.0'
}
```

**SpringDoc OpenAPI 의존성 추가**

**build.gradle**
```groovy
dependencies {
    implementation 'org.springdoc:springdoc-openapi-starter-webmvc-ui:2.2.0'
}
```

**SpringFox**와 **SpringDoc OpenAPI**는 각각의 장단점이 있습니다.

**SpringFox**:
- Spring MVC와의 깊은 통합
- 기존 프로젝트에서 Swagger 2를 사용하고 있다면 마이그레이션이 쉽다
- 상대적으로 더 많은 설정이 필요

**SpringDoc OpenAPI**:
- OpenAPI 3 지원
- Spring Boot와의 자연스러운 통합
- 최소한의 설정으로 간단하게 사용 가능
- 최신 OpenAPI 기능 지원

이 중 저는 SpringDoc OpenAPI를 사용하려고 합니다!! 그 이유는 다음과 같습니다!
1. **최신 사양 지원**: OpenAPI 3.0을 지원하며, 최신 API 문서화 표준을 따른다.
2. **간단한 설정**: 최소한의 설정으로 바로 사용할 수 있다.
3. **Spring Boot와의 통합**: Spring Boot와 자연스럽게 통합되어 추가 설정 없이도 사용 가능.
4. **커뮤니티와 지원**: SpringDoc은 활발히 유지 관리되고 있으며, 최신 기능과 버그 수정이 신속하게 이루어진다.
OpenAPI에 대해서는 다음에 알아보겠습니다!!

## Swagger 사용 방법
### 1. Spring 프로젝트에 Swagger 의존성 추가
**SpringDoc OpenAPI 의존성 추가**

**build.gradle**
```groovy
dependencies {
    // Other dependencies

    // SpringDoc OpenAPI dependencies
    implementation 'org.springdoc:springdoc-openapi-starter-webmvc-ui:2.2.0'
}
```

의존성을 추가한 후 프로젝트를 다시 빌드합니다.


### 2. Swagger 설정 클래스 작성

이제, Swagger 설정 클래스를 구현합니다.

**SpringFox 설정**
**SpringDoc OpenAPI 설정**
**src/main/java/com/example/demo/config/OpenApiConfig.java**
```java
package com.example.demo.config;

import io.swagger.v3.oas.models.info.Info;
import io.swagger.v3.oas.models.OpenAPI;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;

@Configuration
public class OpenApiConfig {

    @Bean
    public OpenAPI customOpenAPI() {
        return new OpenAPI()
                .info(new Info()
                        .title("My API")
                        .version("1.0.0")
                        .description("API documentation"));
    }
}
```
### 3. 모델 클래스 작성

API에서 사용될 모델 클래스를 작성합니다. 모델 클래스는 이전 포스팅에서 만들었던 Test 엔티티를 사용할 것이며 이전 포스팅을 보지 않으신 분들을 위해 코드 남겨놓겠습니다!

**src/main/java/com/example/demo/model/Test.java**
```java
package com.example.demo.model;

import jakarta.persistence.Entity;
import jakarta.persistence.GeneratedValue;
import jakarta.persistence.GenerationType;
import jakarta.persistence.Id;

@Entity
public class Test {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    private String name;
    private int age;

    // Getters and Setters
    public Long getId() {
        return id;
    }

    public void setId(Long id) {
        this.id = id;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }
}
```
### 4. 컨트롤러 작성

Swagger가 API를 문서화하기 위해 REST 컨트롤러를 작성합니다.

**src/main/java/com/example/demo/controller/TestController.java**
```java
package com.example.demo.controller;

import com.example.demo.model.Test;
import org.springframework.web.bind.annotation.*;

import java.util.ArrayList;
import java.util.List;

@RestController
@RequestMapping("/api")
public class TestController {

    private List<Test> tests = new ArrayList<>();

    @PostMapping("/tests")
    public Test addTest(@RequestBody Test test) {
        tests.add(test);
        return test;
    }

    @GetMapping("/tests")
    public List<Test> getAllTests() {
        return tests;
    }
}
```



### 5. Swagger UI 접근

이제 애플리케이션을 실행하고 브라우저에서 Swagger UI에 접근할 수 있습니다.

- **SpringDoc OpenAPI Swagger UI**: `http://localhost:8080/swagger-ui.html`



### 결론

