### 용어 정리

- blocklever striping
	- striping
		- 데이터를 여러 디스크에 분산하여 저장하는 것을 의미한다. 
		- 하나의 디스크에 담을 수 없는 용량의 데이터를 여러개의 디스크에 담기 위함이다.
		- 즉, 보다 큰 용량을 구성하려는 목적을 가진 레이드의 핵심이다.
	- block level striping
		- 파일의 블록들이 여러 디스크에 분산되는 것을 의미한다.
		- 한 개의 블록에 접근하는 여러개의 서로 다른 요청을 각 디스크에 의해 병렬로 처리한다.
		- 따라서 I/O 요청의 대기 시간이 감소한다.

- query plan
	- 사용자가 요청한 SQL을 DBMS가 어떤 실행 절차로 처리하는지에 대한 계획이다.
	- 튜너는 query plan을 확인하고 성능 문제를 진단, 개선한다.

- deadlock prevention
	- 교착 상태 발생을 방지하는 프로토콜을 의미한다.
	- 상호배제 조건의 제거
		- deadlock은 두 개 이상의 프로세스가 공유 불가능한 자원을 사용하여 발생한다.
		- 따라서 공유 불가능한, 즉사 상호 배제 조건을 제거하면 해결할 수 있다.
	- 점유와 대기 조건의 제거
		- 한 프로세스에 수행되기 전에 모든 자원을 할당시키고 나서 점유하지 않을 때에는 다른 프로세스가 자원을 요구하도록 한다.
		- 자원 과다 사용으로 인한 효율성, 프로세스가 요구하는 자원을 파악하는 데에 대한 비용, 기아상태, 무한 대기 등의 문제점이 있다.
	- 비선점 조건의 제거
		- 비선점 프로세스에 대해 선점 가능한 프로토콜을 만들어 준다.
	- 환형 대기 조건의 제거
		- 자원 유형에 따라 순서를 매긴다.

- primary index
	- 해당 레코드를 대표하는 컬럼 값으로 만들어진 인덱스
	- 테이블에서 해당 레코드를 식별할 수 있는 기준값이 된다.
	- NULL값이나 중복이 허용되지 않는다.
	- 대부분의 관계형 DB에서는 자동으로 기본키에 대한 인덱스를 생성한다.
	- 두개의 필드로 구성된 고정 길이 레코드들의 순서파일
		- 첫번째 필드 : 순서키 필드와 동일한 타입
		- 두번째 필드 : 디스크 블록에 대한 포인터 저장

- full table scan
	- DB 테이블에 포함된 데이터를 첨부터 끝까지 체크하며 원하는 데이터를 추출하는 것을 의미한다.
	- 데이터 사이즈가 커질수록 지양해야 한다.

- schedule
	- 트랜잭션들의 연산들이 실행되는 순서를 의미한다.
	- 데이터베이스와 트랜잭션 처리 시스템의 일정 분야에서 시간별로 실행하는 작업 명령 목록을 뜻한다.
	- 동시에 여러개의 transaction들이 병행 실행되는 경우에는, 연산들이 실행되는 순서와 원래 트랜잭션 안에 있는 명령어의 순서가 유지되어야 한다.

- serializable
	- n개의 트랜잭션들에 대한 병행스케쥴 S가 동일한 n개의 트랜잭션에 대한 직렬스케쥴 S'와 동등하다면, 스케쥴 S는 serializable이라고 한다.
	- 병행스케쥴 S가 serializable하다면, S는 갱신 분실, 불일치성, 연쇄 복구 문제등이 발생하지 않는 스케쥴을 의미한다.
	- 대부분의 DBMS는 모든 트랜젝션들이 특정 규약을 준수한다면, 그 ㅌ랜잭션이 참요하고 있는 병행 스케쥴이 serializable하다는 것을 보장할 수 있는 동시성 제어 기법을 사용한다.

- cascadeless schedule
	- 한 트랜잭션에 문제가 발생해 롤백했을 때, 다른 트랜잭션들도 영향을 받아 롤백되는 것을 cascading rollback이라고 한다. 
	- 시간이 오래 걸린다.
	- 스케쥴 안의 모든 트랜잭션이 오직 완료된 트랜잭션들이 갱신한 항목만 읽는다면 cascadeless schedule이라고 한다.
	- 이 경우에는 cascading rollback이 일어나지 않는다.

