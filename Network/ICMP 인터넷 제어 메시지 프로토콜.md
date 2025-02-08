<details>
  <summary>ICMP(Internet Control Message Protocol)란 무엇이며, 주요 역할은 무엇인가요?</summary>
  
ICMP(Internet Control Message Protocol)는 **네트워크 계층에서 오류 보고 및 진단 기능을 수행하는 프로토콜**입니다.  
일반적으로 라우터와 호스트 간에 네트워크 상태를 알리는 데 사용됩니다.

### 📌 **주요 역할**
1. **네트워크 오류 보고**  
   - 목적지 도달 불가(Destination Unreachable)  
   - TTL 초과(Time Exceeded)  
   - 포트 도달 불가(Port Unreachable)  

2. **네트워크 진단 및 관리**  
   - `ping` 명령어에서 사용되는 **Echo Request(8) / Echo Reply(0) 메시지**  
   - `traceroute`에서 사용되는 **Time Exceeded(11) 메시지**  

3. **IPv6 확장 기능(ICMPv6)**  
   - **Packet Too Big**: IPv6에서는 패킷 분할을 지원하지 않기 때문에, MTU보다 큰 패킷 전송 시 이 메시지를 반환  
   - **Neighbor Discovery**: ARP를 대체하는 IPv6 주소 확인 기능  

ICMP는 IP 패킷 내에서 전송되며, **TCP/UDP와 같은 IP 페이로드로 포함**됩니다.
</details>

<details>
  <summary>ping과 traceroute 명령어의 차이점은 무엇인가요?</summary>

- **ping**  
  - 네트워크 연결 상태를 확인하는 명령어  
  - **ICMP Echo Request(8) / Echo Reply(0) 메시지를 사용**  
  - RTT(Round Trip Time)를 측정하여 네트워크 응답 속도를 분석  

- **traceroute**  
  - 네트워크 패킷이 목적지까지 가는 **경로(라우터 정보)를 추적**하는 명령어  
  - UDP 패킷의 TTL(Time To Live)을 조절하여 **각 라우터가 TTL 초과 시 ICMP Time Exceeded(11) 메시지를 반환**하도록 함  
  - 목적지 도달 시 ICMP Destination Unreachable(3, 3) 메시지를 반환  

**즉, `ping`은 네트워크 연결 유무를 확인, `traceroute`는 네트워크 경로를 분석하는 도구입니다.**

---
</details>

<details>
  <summary>ICMPv6은 기존 IPv4의 ICMP와 어떤 차이점이 있나요?</summary>

ICMPv6(RFC 4443)은 **IPv6 환경에서 기존 ICMP 기능을 개선하고 추가 기능을 제공**합니다.

### 🆕 **ICMPv6의 주요 차이점**
1. **Packet Too Big 메시지 추가**  
   - IPv6에서는 IP 패킷 분할(Fragmentation)이 없으므로,  
     패킷이 너무 클 경우 **"Packet Too Big"** 메시지를 반환하여 MTU 정보를 제공  

2. **Neighbor Discovery (ND) 지원**  
   - ARP(Address Resolution Protocol)를 대체하는 기능  
   - IPv6 주소를 MAC 주소로 매핑  

3. **Router Solicitation & Advertisement 추가**  
   - 호스트가 동적으로 라우터 정보를 획득 가능  
   - DHCP 없이 자동으로 네트워크 설정  

IPv6 환경에서는 ICMPv6가 **네트워크 설정, 주소 확인 및 패킷 오류 보고까지 수행**합니다.

</details>
