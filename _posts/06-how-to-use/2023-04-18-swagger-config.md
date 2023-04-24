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

SecurityConfig
```java

@EnableWebSecurity
@Configuration
public class SecurityConfig {

  ...

	@Bean
	public SecurityFilterChain filterChain(HttpSecurity httpSecurity) throws Exception {
		httpSecurity
				// token을 사용하는 방식이기 때문에 csrf를 disable합니다.
				.csrf().disable()

				.addFilterBefore(corsFilter, UsernamePasswordAuthenticationFilter.class)

				.exceptionHandling()
				.authenticationEntryPoint(jwtAuthenticationEntryPoint)
				.accessDeniedHandler(jwtAccessDeniedHandler)

				// enable h2-console
				.and()
				.headers()
				.frameOptions()
				.sameOrigin()

				// 세션을 사용하지 않기 때문에 STATELESS로 설정
				.and()
				.sessionManagement()
				.sessionCreationPolicy(SessionCreationPolicy.STATELESS)

				.and()
				.authorizeHttpRequests()
				.requestMatchers(PathRequest.toH2Console()).permitAll()
				.requestMatchers( "/swagger-ui/**", "/v3/api-docs/**").permitAll() // Swagger 추가
				.anyRequest().authenticated()

				.and()
				.apply(new JwtSecurityConfig(tokenProvider));

		return httpSecurity.build();
	}
}

```


<br/>

MemberController
```java

@Tag(name = "멤버 컨트롤러")  // Swagger
@RequiredArgsConstructor
@RestController
public class MemberController {
	
  ...
  
}
```

<br/>

LoginReqDto
```java

@Getter
@NoArgsConstructor
@AllArgsConstructor
public class LoginReqDto {

  @Schema(description = "유저이메일", example = "test123@gmail.com") // Swagger
  @NotNull
  private String email;

  @Schema(description = "패스워드", example = "test123!") // Swagger
  @NotNull
  private String password;
}

```

<br/>

![스크린샷 2023-04-24 오후 10 07 07](https://user-images.githubusercontent.com/109974940/234005346-0eb86f70-de08-4a77-8f10-84b73f9901b4.png)

<br/>
<br/>