- 2phase locking
	- 트랜잭션이 root부터 원하는 node까지의 경로를 따라가며 그 노드의 후손들 중 하나에 어떤 형태의 lock을 걸 것인가를 나타내는 것이다.
	- IS(shared-lock 요구)
	- IX(exclusive -lock 요구)
	- ISX(현재 노드가 shared-lock, 후손 노드에게 exclusive-lock 요구) 세 가지가 있다.

### 분산 데이터베이스

- 분산 데이터베이스란?
	- 하나의 DBMS가 여러 CPU에 연결된 저장장치를 제어하는 형태의 DB

- 분산 데이터 저장을 위한 중복과 분할
	- 중복
		- 보다 빠른 검색과 고장에 대비해 여러 사이트에 저장된 데이터의 여러 사본을 유지하는 것
		- 가용성이 높고 질의를 병렬로 처리할 수 있다.
	- 분할
		- 릴레이션을 여러 단편으로 분할하여 서로 다른 사이트에 저장하는 것
		- 샤딩, 파이셔닝과 같은 말
		- 어떻게 분할하는지가 중요한 이슈
	- 중복과 분할을 한다고 하는 것은 릴레이션이 여러 단편으로 분할되어 시스템은 각 단편의 동일한 여러 사본을 유지하는 것을 뜻함

- 데이터 중복의 장/단점
	- 장점
		- 가용성 : 한 릴레이션을 가지는 사이트에 장애가 생겨도 그 릴레이션을 사용할 수 있다.
		- 병렬화 : r 상의 질의가 여러 노트에서 병렬로 처리가 가능하다. 따라서 요청이 많다면 빠르게 처리할 수 있다.
		- 데이터 전송의 감소 : r의 사본을 가지는 각 사이트에서 릴레이션 r이 데이터 교환 없이 지역적으로 사용이 가능해진다.
	- 단점
		- 갱신 비용의 증가 : 릴레이션 r이 갱신 될 때마다 릴레이션 r의 사본들이 모두 갱신되어야 한다.
		- 동시성 제어의 복잡성 증가 : 특수한 동시성 제어 기법이 수행되지 않으면 서로 다른 사본들의 동시 갱신이 일어나지 않아 데이터가 일치하지 않을 수 있다.

### 물리적 데이터베이스 저장 구조
- RAID가 Reliability와 Performance를 향상시키는 접근 방법
	- RAID란?
		- 복수 배열 독립 디스크 (Redundant Array of Independent/Inexpensive Disks)
		- 여러개의 하드 디스크에 일부 중복된 데이터를 나눠서 저장하는 기술이다.
		- 데이터를 나누는 다양한 방법이 존재한다. 그 방법을 "레벨"이라고 부른다.
		- 레벨에 따라 저장장치의 신뢰성을 높이거나, 전체적인 성능을 향상시키는 등의 다양한 목적을 만족시킨다.
		- 최초에는 5가지 레벨이 존재했으나 이후 다른 레벨들이 추가되었다.
	- Redunduncy를 통해 Reliability 향상
		- shading을 통해 두개의 동일한 물리적 디스크에 중복해서 기록한다,
		- 만일 오류가 발생하면 다른 디스크를 사용한다.
		- 디스크 오류 발생 시 손실 정보를 재구축 하는 데 사용할 부가 정보를 저장할 수도 있다.
	- Parallelism을 통해 Performance를 향상
		- RAID는 더 빠른 전송 속도를 제공하기 위해 데이터 스트라이핑 기법을 사용한다.
		- 데이터 스트라이핑 기법이란, 파일의 블록들이 여러 디스크에 분산되는 것을 뜻한다.
		- 블록 레벨 스트라이핑에서는 한 개의 블록에 접근하는 여러개의 서로 다른 요청을 각 디스크에 의해 병렬로 처리한다.
		- 따라서 I/O 요청들의 대기 시간이 감소된다.

