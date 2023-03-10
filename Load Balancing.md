## 로드밸런싱 (Load Balancing)
- 서버가 처리해야 할 업무 혹은 요청(Load)을 여러 대의 서버로 나누어(Balancing) 처리하는 것을 의미 (분산 처리)
- 한 대의 서버로 부하가 집중되지 않도록 트래픽을 관리해 각각의 서버가 최적의 퍼포먼스를 보일 수 있도록 하는 것이 목적

## 동작 원리
Bridge/Transparent Mode에서는 사용자가 서버에 서비스를 요청할 때 중간에서 로드밸런서가 NAT를 통해 IP/MAC주소를 변조한다. 즉, 요청과 응답이 모두 Load Balancer를 경유한다.

```NAT (Network Address Translation – 네트워크 주소 변환): 사설Ip주소를 공인IP 주소로 변경하는 기술```

## 로드밸런서 (Load Balancer)
### 정의
로드밸런싱 기술을 제공하는 서비스 또는 장치
클라이언트와 네트워크 트래픽이 집중되는 서버들 또는 네트워크 허브 사이에 위치한다.

### 종류
### L4 Load Balancing (전송 계층)
- IP주소나 포트번호, MAC주소 등에 따라 트래픽을 나누고 분산처리가 가능
- CLB(Connection Load Balancer) 혹은 SLB(Session Load Balancer)라고 부르기도 한다.

### L7 Load Balancing (애플리케이션 계층)
- OSI 7계층의 프로토콜(HTTP, SMTP, FTP 등)을 바탕으로도 분산 처리가 가능

## 알고리즘 (Algorithm)
### 라운드로빈 방식(Round Robin Method)
- 서버에 들어온 요청을 순서대로 돌아가며 배정하는 방식
- 클라이언트의 요청을 순서대로 분배하기 때문에 여러 대의 서버가 동일한 스펙을 갖고 있고, 서버와의 연결(세션)이 오래 지속되지 않는 경우에 활용하기 적합

### 가중 라운드로빈 방식(Weighted Round Robin Method)
각각의 서버마다 가중치를 매기고 가중치가 높은 서버에 클라이언트 요청을 우선적으로 배분한다. 주로 서버의 트래픽 처리 능력이 상이한 경우 사용되는 부하 분산 방식이다. 예를 들어 A라는 서버가 5라는 가중치를 갖고 B라는 서버가 2라는 가중치를 갖는다면, 로드 밸런서는 라운드로빈 방식으로 A 서버에 5개 B 서버에 2개의 요청을 전달한다.

### IP 해시 방식(IP Hash Method)
클라이언트의 IP 주소를 특정 서버로 매핑하여 요청을 처리하는 방식이다. 사용자의 IP를 해싱해(Hashing, 임의의 길이를 지닌 데이터를 고정된 길이의 데이터로 매핑하는 것, 또는 그러한 함수) 로드를 분배하기 때문에 사용자가 항상 동일한 서버로 연결되는 것을 보장한다.

### 최소 연결 방식(Least Connection Method)
요청이 들어온 시점에 가장 적은 연결상태를 보이는 서버에 우선적으로 트래픽을 배분한다. 자주 세션이 길어지거나, 서버에 분배된 트래픽들이 일정하지 않은 경우에 적합한 방식이다.

### 최소 응답 시간 방식(Least Response Time Method)
서버의 현재 연결 상태와 응답 시간(Response Time, 서버에 요청을 보내고 최초 응답을 받을 때까지 소요되는 시간)을 모두 고려하여 트래픽을 배분한다. 가장 적은 연결 상태와 가장 짧은 응답 시간을 보이는 서버에 우선적으로 로드를 배분하는 방식이다.
