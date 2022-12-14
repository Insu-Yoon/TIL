> **Aspect(앞서 '공통 관심사'라고 학습한 적이 있다) : 부가 기능과 해당 부가 기능을 어디에 적용할 지 정의한 것.**  
> **로깅, 보안, 트랜잭션 등의, 따로 분리한 부가 기능과 그 기능들을 어디에 적용할 지 선택하는 기능을 합쳐 하나의 모듈로 만든 것이 Aspect의 조금 더 구체적인 정의이다.  
> "  Aspect = Module의 일종 = (부가 기능 + 부가 기능의 적용 대상 지정)  "**

> **AOP는 OOP를 대체하는 것이 아니라, OOP의 부족한 부분을 보완하는 목적으로 개발되었다.**

# **AOP의 필요성**

## **기본 개념**

-   핵심 기능(Core Concerns) : 비즈니스 로직을 포함하는 기능
-   부가 기능(Cross-Cutting Concerns) : 핵심 기능을 도와주는 부가적인 기능  
    (ex. 로깅, 보안, 트랜잭션 등)
-   Aspect : 부가 기능을 정의한 코드인 어드바이스(Advice)와 어드바이스를 어디에 적용할 지 결정하는 포인트컷(PointCut)을 합친 개념. (Aspect = Advice + PointCut)

## **좋은 OOP가 되려면**

-   OOP는 공통된 목적을 띤 데이터와 동작을 묶어 하나의 객체로 정의 
-   하나의 객체를 규정하는 클래스/인터페이스가 온갖 기능을 다 가지고 있다? 좋은 설계는 아님
-   객체를 잘 활용하기 위해서는 관심사 분리의 디자인 원칙을 준수해야함
-   **관심사의 분리는 모듈화의 핵심**

## **그런데 말입니다**

기본 개념과 좋은 OOP 설계에 대한 이해가 되었다면 다음 상황을 가정해보자