- RAID level 0, 1, 5 비교
	- RAID 0
		- ![RAID0](http://static.thegeekstuff.com/wp-content/uploads/2010/07/raid-0.png)
		- 최소 2개의 디스크
		- 용량: 디스크 수 * 디스크 용량 
		- 드라이브 하나가 고장나면 안전장체가 없어서 전체 어레이가 고장나기 때문에 중요한 시스템에서 사용하면 안된다.

	- RAID 1
		- ![RAID1](http://static.thegeekstuff.com/wp-content/uploads/2010/07/raid-1.png)
		- 최소 2개의 디스크
		- 용량 : 디스크 수/2 * 디스크 용량
		- 디스크 미러링이 되어, 스토리지에 저장되는 모든 데이터가 중복된다. 
		- 드라이브 하나가 고장나도 다른 드라이브가 하나 더 있어서 매우 안전하다.

	- RAID 5
		- ![RAID5](http://static.thegeekstuff.com/wp-content/uploads/2010/07/raid-5.png)
		- 최소 3개의 디스크
		- 용량: (디스크 수 - 1) * 디스크 용량 
		- 한개의 드라이브가 고장나는 것은 허용한다.
		- 데이터의 블럭과 parity정보가 모든 디스크에 나뉘어 저장되나, 항상 균등하진 않다. 
		- rebuild가 매우 느리고, parity 정보를 끊임없이 갱신해야 해서 성능이 우수하지는 않다.

- 가변 길이 레코드 저장을 위한 slotted page 구조
	- slotted page 구조
		- 해당 블록에 대한 메타 정보를 header에 가지고 데이터를 관리 하는 것을 의미한다.
		- header에서는 레코드의 수와 각각의 레코드 크기와 위치를 가지고 있다.
		- 또한 header에서는 블록 안의 free space의 끝이 어디인지 저장해 놓는다.
	- dense/sparse index
		- dense index
			- 데이터 파일 내의 모든 레코드에 대한 키-포인터 쌍을 가진 파일
			- 중복키를 가진 클러스터드 인덱스에서, dense index는 그러한 키를 가진 첫번째 레코드를 가리킨다.
		- sparse index
			- 데이터 파일 내의 모든 블록에 대한 키-포인터 쌍을 가진 파일
			- 파일 내의 모든 키는 정렬된 데이터 파일 내의 블록에 연결된 특정 포인터들과 연계되어 있다.
			- 중복된 키를 가진 클러스터드 인덱스에서, sparse index는 각 블록 내의 가장 빈도가 낮은 검색 키를 지시한다.

- 키값이 {7, 14, 30, 10, 15, 18, 6, 20, 9} 의 순서로 추가될 때, B+ tree가 만들어지는 과정 : <그림1 참고>

### 데이터베이스 튜닝과 join 알고리즘

- 복합 인덱스 생성 시 애트리뷰트 순서가 중요한 이유
	- 복합인덱스란?
		- 복수개의 컬럼으로 구성된 인덱스를 의미한다.
		- 각각의 컬럼의 분포도는 나쁘지만, 컬럼 몇개가 결합되면 분포도가 양호해지는 경우에 사용한다.
	- 복합 인덱스는 컬럼의 순소에 따라 access하는 범위가 결정된다.
		- 즉, where 조건절에서 비교연산자 = 상수의 조건이 and의 조건으로 여러개의 컬럼이 열거되어 인덱스 컬럼의 매칭율을 높일수록 Access의 범위는 줄어들어 수행 속도가 빨라진다.
		- 만약, 3개 이상의 컬럼으로 구성되는데 중간 컬럼값이 조건에 없다면 결합 인덱스를 구성하는 첫번째 컬럼의 조건의 범위를 모두 스캔해야 한다. 그러므로 결합인덱스를 생성 할 때의 순서는 매우 중요하다.
- clustered index
	- 지정한 열에 대해 내용 자체가 자동 정렬되어 있다. 한 테이블에 한개만 생성 가능하다. (사전과 비슷하다.)
	- clustered index는 테이블의 데이터가 물리적으로 정렬되어 있기 때문에 부분 범위 처리에 활용하면 적은 I/O를 통해 원하는 데이터를 추출 할 수 있다.
	- non-clustered index는 leaf level 인덱스 페이지에 테이블 데이터의 위치가 저장되어 있기 때문에 테이블 데이터로 직접 access 가능하다.
- block nested loop join 알고리즘의 과정과 worst case IO 비용 
	- R(외부 루프)의 각 블록에 대해 S(내부 루프)의 모든 블록에 대해 검색하고, 두 레코드가 조인 조건 만족하는지 테스트한다.
	- worst case
		- 각 테이블의 한개 블록만 메모리에 수용하는 경우 : br * bs + br
- indexed nexted loop join 알고리즘의 과정과 IO 비용
	- 부합되는 레코드를 검색하기 위해 index를 사용한다.
	- join attribute 두개 중 하나에 인덱스가 존재하면, 다른쪽에 있는 각 레코드에 대해 루프를 돌면서 인덱스가 존재하는 쪽에 있는 레코드들 중에서 조인 조건을 만족하는 레코드가 있는지 검사한다.
	- worst case
		- r테이블의 한개 블록만 메모리에 수용하는 경우, c는 r의 투플과 조인조건을 만족하는 s의 투플을 찾는 비용
		- br + nr * c
- sort merge join 알고리즘의 과정과 IO 비용
	- R과 S의 레코드들이 각각 조인 애트리뷰터 값에 따라 물리적으로 정렬되어 있으면 가장 효율적으로 조인을 구현할 수 있다.
	- 먼저 조인 애트리뷰트 값으로 정렬한다.
	- 그리고 순서에 따라 동시에 스캔하며 조인 조건에 맞는 레코드들을 검색한다.
	- 이 경우, 각 릴레이션의 블록을 한번만 읽으면 된다.
	- I/O 비용 : br + bs
- hash join 알고리즘의 조인 과정과 IO 비용
	- R의 조인 애트리뷰트와 S의 조인 애트리뷰트들에 대해 동일한 해시 함수를 하용하여 조인한다.
	- 먼저 분할 단계에서 한 쪽의 애트리뷰트들을 해시하여 R의 레코드들을 해시 버켓들로 분할한다.
	- 그 다음 조사 단계에서 S에 대해 해시하여 조사할 버켓을 구한다.
	- 그 레코드를 그 버넷에 있는 레코드들과 검사하여 조인 조건에 맞는지 확인한다.
	- 분할 단계에서 각 릴레이션들을 분할하기 위해 1) 읽고, 2) 파티션을 쓰고, 조사단계에서 해싱된 버켓들을 각각 3) 읽는다.
	- I/O 비용 : 3(br + bs)

