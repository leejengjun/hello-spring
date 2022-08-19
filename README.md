# hello-spring
<h2>스프링부트 스터디 입니다</h2>
<h3>프로젝트 관련한 설명은 추후 작성할 예정입니다.</h3>
<h4>스프링부트 스터디 및 내용 정리 요약은 김영한님의 스프링 입문 - 코드로 배우는 스프링 부트, 웹 MVC, DB 접근 기술 (인프런강의) 를 들으면서 실습 및 내용 정리하였습니다. </h4>
https://www.inflearn.com/course/%EC%8A%A4%ED%94%84%EB%A7%81-%EC%9E%85%EB%AC%B8-%EC%8A%A4%ED%94%84%EB%A7%81%EB%B6%80%ED%8A%B8/dashboard 강의링크
==============================================
<h4>스프링 부트 구축 환경</h4>
---------------------------

Project: Gradle Project

Spring Boot: 2.3.x

Language: Java

Packaging: Jar

Java: 11

Project Metadata

groupId: hello

artifactId: hello-spring

Dependencies: Spring Web, Thymeleaf

DB연동 : DB는 H2 DB를 활용

----------------------------

2022.8.19. 스터디 내용

JPA에 대해서
- 기존의 반복 코드는 물론 기본적인 SQL도 JPA가 직접 만들어서 실행해줌.
- JPA 사용하면, SQL과 데이터 중심의 설계에서 객체 중심의 설계로 패러다임을 전환 할 수 있다.
- JPA 사용하면 개발 생산성을 크게 높일 수 있다.

적용하기 위한 흐름 및 순서는
1) bulid.gradle 파일에 JPA와 사용하는 데이터베이스 관련 라이브러리를 추가
2) 스프링 부트(application.properties)에 JPA 설정 추가
  - 예시
    spring.jpa.show-sql=true
    spring.jpa.hibernate.ddl-auto=none
3) JPA 엔티티 매핑 (도메인 패키지 하위 파일들에서 필요한 부분을 설정함)
  @Entity
 
4) JPA 리포지토리에서 설정 추가
  private final EntityManager em;

5) 서비스 계층에 트랜잭션 추가
  @Transactional
  -  스프링은 해당 클래스의 메서드를 실행할 때 트랜잭션을 시작하고, 메서드가 정상 종료되면 트랜잭션을 커밋한다. 만약 런타임 예외가 발생하면 롤백한다.
  *** JPA를 통한 모든 데이터 변경은 트랜잭션 안에서 실행해야 한다 ***
 
6) JPA를 사용하도록 스프링 설정 변경
  - 간단한 코드 예
  public class SpringConfig 내부에
  private final EntityManager em; 과
  
  @Bean 어노테이션 설정한 리포지토리 내에 
  return new JpaMemberRepository(em); 추가
  
  
 개인생각
 - 본인이 입사전 학원 교육과정에서는 JDBC로 SQL 부분을 코딩하였는데 그 코드의 양이 데이터 처리 과정이 복잡하고 쿼리문이 복잡해질 수록 점점 많아졌다.
   그런데 JPA를 사용하면 제공하는 기능들 (select, insert등)로 인해서 코드양이 줄어드는 것을 볼때 신세계였다.
   이래서 신기술을 공부해야하는 것이구나를 느낄 수 있었다.




