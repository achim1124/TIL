# TIL
OSIV 정리
특징
OSIV는 클라이언트 요청이 들어올 때 영속성 컨텍스트를 생성해서 요청이 끝날 때까지 같은 영속성 컨텍스를 유지한다. 하여 한 번 조회된 엔티티는 요청이 끝날 때까지 영속 상태를 유지한다.
엔티티 수정은 트랜잭션이 있는 계층에서만 동작한다. 트랜잭션이 없는 프레젠테이션 계층은 지연 로딩을 포함해 조회만 할 수 있다.

단점
영속성 컨텍스트와 DB 커넥션은 1:1로 물고있는 관계이기 때문에 프레젠테이션 로직까지 DB 커넥션 자원을 낭비하게 됨.
OSIV를 적용하면 같은 영속성 컨텍스트를 여러 트랜잭션이 공유하게될 수도 있다.
프레젠테이션에서 엔티티를 수정하고 비즈니스 로직을 수행하면 엔티티가 수정될 수 있다.
프레젠테이션 계층에서 렌더링 과정에서 지연 로딩에 의해 SQL이 실행된다. 따라서 성능 튜닝시에 확인해야 할 부분이 넓어진다.

## yml 설정 방법(기본값은 true)
spring:
  jpa:
    open-in-view: true    
    
![image](https://user-images.githubusercontent.com/18023672/199469598-9e4034e2-2bf1-4386-ba98-62e3767dc840.png)
