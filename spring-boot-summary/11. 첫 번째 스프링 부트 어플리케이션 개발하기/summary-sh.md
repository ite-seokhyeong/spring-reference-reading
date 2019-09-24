# 첫 번째 스프링 부트 어플리케이션 개발하기

* <I>스프링 부트 동작 원리</I>
* <I>실행 가능한 jar 및 war</I>

<br><br>

## 스프링 부트 동작 원리
아래 내용은 Spring boot로 웹 어플리케이션을 생성하는 것을 기준으로 한다. 
<br><br>
Spring boot 1.2.0 버전 이후 등장한 `@SpringBootApplication` 어노테이션은 `@Configuration`, `@EnableAutoConfiguration`, `@ComponentScan` 어노테이션을 포함한다. 이 중, `@EnableAutoConfiguration` 어노테이션은 Spring boot를 구동하는 데 원동력이 되는 어노테이션으로, @SpringBootApplication와 함께 어플리케이션의 전체 컴포넌트를 식별한다. 
<br><br>
가장 먼저, Spring boot는 클래스 패스를 탐색하여 `spring-boot-starter-web` 디펜던시가 선언 됨을 인지하고 웹 어플리케이션을 구성한다. 즉, `@Controller` 어노테이션이 붙고 `@RequestMapping`이 붙은 메서드를 가지고 있는 클래스를 웹 컨트롤러로 보고 `spring-boot-starter-web`의 의존체 중 하나인 톰캣 서버로 어플리케이션을 구동한다. (Spring boot로 웹 어플리케이션을 생성하면 톰캣 서버는 무조건 내장된다. 톰캣 서버를 제거하고 제티나 언더토우와 같은 다른 서버를 대신 사용할 수도 있다)

<br>

### 메인 메소드 동작

### 기본 어노테이션
#### @SpringBootApplication

* <b>@Configuration</b> 
Spring Framework 에서 설정 파일로 쓰겠다 라는 것을 의미!

<br>

* <b>@EnableAutoConfiguration</b>
설정을 자동으로 등록해주는 역할! 즉, 미리 정의되어 있는 빈들을 가져와서 등록해준다. 이렇게 기본적으로 설정되어 있는 빈들은 외부 라이브러리(External Libraries) 중 `spring-boot-autoconfigure`에 정의되어 있다. 이 라이브러리를 열어보면, META-INF/spring.factories 파일에 자동으로 가져올 빈들이 정의되어 있는 것을 볼 수 있다. 이런 식으로 설정들이 기본적으로 정의되어 있고, 프로젝트에서 사용하고자 하는 디펜던시를 설치했을 때 파일에 설정되어 있는대로 적용이 되는 것이다. 
예를 들어, 이 중 `org.springframework.boot.autoconfigure.web.DispatcherServletAutoConfiguration`이라는 것은 DispathcerServlet을 정의해주는 설정 파일이다. 이 패키지는 `org.springframework.boot.autoconfigure.web` 패키지 아래에 있다. 
이러한 설정 구조들을 파악하여 사용자가 빈을 재 정의할 수도 있다. 따라서, DispatcherServlet을 재 정의하는 것도 가능하다. 
정리하면, @EnableAutoConfiguration 어노테이션은 spring.factories 파일에 미리 정의되어 있는  `org.springframework.boot.autoconfigure.EnableAutoCOnfiguration`을 키 값으로 하는 모든 패키지를 가져오는 역할을 하며 각 클래스는 `@Configuration`으로 설정되어 있다. 이 때 모든 설정을 가져오는 것은 아니다. 각 클래스에 붙어 있는 `@Conditional~` 조건을 보고, 조건에 해당하는 경우에 각 Configuration을 참조한다. 즉 웹 환경에 필요한 추가적인 빈을 등록하여 최종적으로 웹 어플리케이션이 구동될 수 있도록 도와준다.

<br>

