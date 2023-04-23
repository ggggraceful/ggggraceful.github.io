---
title: 🔍 Swagger 사용하기
author: ggggraceful
date: 2023-04-18
categories: [06.HOW TO USE]
tags: [how to use]
---

<br/>
<br/>

Swagger, Rest Docs

<br/>

Swagger 접속 URL
 
http://localhost:8080/swagger-ui/index.html

<br/>
<br/>

SwaggerConfig
```java
import io.swagger.v3.oas.annotations.OpenAPIDefinition;
import io.swagger.v3.oas.annotations.info.Contact;
import io.swagger.v3.oas.annotations.info.Info;
import org.springframework.context.annotation.Configuration;

@OpenAPIDefinition(
		info = @Info(
				title = "Side-Project API",
				description = "사이드프로젝트 API 명세서",
				version = "v1",
				contact = @Contact(
						name = "beginners",
						email = "sample@email.co.kr"
				)
		)
)

@Configuration
public class SwaggerConfig {

//GroupedOpenApi 설정을 하면 그룹 설정된 api 들만 문서에 노출
//    @Bean
//    public GroupedOpenApi sampleGroupOpenApi() {
//        String[] paths = {"/member/**"};
//
//        return GroupedOpenApi.builder().group("샘플 멤버 API").pathsToMatch(paths)
//            .build();
//    }

}
```

<br/>

```java


@Tag(name = "멤버 컨트롤러")
@RequiredArgsConstructor
@RestController
public class MemberController {
	
	
}
```

<br/>


<br/>

