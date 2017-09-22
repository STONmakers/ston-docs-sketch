.. _sync:

Sync
******************

API를 이용한 Purge는 직관적으로 간편하다는 장점이 있는 반면 서비스 규모가 커지면서 다소 한계점이 있다.

- 대상 서버가 많아지면 일일이 API를 호출하기 번거롭다.
- 클라우드 Auto-Scale 등으로 인해 서버 인스턴스가 지속적으로 변동되면 대상 서버 리스트를 만들기 어렵다.
- 점검등의 이유로 일시적으로 서버가 배제되고 재투입된 경우 해당 시간동안의 Purge가 반영되기 힘들다.

Sync는 Publish-Subscribe 모델을 통해 복수의 STON을 동일하게 관리할 수 있는 기법이다.

.. figure:: img/xxx.png
   :align: center

이 모델은 관리자가 URL로 게시(Publish)하고, 각 서버들이 이를 수신(Subscribe)하여 반영하는 구조이다. 
각각의 서버가 능동적으로 목록을 수신하기 때문에 서비스 규모가 커지면서 발생하는 대상 지정의 어려움이 근본적으로 사라진다.

.. note::

   Sync는 목적에 의해 설정 동기화, 캐싱 동기화(Pre-Caching), Purge 동기화로 분류할 수 있다. 
   본 Prototype에서는 Purge 동기화만을 대상으로 한정한다.



설정
====================================

Purge목록을 수신(Subscribe)할 수 있는 URL을 설정한다.

::

   $ server.xml - <Server>
   
   <Sync>
      <Purge Status="Inactive" Timeout="5" Cycle="3">http://example.com/purge.html</Purge>
   </Sync>

-  ``<Purge>``

   Purge목록의 게시 URL을 설정한다. ``Status="Active"`` 일 때 활성화된다.

   -  ``Timeout (기본: 5초)`` 소켓연결부터 HTTP Transaction이 완료될 때까지 유효시간

   -  ``Cycle (기본: 3초)`` 게시 URL 접근주기

설정된 서버는 게시 URL을 ``Cycle`` 초 마다 Polling한다.




게시 파일형식
====================================

