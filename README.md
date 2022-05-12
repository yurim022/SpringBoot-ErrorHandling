# Springboot-ErrorHandling

# 인증 / 인가 스프링 내부구조

먼저 Spring의 인증/ 인가 부분의 내부 구조를 살펴보자. 

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/693a95a5-0ab5-4882-b135-203546137e90/Untitled.png)

FilterSecurityInterceptor에서 스프링시큐리티 내 예외를 감지한다. 

ExceptionTranslationFilter에서 인증/인가 예외를 처리하고 종류에 따라 AuthenticationException 혹은 AccessDeniedException을 발생시킨다. 

# Custom 인증 Exception 발생

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

# 인증실패 처리

인증실패 처리는 **AuthenticationEntryPoint**를 통해 할 수 있다. 

```java
public class AuthenticationErrorHandler implements AuthenticationEntryPoint {

	@Override
	public void commence(HttpServletRequest request, HttpServletResponse response, AuthenticationException authException) throws IOException {
		
		//logging 등 에러처리
		
	}
}
```

참고링크: 

[https://bcp0109.tistory.com/301](https://bcp0109.tistory.com/301)

[https://the-boxer.tistory.com/2](https://the-boxer.tistory.com/2)

[https://055055.tistory.com/96](https://055055.tistory.com/96)

[https://bamdule.tistory.com/149](https://bamdule.tistory.com/149)

[https://www.baeldung.com/spring-mvc-handlerinterceptor](https://www.baeldung.com/spring-mvc-handlerinterceptor)

[https://www.baeldung.com/java-threadpooltaskexecutor-core-vs-max-poolsize](https://www.baeldung.com/java-threadpooltaskexecutor-core-vs-max-poolsize)

[https://hanswsw.tistory.com/17](https://hanswsw.tistory.com/17)

[https://ktko.tistory.com/entry/Spring-AOP구현Aspect-어노테이션-사용](https://ktko.tistory.com/entry/Spring-AOP%EA%B5%AC%ED%98%84Aspect-%EC%96%B4%EB%85%B8%ED%85%8C%EC%9D%B4%EC%85%98-%EC%82%AC%EC%9A%A9)

[https://linkeverything.github.io/springboot/spring-aop/](https://linkeverything.github.io/springboot/spring-aop/)

[https://stackoverflow.com/questions/43124391/restcontrolleradvice-vs-controlleradvice](https://stackoverflow.com/questions/43124391/restcontrolleradvice-vs-controlleradvice)

[[Spring] Rest API Exception Handling](https://blog.naver.com/PostView.naver?blogId=writer0713&logNo=221605253778&parentCategoryNo=&categoryNo=83&viewDate=&isShowPopularPosts=true&from=search)

[https://kogle.tistory.com/115](https://kogle.tistory.com/115)

[https://galid1.tistory.com/494](https://galid1.tistory.com/494)

[https://coder-in-war.tistory.com/entry/Spring-Security-05-인증인가-API의-예외처리](https://coder-in-war.tistory.com/entry/Spring-Security-05-%EC%9D%B8%EC%A6%9D%EC%9D%B8%EA%B0%80-API%EC%9D%98-%EC%98%88%EC%99%B8%EC%B2%98%EB%A6%AC)
