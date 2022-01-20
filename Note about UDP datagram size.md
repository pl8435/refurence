# Note about UDP datagram size

```jsx
The maximum size of an IPv4/v6 datagram depends 
on the MTU (Maximum Transmission Unit) and on the 
Payload Length field size.
```

> IPv4/v6 데이터그램의 최대 크기는 MTU(최대 전송 단위) 및 페이로드 길이 필드 크기에 따라 다릅니다.
> 

```jsx
The Payload Length field is 16 bits wide,
```

> 페이로드 길이 필드의 너비는 16비트입니다.
> 

```jsx
which means that a normal payload cannot exceed 
64K octets including the internet header and data 
(65,507 bytes = 65,535 − 8 bytes UDP header − 
20 bytes IP header);
```

> 일반 페이로드는 인터넷 헤더 및 데이터를 포함하여 64K 옥텟을 초과할 수 없습니다(65,507바이트 = 65,535 - 8바이트 UDP 헤더 - 20바이트 IP 헤더).페이로드 길이 필드의 너비는 16비트입니다.
> 

```jsx
this is generally true for loopback interfaces, 
but such long datagram messages are impractical 
for most hosts and networks.
```

> 이것은 일반적으로 루프백 인터페이스에 해당되지만 이러한 긴 데이터그램 메시지는 대부분의 호스트 및 네트워크에서 비실용적입니다.
> 

```jsx
The MTU is the largest size a given link layer 
technology can support for datagram messages.
```

> MTU는 주어진 링크 계층 기술이 데이터그램 메시지를 지원할 수 있는 가장 큰 크기입니다.
> 

```jsx
For any link, IPv4 mandates a minimum MTU of 68 
octets, while the recommended MTU for IPv4 is 576 
(typically recommended as the MTU for dial-up type 
applications), whether they arrive whole or in fragments.
```

> 모든 링크에 대해 IPv4는 68옥텟의 최소 MTU를 요구하지만 IPv4에 권장되는 MTU는 576(일반적으로 전화 접속 유형 응용 프로그램의 경우 MTU로 권장됨)입니다. (그들이 전체 또는 조각으로 도착하는지 여부.)
> 

```jsx
For IPv6, the minimum MTU is 1280 octets. However, 
the mandatory minimum fragment reassembly buffer size is 
1500 octets.
```

> IPv6의 경우 최소 MTU는 1280옥텟입니다. 그러나 필수 최소 조각 리어셈블리 버퍼 크기는 1500옥텟입니다.
> 

```jsx
The value of 68 octets is very small, since most current 
link layer technologies, like Ethernet, have a minimum 
MTU of 1500.
```

> 이더넷과 같은 대부분의 최신 링크 계층 기술은 최소 MTU가 1500이기 때문에 68옥텟의 값은 매우 작습니다.
> 

```jsx
It is impossible to know in advance the MTU of each link 
through which a packet might travel.
```

> 패킷이 이동할 수 있는 각 링크의 MTU를 미리 아는 것은 불가능합니다.
> 

```jsx
Sending a datagram greater than the receiver MTU will 
not work because the packet will get silently dropped 
without informing the source that the data did not reach 
its intended recipient.
```

> 수신자 MTU보다 큰 데이터그램을 보내면 데이터가 의도한 수신자에게 도달하지 않았다는 사실을 소스에 알리지 않고 패킷이 자동으로 삭제되기 때문에 작동하지 않습니다.
> 

```jsx
데이터그램: 발신지와 수신지 컴퓨터 사이에서 데이터 교환과 
관계없이 독립적인 전송 정보 데이터이다. 패킷이라는 용어로 
대체할 수 있다.

페이로드:　사용에 있어서 전송되는 데이터, 전송의 근본적인 
목적이 되는 데이터의 일부분으로 그 데이터와 함께 전송되는 
헤더와 메타데이터와 같은 데이터는 제외

헤더: 저장되거나 전송되는 데이터 블록의 맨앞에 위치한 보충 
데이터

메타데이터: 어떤 목적을 가지고 만들어진 데이터

필드: 클래스를 구성하는 요소 중 하나로 클래스 내부 멤버

옥텟: 컴퓨팅에서 8개의 비트가 한데 모인 것

루프백 인터페이스: 물리적으로 연결하는 Port가 존재하지 않는
논리적인 Port, Test 등을 목적으로 네트워크를 추가 시 사용
할 수 있는 Interface

MTU: TCP/IP 네트웍 등과 같이 패킷 또는 프레임 기반의 
네트웍에서 전송될 수 있는 최대크기의 패킷 또는 프레임을 
가리키며, 대개 옥텟을 단위로 사용

이더넷: 컴퓨터 네트워크 기술의 하나로, 일반적으로 LAN, MAN 
및 WAN에서 가장 많이 활용되는 기술 규격
```