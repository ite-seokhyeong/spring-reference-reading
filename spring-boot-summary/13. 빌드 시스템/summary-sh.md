# 13. 빌드 시스템

* <I>Apache Ant</I>
* <I>Apache Maven</I>
* <I>Apache Gradle</I>

<br><br>

<b>Ant, Maven, Gradle</b>은 <b>자바 빌드 툴</b>이다. (순서대로 보완됨)
<br>
즉, 자바 프로젝트의 빌드를 자동화해주는 빌드 툴로, 자바 소스를 컴파일하고 패키징하여 디플로이하는 일을 자동화해주는 것이다. 
<br>

> <b>Build = Compile + Test + Inspect + Deploy</b>
>> 컴파일(소스의 문법을 분석하여 기게어로 변환하는 과정)된 것과 그 외의 것(라이브러리, 이미지)들을 모아서 실행 가능한 파일로 산출하여 서버에 올리는 과정 전반을 의미한다.

<br>

하나의 프로젝트를 생성할 때 필요한 라이브러리가 많아지면서, 
이렇게 많은 각 라이브러리들을 직접 사이트에서 다운받아 추가하는 번거로움을 줄이고, 
프로젝트를 진행하면서 라이브러리의 버전을 쉽게 동기화할 수 있도록 빌드 툴이 등장했다. 
<br>
초기의 자바 프로젝트 빌드 툴로 "Ant"를 많이 사용했지만, 
점점 방대해지는 라이브러리를 더 효율적으로 관리하기 위해 기존의 Ant를 보완한 "Maven", "Gradle"과 같은 빌드 툴도 등장했다.
이 툴들은 자바 프로젝트의 빌드를 자동화해준다. 

<br>

## Apache ANT

<br><br>

## Apache Maven
[메이븐 공식 홈페이지](http://maven.apache.org/)
<br>
<b>자바용 프로젝트 빌드 및 라이브러리 관리 도구</b>로, 필요한 라이브러리를 특정 문서(pom.xml)에 정의해 두면 네트워크를 통해서 라이브러리들을 자동으로 다운받아준다. 따라서 jar 파일을 서로 전송해서 공유할 필요 없이 pom.xml에 필요한 것들 명시해 놓으면 라이브러리를 쉽게 관리할 수 있다. 

<br>
### 플러그인 (Plugin)
[메이븐 플러그인 검색 사이트](http://maven.apache.org/plugins/index.html)
<br>
메이븐에서 제공하는 모든 기능은 플러그인 기반으로 동작한다. "goal"은 플러그인에 포함되어 있는 명령이며 플러그인은 하나 이상의 goal의 집합체이다. 기본 명령어는 `mvn [-option] [<goal(s)>] [phase(s)>]`의 형태이다. 예를 들어, `mvn clean compiler:compile`은 clean 페이즈를 실행하고 compiler 플러그인의 compile 골을 실행한다는 명령어이다. phase에 goal이 연결되어 있으므로 phase를 통해 메이븐 Build를 실행하면 해당 phase에 연결되어 있는 goal이 실행된다. 
<br><br>
메이븐에서 phase는 빌드 라이프사이클에서 빌드 단계와 각 단계의 순서만을 정의하고 있는 개념으로 "단계"를 의미한다. 따라서 phase가 Build 작업을 수행하지는 않으며, 실질적인 Build 작업은 각 phase에 연결되어 있는 플러그인의 goal이 수행한다. 예를 들어, `mvn test`라는 phase를 통해 Build를 수행하면 로그를 통해 `process-resources(resources:resources)`, `compile(compiler:compile)`, `process-test-resources(resources:textResources)`, `test-compile(compiler:testCompile)`, `test(surefire:test)` 순서로 phase가 실행되는 것을 볼 수 있다. 

### 라이프사이클
메이븐에서 미리 정의하고 있는 Build 순서를 의미하며 메이븐에서는 총 3개의 라이프사이클을 제공한다. 
<br>
* 소스코드 컴파일/테스트/패키징/배포를 담당하는 기본 라이프사이클
compile : 소스코드를 컴파일 한다. 
<br>
test : JUnit과 같은 프레임워크를 통해 단위테스트를 한다.
<br>
package(--산출물 생성) : 단위 테스트가 성공하면, pom.xml의 <packaging> 값(jar, war 등)에 따라 압축한다. 
<br>
install(--로컬 저장소 배포) : 개발자 PC 저장소에 압축한 파일을 배포한다. 
<br>
deploy(--원격 저장소 배포) : 외부에 위치한 메이븐 저장소에 압축한 파일을 배포한다. 
<br>
* Build한 결과물을 제거하기 위한 Clean 라이프사이클
clean 페이즈를 실행하면 메이븐 Build를 통해 생성된 모든 산출물을 삭제한다. 메이븐은 기본적으로 모든 산출물을 target 디렉토리에 생성하므로 clean 페이즈를 실행하면 target 디렉토리가 삭제된다. 
<br>
* 프로젝트 문서 사이트를 생성하는 site 라이프사이클
메이븐 설정 파일 정보를 활용하여 프로젝트에 대한 문서 사이트를 생성할 수 있도록 지원한다. site 페이즈는 문서 사이트를 생성하고, site-deploy 페이즈는 생성한 문서 사이트를 설정되어 있는 서버에 배포하는 역할을 한다. 

### 의존성
### 프로필
### POM
<br><br>


## Apache Gradle

