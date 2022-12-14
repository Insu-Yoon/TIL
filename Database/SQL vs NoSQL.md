# **SQL과 NoSQL**

데이터베이스는 크게 관계형 데이터베이스(RDB)와 비관계형 데이터베이스(NoSQL)로 구분한다. RDB는 SQL을 기반으로 하고, NoSQL은 NoSQL로 데이터를 다룬다.(표현이 어색하지만, 비관계형 데이터베이스는 NoSQL로 부르고, 해당 데이터 베이스를 다루는 언어도 NoSQL로 부른다.)

## **SQL**

관계형 데이터베이스에서는 테이블의 구조, 데이터 타입 등을 사전에 정의하고, 테이블에 정의된 내용에 알맞은 형태의 데이터만 삽입할 수 있다. 이 과정에서 데이터는 행(row)과 열(column)로 구성된 테이블에 저장된다.

각 열은 하나의 속성에 대한 정보를 저장하며, 행에는 각 열의 데이터 형식에 맞는 데이터가 저장된다. 이렇게 특정한 형식을 지키기 때문에, 데이터를 정확히 입력했다면 데이터를 사용할 때 매우 수월하다. 관계형 데이터베이스에서는 SQL을 사용해 원하는 정보를 추출할 수 있는데, 이 말은 관계형 데이터베이스에서 스키마(Schema)가 뚜렷하게 보인다는 뜻이며, 또한 관계형 데이터베이스에서는 테이블 간의 관계가 직관적으로 파악가능하다는 의미이다.

대표적인 관계형 데이터베이스에는 MySQL, Oracle, SQLite, PostgresSQL, MariDB 등이 있다.

## **NoSQL**

NoSQL은 데이터가 고정되어 있지 않은 데이터베이스를 가르킨다. 그렇다고 해서 NoSQL에 스키마가 반드시 없는 것은 아니다. 관계형 데이터베이스에서는 데이터를 입력할 때 스키마에 맞게 입력해야 하는 반면, NoSQL에서는 데이터를 읽어올 때 스키마에 따라 데이터를 추출한다. 이런 방식을 'schema on read'라고도 부른다.

그리고 NoSQL이 데이터를 쓸 때 정해진 방식이 아예 없다는 의미도 아니다. 데이터를 입력하는 방식에 따라, 데이터를 읽어올 때 영향을 미친다.

대표적인 NoSQL은 몽고DB, Cassandra 등이 있다.

NoSQL기반의 비관계형 데이터베이스는 일반적으로 다음과 같이 구성된다.

-   Key-Value 타입 : 속성을 Key-Value 쌍으로 나타내는 데이터를 배열의 형태로 저장한다.  
    Redis, Dynamo 등이 대표적인 Key-Value 형식의 데이터 베이스이다.
-   문서형 데이터베이스 : 데이터를 테이블이 아닌 문서처럼 저장하는 데이터베이스이다. 많은 문서형 데이터베이스에서 JSON과 유사한 형식의 데이터를 문서화하여 저장한다. 각각의 문서는 하나의 속성에 대한 데이터를 가지고 있으며, 컬렉션이라고 하는 그룹으로 묶어서 관리한다.  
    MongoDB가 대표적인 문서형 데이터베이스이다.
-   Wide-Column 데이터베이스 : 데이터의 열(column)에 대한 데이터를 집중적으로 관리하는 데이터베이스이다. 각 열에는 key-value 형식으로 데이터가 저장되고, 컬럼 패밀리(column families)라고 하는 열의 집합체 단위로 데이터를 처리한다. 하나의 행에 많은 열을 포함할 수 있어 유연성이 높다. 데이터 처리에 필요한 열을 유연하게 선택할 수 있다는 장점 덕분에 규모가 큰 데이터 분속에 주로 사용되는 데이터베이스 형식이다.  
    Cassandra, HBase가 대표적인 Wide-Column 데이터베이스이다.
-   그래프 데이터베이스 : 자료구조의 그래프와 비슷한 형식으로 데이터 간의 관계를 구성하는 데이터베이스이다. node에 속성별 데이터를 저장하며, 각 노드간의 관계는 선(edge)로 표현한다.  
    Neo4J, InfiniteGraph가 대표적인 그래프 데이터베이스이다.

# **관계형 데이터베이스와 비관계형 데이터 베이스의 차이**

## **데이터 저장(Storage)**

-   관계형 데이터베이스는 SQL을 이용하여 데이터를 테이블에 저장한다. 미리 작성된 스키마를 기반으로 정해진 형식에 맞게 데이터를 저장해야 한다.
-   비관계형 데이터베이스는 key-value, document, wide-column, graph 등의 방식으로 데이터를 저장한다.

## **스키마(Schema)**

-   SQL을 사용하려면, 고정된 형식의 스키마가 필요하다. 따라서 처리하려는 데이터 속성별로 열(column)에 대한 정보를 미리 정해두어야 한다. 스키마는 나중에 변경할 수 있지만, 이 경우 데이터베이스 전체를 수정하거나 오프라인(down-time)으로 전환할 필요가 있다.
-   NoSQL은 관계형 데이터베이스보다 동적으로 스키마의 형태를 관리할 수 있다. 행을 추가할 때 즉시 새로운 열을 추가할 수 있고, 개별 속성에 대해 모든 열의 데이터를 반드시 입력하지 않아도 된다.