-   웹 애플리케이션을 만드는 데, 로그도 남기고 보안도 신경쓰면서 트랜잭션도 구현해야한다.
-   위에서 언급한 기능들은 제작하려는 웹 애플리케이션의 핵심 기능과는 관련없지만, 필수적인 부가기능이다.
-   해당 부가기능들은 불특정 다수의 클래스에 존재하게 된다.  
    (관심사 관점에서 로깅, 보안, 트랜잭션 코드들은 횡단 관심사(Cross-cutting Concerns)라고 한다.

위와 같은 상황이라면, 비즈니스 클래스에 핵심 기능과 부가 기능이 공존하게 된다. 당연히 코드가 복잡해지고, 핵심 코드(비즈니스 코드) 파악이 어려울 것이다. 또한 부가 기능의 메소드가 필요에 따라 각각 다르게, 반복적으로 구현되므로, 횡단 관심사의 모듈화가 어렵다.

이러한 상황은 OOP만으로는 해결하기 어려웠다고 한다.

> 문득, '그냥 인터페이스 만들어서 필요할 때만 적용하면 되는거 아냐? 왜 OOP로는 안된다는거야?'  
> 라는 생각이 들었는데, 곧장 '아, 그게 AOP인가?' 하고 납득했다.  
> 정확히 내가 생각한 방식이 AOP가 맞는지에 대해서는, AOP의 이해가 끝나면 다시 되돌아보자.

## **그래서 AOP가 등장했다**

> **AOP는 기존과 다른 프로그램 구조 사고 방식을 제공함으로써 OOP의 부족한 부분을 보완한다.**  
> **OOP에서 모듈화의 핵심 단위는 클래스이고, AOP에서 모듈화의 핵심 단위는 관점이다.**

AOP는 애플리케이션 로직을 크게 핵심 기능과 부가 기능으로 나눠서 다룬다. 핵심 기능은 객체가 제공하는 고유의 기능(업무 로직 등을 포함)이며, 부가 기능은 핵심 기능을 보조하기 위한 기능으로, 로직, 보안, 트랜잭션 기능 등이 있다. 

-   핵심 기능인 비즈니스 로직과 부가 기능이 하나의 객체로 들어가게 된다.
-   부가 기능이 필요한 경우엔 위와 같은 형태로 합쳐져서 하나의 로직을 완성하게 된다.
-   서비스를 실행하면 핵심 기능과 부가 기능이 함께 실행된다.


---

> 공부중 메모  
>   
> aspect - 공통 관심사 ( 처리할 로직? 행동? ex. 로그남기기, 보안 등등) ( " 무엇을 " )  
>   
> 조인 포인트 - 앱 실행 흐름에서 특정 포인트. (메서드 호출, 객체 인스턴스화, 필드 접근 등등) 이 조인 포인트에 AOP 적용할거임 ! 근데 스프링 AOP는 프록시 방식이라, 메서드 실행 지점에서만 사용가능함. 따라서 조인 포인트는 메서드 실행 지점 딱 하나로 한정됨  
>   
> 어드바이스 - 조인포인트에서 수행되는 코드. Aspect를 언제 핵심 코드에 적용할 지 정의한다. ( " 언제? " )  
>   
> 포인트컷 - 조인 포인트 중 어드바이스가 적용될 위치를 특정한다 ( " 어디에? " )

---

# **AOP 용어 및 개념 정리**

## **애스팩트(Aspect)**

> **공통 관심사 ! -> 무엇을 할 것인가?**

-   여러 객체에 공통으로 적용되는 기능(공통 기능)
-   어드바이스 + 포인트컷을 모듈화한 횡단 기능. (애플리케이션에 포함된다)
-   여러 어드바이스와 포인트컷이 함께 존재한다.

## **조인 포인트(Join Point)**

> **AOP를 적용할 수 있는 부분들 ! - Spring AOP는 메서드로 실행 전후로 고정**

-   클래스 초기화, 객체 인스턴스화, 메소드 호출, 필드 접근, 예외 발생 등등
-   애플리케이션 실행 흐름에서의 특정 포인트 의미
-   횡단 관심(공통 관심)은 조인포인트 전/후에 AOP에 의해 자동으로 추가된다.
-   스프링 AOP는 프록시 방식을 사용하므로, 조인 포인트는 항상 메소드 실행 지점으로 제한됨
-   프록시 방식을 사용하는 스프링 AOP의 경우, 스프링 컨테이너가 관리할 수 있는 스프링 빈에만 AOP 적용가능
-   어드바이스의 종류에 따라 사용 방법이 다르지만, 기본적으로 어드바이스 메서드에 매개변수로 선언하여 사용 가능

## **어드바이스(Advice)**

> **언제 적용할 것인가? (Before, AfterReturn, AfterThrowing, After, Around)**

-   조인 포인트에서 수행되는 코드
-   Aspect를 언제 핵심 코드에 적용할 지를 정의함
-   시스템 전체 에스펙트에 API 호출을 제공함
-   단어 그대로 조인 포인트의 실행 전, 후, 반환후, 예외발생 시 AOP를 적용
-   Around는 메서드 호출 전후에 수행하며, 가장 강력한 어드바이스다.
    -   조인 포인트의 실행 여부 선택, 반환 값 변환, 예외 변환 등이 가능하다
-   어드바이스의 첫 번째 파라미터는 ProceedingJoinPoint를 사용해야 한다.
-   proceed()는 '메서드를 실행한다' - 여러번 사용 가능

@Around만 있어도 모든 기능의 수행이 가능하다. 하지만 타겟 등 고려해야할 사항이 있을 때 정상적으로 작동하지 않을 수 있다. 따라서 @Around만 사용하기보단, 제약을 가지더라도 적절한 애너테이션이 있다면 그걸 사용하도록 하자

## **포인트컷(Pointcut)**

> **조인 포인트 중에서 어드바이스가 적용될 위치를 선별 ! -> 어디에 적용할 것인가?  
> **

-   조인 포인트 중 어드바이스를 적용할 조인 포인트를 고른다.
-   스프링 AOP는 프록시를 사용하므로, 메서드 실행 지점만 포인트컷으로 선별 가능

### **일반적인 pointcut 표현식들**

-   모든 public 메서드 실행
    -   execution(public \* \*(..))

-   set 다음 이름으로 시작하는 모든 메서드 실행
    -   execution(\* set\*(..))

-   AccountService 인터페이스에 의해 정의된 모든 메서드 실행
    -   execution(\* com.xyz.service.AccountService.\*(..))

-   service 패키지에 정의된 메서드 실행
    -   execution(\* com.xyz.service.\*.\*(..))

-   서비스 패키지 또는 서비스 패키지의 하위 패키지 중 하나에 정의된 메서드 실행
    -   execution(\* com.xyz.service..\*.\*(..))

-   서비스 패키지 내의 모든 조인 포인트 **(Spring AOP에서만 메서드 실행)**
    -   within(com.xyz.service.\*)

-   서비스 패키지 또는 하위 패키지 중 하나 내의 모든 조인 포인트 **(Spring AOP에서만 메서드 실행)**
    -   within(com.xyz.service..\*)

-   AccountService 프록시가 인터페이스를 구현하는 모든 조인 포인트 **(Spring AOP에서만 메서드 실행)**
    -   this(com.xyz.service.AccountService)

-   AccountService 대상 객체가 인터페이스를 구현하는 모든 조인 포인트 **(Spring AOP에서만 메서드 실행)**
    -   target(com.xyz.service.AccountService)

-   단일 매개변수를 사용하고 런타임에 전달된 인수가 Serializable과 같은 모든 조인 포인트 **(Spring AOP에서만 메소드 실행)**
    -   args(java.io.Serializable)

-   대상 객체에 @Transactional 애너테이션이 있는 모든 조인 포인트 **(Spring AOP에서만 메서드 실행)**
    -   @target(org.springframework.transaction.annotation.Transactional)

-   실행 메서드에 @Transactional 애너테이션이 있는 조인 포인트 **(Spring AOP에서만 메서드 실행)**
    -   @annotation(org.springframework.transaction.annotation.Transactional)

-   단일 매개 변수를 사용하고 전달된 인수의 런타임 유형이 @Classified 애너테이션을 갖는 조인 포인트(Spring AOP에서만 메서드 실행)
    -   @args(com.xyz.security.Classified)

-   tradeService 라는 이름을 가진 스프링 빈의 모든 조인 포인트 **(Spring AOP에서만 메서드 실행)**
    -   bean(tradeService)

-   와일드 표현식 \*Service 라는 이름을 가진 스프링 빈의 모든 조인 포인트
    -   bean(\*Service)

## **위빙(Weaving)**

> **스프링AOP에서의 위빙 = 프록시 방식으로 AOP가 구현되는 과정**

-   포인트컷으로 결정한 타겟의 조인 포인트에 어드바이스를 적용하는 것
-   핵심 코드에 영향을 주지 않고 부가 기능을 추가할 수 있다.
-   AOP 적용을 위해 Aspect 객체에 연결한 상태이다.
    -   컴파일 타임 - 컴파일 시점에(.java가 .class로 변환될 때) AOP 적용
    -   로드 타임 - 컴파일 후 메모리에 올라가는 시점에 AOP 적용
    -   런타임 - 런타임에 AOP 적용(Spring AOP는 여기에 해당)

위빙은 위의 세 시점에서 일어날 수 있다. 스프링 AOP는 프록시 방식이며, 런타임에 실행된다.

스프링 AOP가 런타임에 적용될 수 있는 이유?

-   IoC덕분. 런타임에도 스프링 컨테이너가 제어권을 갖고 객체를 다루기 때문에 런타임에 .AOP적용이 가능하다 !

> **더 공부해보면 좋을 내용 : JDK 동적 프록시, CGLIB 프록시**
