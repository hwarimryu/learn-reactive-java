# Spring MVC vs Webflux

> 참고링크
> - _[토리맘-webflux](https://godekdls.github.io/Reactive%20Spring/springwebflux/#11-overview)_
> - _[토리맘-webflux2](https://godekdls.github.io/Reactive%20Spring/springwebflux2/)_

![img.png](img.png)

### Q. webflux&netty 조합이 기본이다. 왜?
보통 비동기 논블로킹에 netty를 많이 사용하기도 하고, 클라이언트와 서버가 리소스를 공유할 수 있기때문이다.

### Q. mvc&netty 조합, 언제쓰고 어떤 장점이 있을까?
### Q. webflux&tomcat 조합, 언제쓰고 어떤 장점이 있을까?
mvc는 서블릿의 블로킹 I/O를 사용하는데,,

### Q. reactive와 non-blocking 의 주된 이점
고정된 적은 쓰레드와 적은 메모리로도 확장이 가능하다는 것이다.

## 1.1.7 Concurrency Model
- mutable state: 상태공유 신경쓰지 않아도 된다.
- threading model
  - (Default) thread 1개로 서버 운영, CPU 코어 수 만큼의 thread로 요청 처리함.
  - tomcat은 아마 10개..?


## 1.3 Dispatcher Handler
Spring MVC와 동일하게 front controller 패턴을 사용하고, dispatcher servlet(= front controller) 역할을 하는 게 Dispatcher Handler이다.

### DispatcherServlet
클라이언트로부터 어떤 요청(Request)을 받으면 모든 요청을 한 곳에서 받아서 필요한 공통된 처리를 한 후, 요청에 맞는 Handler로 요청을 보내고(Dispatch), 해당 Handler의 실행 결과를 Http Response형태로 만드는 역할을 한다.   
DispatcherServlet이 어떤 Controller를 사용할 지에 대한 전략은 Handler Mapping 전략을 통해서 이루어진다. 즉, 어떤 URL로 들어온 경우 어떤 컨트롤러를 사용할 지 결정한다.   

#### HandlerMapping
request의 URL과 매칭되는, 이 요청을 처리할 handler를 선택하는 역할을 수행하는 인터페이스   
보통 @RequestMapping 어노테이션 사용
> dispatcher servlet  (여기까지가 tomcat, 이 뒤는 spring container)   
<-> handler mapping   
<-> handler adapter <-> controller <-> service <-> repository


### font controller ?
#### 프론트 컨트롤러 패턴 사용 장점.
1. 컨트롤러를 구현할 때 직접 서블릿을 다루지 않아도 된다.
2. 공통 로직 처리가 가능하다.

## 1.5 Functional Endpoints
- 함수형 모델과 어노테이션 모델 중 함수형 모델 사용함.
  ~~HttpHandler vs WebHandler API 중에서 WebHandler API 사용함.~~   
- functional endpoint를 사용했다. 
  - @Controller 사용하지 않고 config에서 router에 handler mapping 하는 방식을 사용했다.   
  - 간단하고 관리포인트가 DispatcherHandler 하나라 편함. 모든 endpoint들을 메서드별 권한까지 다 한 파일에서 관리해서 좋았다.   
  <img src="img_1.png" width="600"/>
- 

