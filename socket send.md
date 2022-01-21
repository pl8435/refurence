# socket.send(msg[, offset, length][, port][, address][, callback])

```jsx
msg<Buffer>|<TypedArray>|<DataView>|<string>|<Array> 
Message to be sent.
```

> msg<Buffer>|<TypedArray>|<DataView>|<string>|<Array> 보낼 메시지입니다.
> 

```jsx
offset <integer> Offset in the buffer where the 
message starts.
```

> <정수형> 메시지가 시작되는 버퍼의 오프셋입니다.
> 

```jsx
length <integer> Number of bytes in the message.
```

> <정수형> 메시지의 바이트 수입니다.
> 

```jsx
port <integer> Destination port.
```

> <정수형> 목적지 포트.
> 

```jsx
address <string> Destination host name or IP address.
```

> <string> 대상 호스트 이름 또는 IP 주소.
> 

```jsx
callback <Function> Called when the message has been 
sent.
```

> <Function> 메시지가 전송되었을 때 호출됩니다.
> 

```jsx
Broadcasts a datagram on the socket.
```

> 소켓에서 데이터그램을 브로드캐스트합니다.
> 

```jsx
For connectionless sockets, the destination port 
and address must be specified.
```

> 비연결 소켓의 경우 대상 포트와 주소를 지정해야 합니다.
> 

```jsx
Connected sockets, on the other hand, will use 
their associated remote endpoint, so the port and 
address arguments must not be set.
```

> 반면에 연결된 소켓은 연결된 원격 엔드포인트를 사용하므로 포트 및 주소 인수를 설정하면 안 됩니다.
> 

```jsx
The msg argument contains the message to be sent.
```

> msg 인수는 보낼 메시지를 포함합니다.
> 

```jsx
Depending on its type, different behavior can apply.
```

> 유형에 따라 다른 동작이 적용될 수 있습니다.
> 

```jsx
If msg is a Buffer, any TypedArray or a DataView, 
the offset and length specify the offset within 
the Buffer where the message begins and the number 
of bytes in the message, respectively.
```

> msg의 Buffer가 TypedArray 또는 DataView인 경우 오프셋과 길이는 각각 메시지가 시작되는 버퍼 내의 오프셋과 메시지의 바이트 수를 지정합니다.
> 

```jsx
If msg is a String, then it is automatically 
converted to a Buffer with 'utf8' encoding.
```

> msg가 문자열이면 자동으로 'utf8' 인코딩을 사용하여 버퍼로 변환됩니다.
> 

```jsx
With messages that contain multi-byte characters, 
offset and length will be calculated with respect 
to byte length and not the character position.
```

> 다중 바이트 문자가 포함된 메시지의 경우 오프셋 및 길이는 문자 위치가 아니라 바이트 길이를 기준으로 계산됩니다.
> 

```jsx
If msg is an array, offset and length must not be 
specified.
```

> msg가 배열인 경우 오프셋과 길이를 지정하지 않아야 합니다.
> 

```jsx
The address argument is a string.
```

> 주소 인수는 문자열입니다.
> 

```jsx
If the value of address is a host name, DNS will 
be used to resolve the address of the host.
```

> 주소 값이 호스트 이름이면 DNS를 사용하여 호스트 주소를 확인합니다.
> 

```jsx
If address is not provided or otherwise nullish, 
'127.0.0.1' (for udp4 sockets) or '::1' (for udp6 
sockets) will be used by default.
```

> 주소가 제공되지 않거나 null인 경우 기본적으로 '127.0.0.1'(udp4 소켓용) 또는 '::1'(udp6 소켓용)이 사용됩니다.
> 

```jsx
If the socket has not been previously bound with 
a call to bind, the socket is assigned a random 
port number and is bound to the "all interfaces" 
address ('0.0.0.0' for udp4 sockets, '::0' for udp6 
sockets.)
```

> 소켓이 이전에 bind 호출로 바인딩되지 않은 경우 소켓에 임의의 포트 번호가 할당되고 "모든 인터페이스" 주소(udp4 소켓의 경우 '0.0.0.0', udp6 소켓의 경우 '::0')에 바인딩됩니다.
> 

```jsx
브로드캐스트: 송신 호스트가 전송한 데이터가 네트워크에
연결된 모든 호스트에 전송되는 방식을 의미
```