* <b>@ComponentScan</b>
빈을 등록하는 역할! 
현재 패키지 아래에서 `@Component` 어노테이션이 붙어 있는 클래스들을 찾아서 빈으로 등록한다. Spring MVC 에서 자주 사용하는 `@RestController` 어노테이션도 내부에 `@Component`어노테이션이 포함되어 있으며 `@Configuration`과 같은 설정 파일 어노테이션 자체도 `@Component`이다. 그 외에도 `@Repository`, `@Controller`, `@Service` 

<br>



<br><br>

## 실행 가능한 jar 및 war

기존의 Spring에 비하여 Spring boot가 제공하는 이점 중 대표적인 것이 "단독으로 실행 가능한 JAR"이다. <br>
Spring boot는 기본적으로 JAR 배포형태를 가진다. 
기존의 Spring에서는 Maven이나 Gradle과 같은 디펜던시 툴을 사용하여 WAR 파일을 생성(빌드)한 후 톰캣과 같은 WAS에 배포하여 웹 어플리케이션을 구동(WAR는 톰캣과 같은 웹 서버 위에서 돌아가는 웹 프로젝트라고 생각하면 된다)했던 반면에,
Spring boot는 JAR 파일에 내장 톰캣이 존재하여, JAR 파일을 빌드하고 단순히 실행함으로써 웹 어플리케이션을 구동할 수 있다. 
즉, <b>프로젝트를 빌드할 때 필요하다면 톰캣, 언더토우, 제티와 같은 WAS를 '임베드'하고 그 외에 필요한 스프링 디펜던시들을 모두 함께 JAR로 패키징하여 구동할 수 있다.</b> WAR로 배포하는 것과 다르게, 하나의 JAR 파일로 JVM이 설치되어 있는 어디에서든 동일하게 동작하는 어플리케이션을 가질 수 있다. 이것은 가볍기 때문에 JVM이 설치되어있는 컨테이너에 쉽게 추가할 수 있으며 이미지 빌드 속도 또는 컨테이너 가동 속도를 높일 수 있다. 또한, 'java -jar' 커맨드로 간단하게 구동할 수 있다. 
<br>
http://www.itdaily.kr/news/articleView.html?idxno=83127

<br><br>

### 실행가능한 WAR로 패키징하는 이유
JSP를 사용하는 경우에는, "실행가능한 JAR"가 아닌 "실행가능한 WAR"로 패키징을 해야 한다. 
<br><br>
[참고] Spring boot의 spring-boot-starter-web에 포함된 톰캣은 JSP 엔진을 포함하고 있지 않으므로, 아래와 같이 별도의 설정을 해줘야 JSP 파일을 구동할 수 있다. 
<br><br>
a. jasper와 jstl 디펜던시를 별도로 추가
<br>
b. application.properties에 "spring.mvc.view.prefix=/WEB-INF/jsp/", "spring.mvc.view.suffix=.jsp" 추가
<br>
c. jsp 파일은 Spring boot의 templates 폴더 안에서 동작하지 않으므로 src/main 아래에 "/webapp/WEB-INF/jsp" 폴더를 생성하고 그 안에 .jsp 파일을 생성

<br><br>

### JAR Vs. WAR 
둘 다 jar 툴을 사용한 압축 파일이지만 사용 목적이 다르다. 

#### JAR (= Java Archive)
자바로 작성된 응용 프로그램 또는 라이브러리!
<br>
여러 개의 자바 클래스 파일과 클래스들이 사용하는 관련 리소스 및 메타데이터를 하나의 파일로 묶어서 자바 플랫폼에 응용 소프트웨어나 라이브러리를 배포하기 위한 소프트웨어 패키지 파일 포맷이다. 

#### WAR (= Web Application Archive)
자바로 작성된 웹 응용 프로그램! JAR의 웹 응용 특화 버전으로, 자바 이외에 다른 언어들도 포함되어 있다. 
<br>
자바 서버 페이지(JSP), 자바 서블릿, 자바 클래스, XML, 태그 라이브러리, 정적 웹 페이지(HTML 등) 및 웹 어플리케이션을 구성하는 기타 리소스들을 한 데 모아 배포하는 데 사용되는 JAR 파일이다. 



