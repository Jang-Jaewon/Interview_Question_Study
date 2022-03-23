# Database

- [noSQL과 RDBMS 장단점, 차이는 무엇인가요?](#%EF%B8%8F-nosql과-rdbms-장단점-차이는-무엇인가요)
- [데이터베이스에서 인덱스를 사용하는 이유와 장단점](#%EF%B8%8F-데이터베이스에서-인덱스를-사용하는-이유와-장단점)
- [ORM을 쓰는 이유와 장점](#%EF%B8%8F-orm을-쓰는-이유와-장점)
- [N+1 문제가 무엇인지](#%EF%B8%8F-n+1-문제가-무엇인지)
- [ORM 최적화란?](#%EF%B8%8F-orm-최적화란?)
- [select_related, prefetch_related의 차이](#%EF%B8%8F-select_relate,-prefetch_related-차이)

<br>

## 💡️ noSQL과 RDBMS 장단점, 차이는 무엇인가요?
>데이터베이스 시스템 중 관계형 데이터베이스를 RDBMS라 부르고, 대표적인 관계형 RDBMS는 Oracle, mysql 등이 있다. RDBMS는 데이터베이스 중 가장 역사가 오래되고 많이 사용되어 지고 있다. RDBMS의 장점은 신뢰성이 높고, 데이터 분류, 정렬, 탐색 속도가 빠르다. NoSQL은 Not Only SQL의 약자로, 관계형 데이터 베이스(RDBMS)의 한계를 극복하기 위한 새로운 형태의 DBMS이다. NoSQL은 고정된 스키마 및 JOIN이 존재하지 않고 분산처리가 비교적 쉽기 때문에 최근 빅데이터 분야에서 주목받고 있다. 


### 추가적인 내용 기술 
- RDBMS는 데이터를 저장하기 위해서 컬럼을 기준으로 데이터를 삽입하기 때문에 새로운 데이터를 담을 필드가 발생하게 되면 스키마를 수정해야한다.
- NoSQL의 경우는 정해진 규격(schema, table-clumn)이 없이도 데이터 저장이 가능하다는 장점이 있다. 
- 이에 저장된 데이터베이스를 주로 읽기(read)만 할 경우 RDBMS로 충분하지만, 쓰기(write) 작업이 많은 경우 RDBMS는 성능 저하 또는 불안정한 모습을 보일 수 있다. 


<br>

## 💡 데이터베이스에서 인덱스를 사용하는 이유와 장단점
> 인덱스는 데이터를 논리적으로 정렬해서 테이블에 대한 검색과 정렬 속도를 높이기 위해 사용한다. 단, 데이터 삽입, 변경이 수시로 일어나면 매번 인덱스를 변경해야하기 때문에 성능 저하를 막기 위한 고려가 필요하다.


### 추가적인 내용 기술
- 인덱스의 장점은 데이터들이 정렬된 형태를 갖기 때문에 테이블을 검색하는 속도와 성능이 향상된다. 또 그에 따라 시스템의 전반적인 부하를 줄일 수 있다. 
- 만약 index를 사용하지 않고 조회해야 하는 경우, 전체를 탐색하는 Full Scan을 수행해야 한다. Full Scan은 전체를 비교하여 탐색하기 때문에 처리 속도가 떨어진다.
- 인덱스 사용의 단점으로는 항상 정렬된 상태로 유지해야 하기 때문에 인덱스가 적용된 컬럼에 삽입(INSERT), 삭제(DELETE), 수정(UPDATE) 빈번히 일어나면 성능 저하가 발생될 수 있다.
- 삽입은 새로운 데이터에 대한 인덱스를 추가하는 작업이 필요하고, 수정은 기존의 인덱스를 사용하지 않음 처리 후 갱신된 데이터에 대한 인덱스 추가하는 작업이 필요하다.
- 삭제는 데이터의 인덱스를 제거하는 것이 아니라 '사용하지 않음'으로 처리하고 남겨두기 때문에 수정 작업이 많은 경우 실제 데이터에 비해 인덱스가 과도하게 커지는 문제점이 발생할 수 있다. 별도의 메모리 공간에 저장되기 때문에 추가 저장 공간이 많이 필요하게 된다. 
- 또한 인덱스를 사용하게 되면, 인덱스를 관리하기 위해 DB의 약 10%에 해당하는 저장공간이 필요하다.
- 이에 규모가 작지 않은 테이블, INSERT, UPDATE, DELETE가 자주 발생하지 않는 컬럼, JOIN이나 WHERE 또는 ORDER BY에 자주 사용되는 컬럼, 데이터의 중복도가 낮은 컬럼에서 인덱스를 사용하는 것이 좋다.
- 인덱스를 사용하는 것 만큼이나 생성된 인덱스를 관리해주는 것도 중요하다. 그렇기 때문에 사용하지 않는 인덱스는 바로 제거를 해주어야 한다. 

<br>

## 💡 ORM을 쓰는 이유와 장점
> ORM은 Object Relational Mapping의 약자로, Database의 Data와 Class로 생성된 객체들을 매핑함으로써 Database를 더 쉽게 제어할 수 있도록 도와준다. 이에 SQL 대신 ORM을 사용하면, 선언문, 할당, 종료 같은 부수적인 코드가 줄어들이 때문에 가독성이 높고, 객체지향적인 코드로 인해 더 직관적이기 때문에 비지니스 로직 자체에 집중할 수 있어 생산성이 증가한다. 또한 ORM을 사용하면, DBMS에 대한 종속성이 줄어들기 때문에 재사용 및 유지보수에 용이합니다.


### 추가적인 내용 기술
- ORM은 Object Relational Mapping 즉, 객체-관계 매핑의 줄임말이다. 객체-관계 매핑이란 OOP를 통해 구현한 클래스와 RDBMS의 테이블과 데이터를 자동으로 매핑하는 것을 의미한다. 
- ORM을 사용하면 SQL문이 아닌 클래스의 메서드를 통해 DB에 간접적으로 접근하고 제어할 수 있어, 객체 모델만 이용해서 프로그래밍이 가능하다.
- 또한 SQL문은 절차적/순차적 접근이 혼재되어있지만, ORM은 객체지향적 접근만 고려하면 되기 때문에 생산성이 증가된다.
- 특히, SQL문에 선언문, 할당, 종료 같은 부수적인 코드로 문법이 장황하고 복잡한데 비해, ORM은 가독성이 높아 편리하고 유지보수에 용이하다.
- 뿐만아니라 해당 Database에 대한 종속성을 낮출 수 있기 때문에 DBMS를 교체하는데 리스크가 적고 RDBMS의 데이터 구조와 객체지향 모델 사이의 간격을 좁힐 수 있다.
- 다만, ORM에도 프로젝트가 커지고, Query가 복잡해질 수록 ORM에 의존하면 속도의 저하가 발생하게 되는 한계가 존재한다. 이에 일부 사용되는 대형 Qeury는 속도를 위해 별도의 SQL문을 작성하기도 한다.

<br>

## 💡️ N+1 문제가 무엇인지

### 추가적인 내용 기술
- N+1문제란 ORM을 쓰는 프레임워크에서 Lazy-Loading의 특성으로 인해 다른 테이블의 필드를 외래키로 참조해서 Data를 가져올 때 발생한다.
- Publish와 Book 테이블이 있고, Book 테이블의 user 필드가 Publish 테이블을 정참조하고 있다고 가정해 보자.
```python
# Publish 테이블
class Publish(TimeStampModel):
    name               = models.CharField(max_length=30)
# Book 테이블    
class Board(TimeStampModel):
    name               = models.CharField(max_length=100)
    description        = models.TextField()
    publisher          = models.ForeignKey('Publish', on_delete=models.CASCADE)
```

- Book에 대한 목록을 반환하는 API를 만든다고 가정 할 때, get 매서드는 아래와 같은 로직을 가진다.
```python
class BookListView(View):
    def get(self, request):
        result = []
        queryset = Book.objects.all()
        for book in queryset:
            books.append({
                'id':book.id,
                'name':book.name,
                'publish':book.publisher.name, # 참조하는 테이블에 접근할 때, 이미 캐싱되있지 않아 query 발생(N+1 문제)
            })
        return JsonResponse({"message": result}, status=200)
```

- 하나의 book 객체의 publish 필드를 통해 Publish 테이블로 이동해 name값을 가져오려는 순간 N+1의 문제가 발생된다.
-  여기서 for문이 순회하는 횟수가 N이 되기 때문에 데이터가 많을 수록 엄청난 양의 query가 추가되는 이 현상은 N+1 문제라한다.

<br>

## 💡️ ORM 최적화란?
> ORM 최적화란 Lazy-loading의 특성에 따른  N+1 문제를 해결하는 방법으로 참조되는 테이블을 미리 캐싱해둠으로써 추가적인 query를 예방하는 기술이다. 이는 Database의 부하를 줄여주기 때문에 성능 향상에 있어 필수적이며, Django에서는 select_related prefetch_related 를 통해서 최적화를 할 수 있다.

### 추가적인 내용 기술
- Django뿐 아니라 다른 ORM에서도 Lazy-loading방식을 사용한다. Lazy Loading은 CS 전반의 개념으로 generator의 개념과 유사하다.
- Lazy-loading이란 ORM에서 명령을 실행할 때마다 DB에 접근하여 데이터를 가져오는 것이 아닌 실제 데이터를 불러와야할 때, 즉 Query문이 평가되어야하는 시점에 Query문을 실행하여 DB에 데이터를 가져오는 방식이다.
- 문제는 다른 테이블을 정참조하거나 역참조하면서 데이터를 불러올 때, 위에서 설명한 N+1 문제가 발생해서 수많은 Query가 일으킨다.
- 이에 미리 Query를 캐싱해둠으로써 DB에 불필요한 query를 발생시키지 않는 방법인 EagerLoading을 사용하여 ORM 최적화가 가능하다.
- ORM을 최적화를 하는 이유는 비용 감소와 서비스의 질을 높히기 위해서 데이터를 빠르게 가져와야하기 때문이다.
- 모든 병목은 DB에서 발생하고, 서비스를 많은 이용자가 사용할 수록 데이터를 가져오는 속도에 서비스의 질이 큰 영향을 미치기 때문에 ORM 최적화는 필수이다.

<br>

## 💡️ select_related, prefetch_related의 차이
> ORM에서 N+1 문제를 해결하기 위해 사용하는 기법을 즉시 호출(EagerLoading)라 하는데, 지금 당장 사용하지 않을 데이터도 포함하여 미리 Query문을 가져오는 방식이다. 정참조 일 때는 select_related, 역참조일 때는 prefetch_related 사용하여 데이터를 미리 캐슁하는 방식으로 N+1 문제를 해결한다. select_related은 참조된 객체들이 정참조 관계를 이룰 때 사용하는데, SQL문에서 INNER JOIN의 방식을 사용한다. prefetch_related는 역참조 일 때 사용하는데, SQL문에서는 LEFT OUTER JOIN 방식을 사용하여 추가 쿼리 셋을 이용해 객체를를 가져온 뒤, 애플리케이션 단에서 모두 합쳐 반환한다. 이 때, prefetch_related는 result_cash란 영역에 데이터를 담기는데, 기존 query를 보내고, 추가로 역참조에 대한 prefetch_related를 보내 이를 최종적으로 합쳐주기 때문에 query가 1개 더 생기는 특징을 갖고 있다.

### 추가적인 내용 기술
- 각 각의 쿼리셋은 DB에 접근 할 때 캐시 메모리를 포함하고 있습니다. 최초 DB에 QuerySet이 요청될 때, 캐시가 비었기 때문에 Query가 발생하지만, 이후 동일한 QuerySet이 요청될 경우 추가적인 요청 없이 캐시에서 꺼내서 사용한다.
- select_related 와 prefetch_related는 모두 QuerySet을 DB에 요청할 때, 미리 참조하는 객체들 까지 불러오는 함수이다. 
- 이렇게 미리 가져온 객체들은 모두 캐쉬에 남아있게 되므로 매번 DB에 접근하는 N+1 문제를 해결할 수 있다.
- select_related와 prefetch_related는 DB에 요청되는 Query 수를 줄여, performance를 향상시켜준다는 측면에서는 공통점이 있지만, 그 사용 방식에는 차이점이 있다.
- select_related는 정참조 관계인 테이블의 객체들에 미리 Query를 요청하는 방식이고, prefetch_related는 QuerySet을 반환할 때 foreign-key, OneTonOneFeild 관계뿐만 아니라 ManyToMany, ManyToOne 관계의 모델들까지 가져오는 방식이다.
- 또한 select_related 는 INNER JOIN 으로 쿼리셋을 가져오고, prefetch_related 는 LEFT OUTER JOIN 방식을 사용하여 모델 별로 쿼리를 실행해 최종 쿼리셋을 합쳐 가져오는 방식이다. 이에 prefetch_related는 1개의 추가 Query가 발생된다.
- 또한 일반적으로 정참조에서는 select_related, 역참조에서는 prefetch_related를 사용합니다.

<br>