## **쿼리(Query)**

-   관계형 데이터베이스는 테이블의 형식과 테이블 간의 관계에 맞춰 데이터를 요청해야 한다. 그래서 SQL과 같이 구조화된 쿼리 언어를 사용한다.
-   비관계형 데이터베이스의 쿼리는 데이터 그룹 자체를 주회하는 것에 초점을 두고 있다. 따라서 구조화되지 않은 쿼리 언어로도 데이터 요청이 가능하다. UnQL(UnStructured Query Language)라고 말하기도 한다.

## **확장성(Scalability)**

-   일반적으로 관계형 데이터베이스는 수직적으로 확장한다. 높은 메모리, cpu를 사용하는 확장이라고도 한다. 데이터베이스가 구축된 하드웨어의 성능을 많이 사용하기 때문에 비용이 많이 든다. 여러 서버에 걸쳐 데이터베이스의 관계를 정의할 수 있지만, 매우 복잡하며 시간이 많이 소모된다.
-   NoSQL로 구성된 데이터베이스는 수평적으로 확장한다. 서버 증설 비용이 비교적 저렴하며, 클라우드 서비스를 이용하는 확장도 가능하다. NoSQL 데이터베이스를 위한 서버를 추가적으로 구축하면, 많은 트래픽을 보다 편리하게 처리할 수 있다.

# **SQL vs NoSQL 선택 가이드**

> 데이터베이스를 구축하는 방법을 선택하는 것에 완벽한 정답은 없다. 그래서 많은 개발자들은 유저의 요구를 충족하기 위해 관계형, 비관계형 데이터베이스를 모두 활용하여 서비스에 맞게 설계하고 있다. NoSQL 기반의 비관계형 데이터베이스가 확장성, 속도면에서는 더 뛰어나지만, 고차원으로 구조화된 SQL 기반의 데이터베이스가 더 좋은 성능을 보여주는 서비스도 있다. 여러 사용 사례를 살펴보고 적절한 데이터베이스를 선택하는 것이 중요하다.

## **SQL 기반의 관계형 데이터베이스를 사용하는 경우**

-   데이터베이스가 ACID 성질을 준수해야 하는 경우  
    SQL을 사용하면 데이터베이스와 상호작용 하는 방식을 정확하게 규정할 수 있기 때문에, 데이터베이스에서 데이터를 처리할 때 발생할 수 있는 예외적인 상황을 줄이고, 데이터베이스의 무결성을 보호할 수 있다.  
    전자 상거래를 비롯한 모든 금융 서비스를 위한 소프트웨어 개발에서는 반드시 데이터베이스의 ACID 성질을 준수해야한다. 그래서 이런 경우 일반적으로 SQL 기반의 데이터베이스를 사용한다.
-   소프트웨어에 사용되는 데이터가 구조적이고 일관적인 경우  
    소프트웨어(프로젝트)의 규모가 많은 서버를 필요로 하지않고, 일관된 데이터를 사용하는 경우에는 관계형 데이터베이스를 사용하는 경우가 많다. 다양한 데이터 유형과 높은 트래픽을 지원하도록 설계된 NoSQL 데이터베이스를 사용해야할 이유가 없기 때문이다.

## **NoSQL 기반의 비관계형 데이터베이스를 사용하는 경우**

-   데이터의 구조가 거의, 또는 전혀 없는 대용량의 데이터를 저장하는 경우  
    대부분의 NoSQL 데이터베이스는 저장할 수 있는 데이터의 유형에 제한이 없다. 필요에 따라 언제든지 데이터의 새 유형을 추가할 수 있다. 소프트웨어 개발에 정형화되지 않은 많은 양의 데이터가 필요한 경우, NoSQL을 적용하는 것이 더 효율적일 수 있다.
-   클라우드 컴퓨팅 및 저장공간을 최대한 활요하는 경우  
    클라우드 기반의 데이터베이스를 구축하면 저렴한 비용의 솔루션을 제공받을 수 있다. 소프트웨어에 데이터베이스의 확장서잉 중요하다면, 별다른 번거로움 없이 확장할 수 있는 NoSQL 데이터베이스를 사용하는 것이 좋다.
-   빠르게 서비스를 구축하는 과정에서, 데이터 구조를 자주 업데이트 하는 경우  
    NoSQL데이터베이스의 경우 스키마를 미리 준비할 필요가 없기 때문에 빠르게 개발하는 과정에서 매우 유리하다. 시장에 빠르게 프로토타입을 출시해야 하는 경우가 위의 경우에 해당한다. 또한 소프트웨어 버전별로 많은 Down-time 없이 데이터 구조를 자주 업데이트 해야하는 경우, 매번 스키마를 수정해야 하는 관계형 데이터베이스보다 NoSQL기반의 비관계형 데이터베이스를 사용하는 것이 더 적합하다.
