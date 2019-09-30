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

### 플러그인 (Plugin)
[메이븐 플러그인 검색 사이트](http://maven.apache.org/plugins/index.html)
<br>
메이븐에서 제공하는 모든 기능은 플러그인 기반으로 동작한다. "goal"은 플러그인에서 실행가능한 각각의 작업을 의미한다. 메이븐 빌드에서 goal 영역에 작업하고자 하는 명령어를 입력하여 compile, package 등을 실행할 수 있다. 
<br>
```xml
<project>
  ...
  <build>
    <plugins>
      <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-compiler-plugin</artifactId>
        <version>2.1</version>
      </plugin>
    </plugins>
  </build>
  ...
</project>
```
compiler 플러그인을 사용하도록 설정한 예제로, complier 플러그인 하나를 선언함으로써 아래와 같은 goal들을 수행한다. 
* sourceDirectory의 소스 코드를 컴파일하는 compile goal
* testSourceDirectory의 테스트 소스 코드를 컴파일하는 testCompile goal
* compiler 플러그인에 대한 도움말을 제공하는 help goal
<br><br>

maven compiler의 compile goal 실행 명령어는 다음과 같다. 
<br>
mvn org.apache.maven.plugins:maven-compiler-plugin:2.1:compile

<br>

### 라이프사이클
### 의존성
### 프로필
### POM
<br><br>


## Apache Gradle

