# **정규화의 필요성**

정규화를 거치지 않았을 때 데이터 베이스에서 발생하는 일을 먼저 확인해보면, 정규화의 필요성과 목적이 조금 더 명확하게 다가올 것 같다.

## **1\. 이상(Anomaly) 현상**

> **릴레이션 : 테이블과 거의 같은 개념의 용어로 사용되지만, 엄밀히 말하면 릴레이션이 테이블에 포함되는 관계다.**  
> **아래의 내용에서는 '테이블'로 받아들여도 크게 문제되지 않는다.**

-   정규화를 거치지 않은 데이터베이스에서 발생할 수 있는 현상
-   데이터들이 불필요하게 중복되어 릴레이션 조작에 문제 발생
-   속성들의 종속 관계를 하나의 릴레이션에 표현하기 때문에 발생

위의 이유로 발생하는 이상 현상은 아래의 세 가지로 분류된다.

-   삽입 이상(Insertion Anomaly)  
    데이터 삽입 시 의도와 다른 값들도 삽입됨
-   삭제 이상(Delete Anomaly)  
    데이터 삭제 시 의도와 다른 값들도 연쇄 삭제됨
-   갱신 이상(Update Anomaly)  
    속성값 갱신 시 일부 튜플만 갱신되어 모순 발생

## **2\. 데이터 중복**

-   일관된 자료 처리 어려움
-   저장 공간 낭비
-   데이터 효율성 감소

## **3\. 데이터 무결성**

**이 항목은 정규화를 통해 피하려는 대상인 1, 2와 다르게, 정규화를 통해 추구하는 목표에 속한다.**

데이터 무결성이란 데이터의 수명 주기 동안 정확성과 일관성을 유지하는 것을 뜻한다. 쉽게 표현하면 '입력된 데이터가 오염되지 않고 입력된 그대로 데이터를 사용할 수 있다'는 의미이다.

# **정규화란?**

정규화의 기본적인 목표는 '테이블 간 데이터의 중복을 허용하지 않는다' 이다. 정규화를 통해 아래의 이점을 가져갈 수 있다.

-   중복을 배제하여 삽입, 삭제, 갱신 이상을 방지
-   각 릴레이션에 중복된 종속성을 여러개의 릴레이션에 분할
-   어떠한 릴레이션이라도 데이터베이스 내에서 표현 가능하게 함
-   데이터 삽입 시 릴레이션을 재구성할 필요성 감소
-   효과적인 검색 알고리즘 생성 가능

아직 '정규화'라는 개념이 생소하지만, 위의 내용을 통해 "아, 중복을 허용하지 않도록 데이터 베이스를 잘 정리하는 건가보다." "데이터 베이스를 잘 정리해둠으로써 데이터를 추가하거나, 데이터를 검색할 때 이득을 보는 거구나" 라는 생각이 들었다.

정규화에도 여러 단계가 있고, 그에 따른 방법들이 존재한다. 해당 내용은 아래 링크에서 확인할 수 있다.

추후 필요하다면 링크를 통해 더 깊게 학습하자.

[itwiki.kr/w/데이터베이스\_정규화](https://itwiki.kr/w/%EB%8D%B0%EC%9D%B4%ED%84%B0%EB%B2%A0%EC%9D%B4%EC%8A%A4_%EC%A0%95%EA%B7%9C%ED%99%94 "정규화 링크")
