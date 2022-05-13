# Springboot-ErrorHandling

본 프로젝트는 스프링부트에서 어떻게 에러처리를 하는지 작성한 코드입니다.

## 인증 / 인가 스프링 내부구조

먼저 Spring의 인증/ 인가 부분의 내부 구조를 살펴보자. 

<img width="823" alt="스크린샷 2022-05-12 오후 3 25 26" src="https://user-images.githubusercontent.com/45115557/168235488-d61254bd-55a1-4895-a49e-42542262c7c6.png">

FilterSecurityInterceptor에서 스프링시큐리티 내 예외를 감지한다. 

ExceptionTranslationFilter에서 인증/인가 예외를 처리하고 종류에 따라 AuthenticationException 혹은 AccessDeniedException을 발생시킨다. 

## Custom 인증 Exception 발생

스프링 시큐리티에서 제공하는 필터를 사용해서 인증오류 발생시 에러를 발생시킨다. 

```java
public class JwtFilter extends OncePerRequestFilter {

	@Autowired
	private AuthenticationEntryPoint entryPoint;

	@Override
	protected void doFilterInternal(HttpServletRequest request, HttpServletResponse response, FilterChain filter) throws ServletException, IOException {

		try{
				//인증로직
		}catch(JWTException e){
		
			entryPoint.commence(request,response, new authException());

		}
	}

}
```

## 인증실패 처리

인증실패 처리는 **AuthenticationEntryPoint**를 통해 할 수 있다. 

```java
public class AuthenticationErrorHandler implements AuthenticationEntryPoint {

	@Override
	public void commence(HttpServletRequest request, HttpServletResponse response, AuthenticationException authException) throws IOException {
		
		//logging 등 에러처리
		
	}
}
```

