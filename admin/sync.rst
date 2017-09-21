.. _sync:

Sync
******************

Sync는 Publish-Subscribe 모델을 통해 복수의 STON을 동일하게 관리할 수 있는 기법이다.

.. figure:: img/pubsub_purge.png
   :align: center

이 모델은 관리자가 URL로 게시(Publish)하고, 각 서버들이 이를 수신(Subscribe)하여 반영하는 구조이다. 
각각의 서버가 능동적으로 목록을 수신하기 때문에 서버 대수가 늘어나면서 발생하는 관리의 어려움이 근본적으로 사라진다.

.. note::

   Sync는 목적에 의해 설정 동기화, 캐싱 동기화(Pre-Caching), Purge 동기화로 분류할 수 있다. 
   본 Prototype에서는 Purge 동기화만을 스케치한다.



설정
====================================

API를 이용한 Purge는 직관적으로 간편하다는 장점이 있는 반면 다음과 같은 단점도 존재한다.

- 대상 서버가 많아지면 일일이 API를 호출하기 번거롭다.
- 클라우드 Auto-Scale 등으로 인해 서버 인스턴스가 지속적으로 변동되면 대상 서버 리스트를 만들기 어렵다.
- 점검등의 이유로 일시적으로 서버가 배제되고 재투입된 경우 해당 시간동안의 Purge가 반영되기 힘들다.

::

   $ server.xml - <Server>
   
   <Sync>
      <Purge Status="Inactive" Timeout="5" Cycle="3">http://example.com/ston_purge_list.html</Purge>
   </Sync>

-  ``<Purge>`` 

   관리자가 Purge할 대상으로 URL로 게시한다. ``Statuc`` 가 ``Active`` 일 때만 활성화된다.

   -  ``Timeout (기본: 5초)`` 소켓연결부터 HTTP Transaction이 완료될 때까지 유효시간

   -  ``Cycle (기본: 3초)`` 게시 URL 접근주기

설정된 URL을 ``Cycle`` 마다 반복하여 접근한다.




응답파일 포맷
====================================

XML 형식을 사용하며 예제는 아래와 같다. ::

   <STON>
      <Meta>
         <Method>Purge</Method>
      </Meta>
      <Body>
         <Url>example.com/logo.jpg</Url>
         <Url>example.com/script/myscript.js</Url>
         <Url>foo.com/*.js</Url>
         <Url>foo.com/dummy/</Url>
         <Url>http://bar.com/private.html?id=*</Url>
      </Body>
   <STON>

-  ``<Method> (기본: Purge)`` 수행할 무효화 명령을 선택한다. 
   ``Purge`` , ``HardPurge`` , ``Expire`` 중 선택한다.

-  ``<Url>`` 무효화할 대상을 지정한다. 가상호스트 이름(FQDN)이 포함된 URL을 사용해야 하며 프로토콜은 생략 가능하다. 
   XML 표현을 사용하기 때문에 URL에 XML escape character( ``" ' < > &`` )가 포함되어 있다면 치환하거나 CDATA로 표현해야 한다.

Content-Type이나 확장자는 별도로 체크하지 않는다.



변경감지
====================================

매번 서버에서 변경목록을 가져와 반영할 경우 지나친 중복 처리가 발생할 수 있다. 
Last-Modified 헤더를 통해 이 문제를 해결한다.

.. figure:: img/xxx.png
   :align: center

게시 URL이 example.com/ston_purge_list.html 라면 STON이 보내는 최초 요청은 다음과 같다. ::

   GET /ston_purge_list.html HTTP/1.1
   Host: example.com

서버는 Lats-Modified 헤더를 반드시 명시해야 한다. ::
      
   HTTP/1.1 200 OK
   Server: Apache/1.3.27
   Content-Length: 288
   Last-Modified: Mon, 24 Jul 2017 01:09:43 GMT

   ... Body ...

STON은 마지막 Last-Modified 헤더 값을 기억하며 다음과 같이 If-Modified-Since 헤더를 이용해 내용이 변경되었을 때만 서버가 응답하길 기대한다. ::

   GET /ston_purge_list.html HTTP/1.1
   Host: example.com
   If-Modified-Since: Mon, 24 Jul 2017 01:09:43 GMT

변경이 있을 경우 앞선 응답처럼 200 OK로 응답하며 Last-Modified 시간이 갱신된다. 
변경이 없는 경우 다음처럼 304 Not Modified 로 응답해야 한다. ::

   HTTP/1.1 304 Not Modified
   Server: Apache/1.3.27



서버구성 TIP
====================================