Purge 목록 게시 서버가 제공해야 하는 파일은 아래와 같이 XML 형식이다. ::

   <STON>
      <Meta>
         <Method>Purge</Method>
      </Meta>
      <Body>
         <Item>example.com/logo.jpg</Item>
         <Item>example.com/script/myscript.js</Item>
         <Item>foo.com/*.js</Item>
         <Item>foo.com/dummy/</Item>
         <Item>http://bar.com/private.html?id=*</Item>
      </Body>
   <STON>

-  ``<Method> (기본: Purge)`` 수행할 무효화 명령을 선택한다.
   ``Purge`` , ``HardPurge`` , ``Expire`` 중 선택한다.

-  ``<Item>`` 무효화할 대상을 지정한다. 
   명시적인 주소(URL), 패턴, 디렉토리 표현이 가능하다. 
   가상호스트 이름이 포함되어야 하며 프로토콜(http://)은 생략 가능하다. 

XML 생성시 ``<Item>`` 에 XML escape character( ``" ' < > &`` )가 포함되어 있다면 예약어로 치환하거나 CDATA로 표현해야 한다.
Content-Type이나 확장자는 별도로 체크하지 않는다.



변경감지
====================================

서버에서 변경목록을 매번 가져와 반영할 경우 지나친 중복 처리가 발생할 수 있다. 
``Last-Modified`` 헤더를 통해 이 문제를 해결한다.

.. figure:: img/xxx.png
   :align: center

게시 URL이 example.com/purge.html 라면 STON이 보내는 최초 요청은 다음과 같다. ::

   GET /purge.html HTTP/1.1
   Host: example.com

서버는 ``Lats-Modified`` 헤더를 반드시 명시해야 한다. ::
      
   HTTP/1.1 200 OK
   Server: Apache/1.3.27
   Content-Length: 288
   Last-Modified: Mon, 24 Jul 2017 01:09:43 GMT

   ... Body ...

STON은 마지막 ``Last-Modified`` 헤더 값을 기억하며 다음과 같이 ``If-Modified-Since`` 헤더를 이용해 내용이 변경되었을 때만 서버가 200 OK로 응답하길 기대한다. ::

   GET /purge.html HTTP/1.1
   Host: example.com
   If-Modified-Since: Mon, 24 Jul 2017 01:09:43 GMT

변경이 있을 경우 200 OK로 응답하며 ``Last-Modified`` 시간이 갱신된다. 
변경이 없는 경우 다음처럼 304 Not Modified 로 응답해야 하여 변경없음을 알린다. ::

   HTTP/1.1 304 Not Modified
   Server: Apache/1.3.27



주의사항
====================================

게시(Publish)서버는 ``Last-Modified`` 값을 통해 최적화된 변경목록을 게시할 수 있다.

예를 들어 아래와 같이 변경되는 파일에 대한 이력을 별도로 저장소(i.e. Database)에 기록하고 이를 동적 페이지로 게시하는 경우를 가정해 보자.

.. figure:: img/xxx.png
   :align: center

먼저 동적 페이지에서는 다음과 같이 ``Last-Modified`` 헤더를 명시적으로 설정해 주어야 한다. ::

   <?php
     header("Last-Modified: Mon, 24 Jul 2017 01:09:43 GMT");
   ?>

   <STON>
   ...
   </STON>
   
이 때 ``Last-Modified`` 설정과 관련하여 현재 시간 1초동안 미묘한 시점이 발생한다.
다음과 같이 3개의 URL에 대해 변경이 1초 안에 발생했다고 예를 들어보자. ::

   example.com/a.jpg       // 01:09:43 기록
   example.com/b.jpg       // 01:09:43 기록
   example.com/c.jpg       // 01:09:43 기록

이때 이 목록에 접근하면 게시서버는 다음과 응답한다. ::

   HTTP/1.1 200 OK
   Server: Apache/1.3.27
   Content-Length: 153
   Last-Modified: Mon, 24 Jul 2017 01:09:43 GMT

   <STON>
      <Body>
         <Item>example.com/a.jpg</Item>
         <Item>example.com/b.jpg</Item>
         <Item>example.com/c.jpg</Item>
      </Body>
   <STON>

STON이 기억하는 ``Last-Modified`` 은 ``Mon, 24 Jul 2017 01:09:43 GMT`` 이다.

이 때 서버에서 아래와 같이 3개의 URL(d.jpg ~ f.jpg)이 변경되었다. ::

   example.com/a.jpg       // 01:09:43 기록
   example.com/b.jpg       // 01:09:43 기록
   example.com/c.jpg       // 01:09:43 기록
   example.com/d.jpg       // 01:09:43 기록
   example.com/e.jpg       // 01:09:43 기록
   example.com/f.jpg       // 01:09:44 기록

STON이 다시 목록에 접근할 다음과 같이 ``If-Modified-Since`` 헤더를 붙여서 요청한다. ::

   GET /purge.html HTTP/1.1
   If-Modified-Since: Mon, 24 Jul 2017 01:09:43 GMT

이 경우 동적 페이지에서 아마도 다음 2가지 조건으로 저장소로부터 변경목록을 수집할 가능성이 높다. ::

   Mon, 24 Jul 2017 01:09:43 GMT  <  변경항목
      -> example.com/f.jpg 만 대상이 된다. (d.jpg, e.jpg 누락)

   Mon, 24 Jul 2017 01:09:43 GMT  <=  변경항목
      -> 모두가 대상이 된다. (a~c.jpg 중복)

이상의 문제로 인해 초 단위의 현재시간은 목록에서 배제해야 한다.
서버는 다음과 같이 변경항목을 추출해야 한다. ::

   If-Modified-Since  <  변경항목  <  현재시간

이 경우 다음과 같이 동작하게 되어 누락/중복을 제거할 수 있다.

.. figure:: img/xxx.png
   :align: center




기타
====================================

게시서버에서 변경목록을 무한히 가지고 있을 수 없다. 
가령 서버가 1주일 동안의 변경목록만을 제공할 수 있다면 STON에 캐싱된 1주일 이전 데이터는 유효하다고 볼 수 없다.
이 경우 다음 설정을 통해 STON이 구동될 때 일정시간 이전의 데이터는 로딩하지 않도록 설정해야 한다. ::

   # server.xml - <Server>

   <Cache>
      <Freshness>0</Freshness>
   </Cache>

-  ``<Freshness> (단위: 일)`` 0보다 큰 경우, STON이 구동될 때 설정된 날 이전에 캐싱된 콘텐츠는 삭제하고 로딩한다.