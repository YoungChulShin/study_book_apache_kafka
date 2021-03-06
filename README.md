### 저장소 설명
- 사내 카프카 스터디를 진행하면서 실습 정보를 기록하기 위한 저장소
- 책 이름: 카프카, 데이터 플랫폼의 최강자

### 테스트 환경 정보
개발 환경 구성
- 도커를 이용해서 3개의 주키퍼와 3개의 카프카를 구성
- 네트워크는 별도의 'MyNet'이라는 Bridge 네트워크를 추가

주키퍼 정보
- testZookeeper01 : 1
- testZookeeper02 : 2
- testZookeeper03 : 3

주키퍼 지노드
- ycshin-kafka

카프카 정보
- testKafka01 : 1
- testKafka02 : 2
- testKafka03 : 3

토픽
- ycshin-topic


테스트 네트워크
|PC|Description|IP|SSH Port(22)|Zookeeper Port(2181)|Kafka Port(9092)|
|--|-----------|--|----|-|-|
|testZookeeper01||172.19.0.100|2090|3000||
|testZookeeper02||172.19.0.101|2091|3001||
|testZookeeper03||172.19.0.102|2092|3002||
|testKafka01||172.19.0.103|2093||3003|
|testKafka02||172.19.0.104|2094||3003|
|testKafka03||172.19.0.105|2095||3003|

카프카 서버 설정 정보
- zookeeper.connect=testZookeeper01:2181,testZookeeper02:2181,testZookeeper03:2181/test-kafka

토픽 생성
- ./kafka-topics.sh --zookeeper testZookeeper01:2181,testZookeeper02:2181,testZookeeper03:2181/test-kafka --replication-factor 1 --partitions 1 --topic test-topic --create


### 기타 참고 도커 명령어
도커 네트워크 확인 
~~~bash
docker network inspect bridge
~~~

도커 배쉬 접속
~~~bash
docker exec -it 컨테이너명 bash
~~~

신규 컨테이너 생성
~~~bash
docker container run -it --privileged=true -v /sys/fs/cgroup:/sys/fs/cgroup:ro --name testZookeeper01 -p 2090:22 --network mynet --ip 172.19.0.100  centos:latest /sbin/init
~~~

### 기타 참고 주키퍼 명령어
CLI 접속
~~~bash
/usr/local/zookeeper/bin/zkCli.sh
~~~

브로커 정보 확인
~~~bash
ls /ycshin-kafka/brokers/ids
~~~

### 기타 참고 카프카 명령어
카프카 로그 확인
~~~bash
cat /usr/local/kafka/logs/server.log
~~~