### 데이터 트랜잭션의 동시성 제어
- 트랜잭션의 개념과 트랜잭션의 state diagram <그림2 참고>
	- 트랜잭션
		- 정확성을 보장하기 위해 완전히 종료해야 하는 데이터데이스 처리의 논리적 단위를 표현하는 개념
		- 대부분의 DBMS에서 데이터의 일관성 및 동시성을 보장하기 위해 트랜젝션을 제공한다.
		- 일률적으로 실행되는 작업이 어떤 원인 때문에 실패하는 경우, 모든 작업이 실패하게 지원한다.
	- 트랜잭션의 ACID
		- 원자성 Atomicity : 하나의 트랜잭션은 하나의 원자성을 가진다. 수행되거나/수행되지 않거나.
		- 일관성 Consistency : 트랜잭션을 완전히 실행하면 데이터베이스를 하나의 일관된 상태에서 또 다른 일관된 상태로 바꿔야 한다.
		- 고립성 Isolation : 하나의 트랜잭션은 다른 트랜잭션들과 독립적이다. 
		- 지속성 Durability : 한 트랜젝션이 데이터베이스를 변경시키고, 그 변경이 완료되면 이후에는 손실되지 않아야 한다.
	- 트랜잭션을 실행하다가 문제가 발생하면 중단될 수 있다.
	- 트랜잭션의 마지막 상태는 commit(완전히 완료된 상태)와 rollback(정상적으로 완료되지 않고 종료되어 트랜잭션 시작 전으로 돌아가는 상태)이 있다.
- 트랜잭션을 동시 수행하여 얻는 장점
	- 프로세스들의 동시 실행은 인터리빙을 이용한다.
	- 인터리빙 형태로 동시에 실행되는 두 프로세스는 실행 프로세스가 디스크로부터 블록을 읽을 때 처럼 입출력 연산을 요구하는 경우에도 중앙 처리장치가 정지하지 않고 계속 어떤 프로세스를 수행할 수 있다.
- conflict equivalent
	- 다른 두 트랜잭션에서 한 자원에 접근하는데, 그 자원에 접근하는 명령어 중 하나라도 wirte작업이 있다면 conflict가 있다.
	- 두 스케쥴에 대해서 한 스케쥴의 conflict가 아닌 instruction의 순서를 바꾸어 다른 쪽의 스케쥴로 변할 수 있다면 conflict equivalent 하다고 한다.
	- 같은 트랜잭션이 포함된 두개의 스케쥴 s1, s2가 존재할 때, 비 충돌 발생 연산의 교환으로 S1, S2로 변환될 수 있을 때 conflict equivalent라고 한다.
- 주어진 스케쥴은 conflict serializable한가? 만족시 해당 serial schedule을 제시하고 아니라면 이유를 제시하시오
	<그림 3> 참고
- recoverable schedule의 조건을 설명하고 주어진 스케쥴이 recoverable schedule인지 검사하시오
	<그림 4> 참고 