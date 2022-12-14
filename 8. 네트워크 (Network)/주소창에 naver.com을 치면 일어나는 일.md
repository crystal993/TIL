주소창에 naver.com을 치면 일어나는 일 

## 요약 

1. 브라우저 주소창에 naver.com을 입력한다.
2. 브라우저가 naver.com의 IP 주소를 찾기 위해 캐시에서 DNS 기록을 확인한다.
3. 만약 요청한 URL(naver.com)이 캐시에 없다면, ISP의 DNS 서버가 DNS 쿼리로 naver.com을 호스팅하는 서버의 IP 주소를 찾는다.
4. 브라우저가 해당 서버와 TCP 연결을 시작한다.
5. 브라우저가 웹서버에 HTTP 요청을 보낸다.
6. 서버가 요청을 처리하고 응답을 보낸다.
7. 서버가 HTTP 응답을 보낸다.
8. 브라우저가 HTML 컨텐츠를 보여준다.


# IP 주소 

- IP 주소란 많은 컴퓨터들이 인터넷 상에서 서로를 인식하기 위해 지정받은 식별용 번호라고 생각하면 된다. 
- 현재는 IPv4 버전 (32비트)로 구성되어 있으며, 한번씩은 들어봤을 법한 127.0.0.1 같은 주소를 말한다. 
- 시간이 갈수록 IPv4 주소의 부족으로 IPv6이 생겼는데, 128비트로 구성되어 있기 때문에 IP주소가 부족하지 않다는 특징이 있다. 

# 도메인 네임(Domain Name)

- IP주소는 12자리의 숫자로 되어있기 때문에 사람이 외우기 힘들다는 단점이 있다. 
- 12자리의 IP 주소를 'naver.com'처럼 문자로 표현한 주소를 도메인 네임이라고 한다. 
- 도메인 네임은 사람의 편의성을 위해 만든 주소이므로 
  실제로는 컴퓨터가 이해할 수 있는 IP 주소로 변환하는 작업이 필요하다.
- 이때, 미리 도메인 네임과 함께 해당하는 IP 주소값을 한 쌍으로 저장하고 있는
  데이터베이스를 DNS(Domain Name System) 이라고 부른다. 
- 도메인 네임으로 입력하면 DNS를 이용해 컴퓨터는 IP 주소를 받아 찾아갈 수 있다. 

# 작동 방식 

![image](https://user-images.githubusercontent.com/72599761/210160134-d417e2b2-cb9b-4eb3-8c52-18c9a761b327.png)

1. 사용자가 브라우저에 도메인 네임 (www.naver.com)을 입력한다. 
2. 사용자가 입력한 url 주소 중에서 도메인 네임(Domain Name) 부분을 DNS 서버에서 검색하고, 
   DNS 서버에서 해당 도메인 네임에 해당하는 IP 주소를 찾아 사용자가 입력한 url 정보와 함께 전달한다. 
3. 페이지 url 정보와 전달받은 ip 주소는 HTTP 프로토콜을 사용하여 HTTP 요청 메세지를 생성하고, 
   이렇게 생성된 HTTP 요청 메세지는 TCP 프로토콜을 사용하여 인터넷을 거쳐 해당 IP 주소의 컴퓨터로 전송된다. 
4. 이렇게 도착한 HTTP 요청 메세지는 HTTP 프로토콜을 사용하여 웹 페이지 URL 정보로 변환되어 
   웹 페이지 URL 정보에 해당되는 데이터를 검색한다. 
5. 검색된 웹 페이지 데이터는 또 다시 HTTML 프로토콜을 사용하여 HTTP 응답 메시지를 생성하고 
   TCP 프로토콜을 사용하여 인터넷을 거쳐 원래 컴퓨터로 전송된다. 
6. 도착한 HTTP 응답 메시지는 HTTP 프로토콜을 사용하여 웹 페이지 데이터로 변환되어 
   웹 브라우저에 의해 출력되어 사용자가 볼 수 있게 된다. 
   
   
   
 ### 참고 
 https://github.com/WooVictory/Ready-For-Tech-Interview/blob/master/Network/%EC%A3%BC%EC%86%8C%EC%B0%BD%EC%97%90%20naver.com%EC%9D%84%20%EC%B9%98%EB%A9%B4%20%EC%9D%BC%EC%96%B4%EB%82%98%EB%8A%94%20%EC%9D%BC.md
 https://velog.io/@khy226/%EB%B8%8C%EB%9D%BC%EC%9A%B0%EC%A0%80%EC%97%90-url%EC%9D%84-%EC%9E%85%EB%A0%A5%ED%95%98%EB%A9%B4-%EC%96%B4%EB%96%A4%EC%9D%BC%EC%9D%B4-%EB%B2%8C%EC%96%B4%EC%A7%88%EA%B9%8C
   
