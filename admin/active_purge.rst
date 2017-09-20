.. _active_purge:

Active Purge
******************

Caching무효화를 위한 `Purge <http://ston.readthedocs.io/ko/latest/admin/caching_purge.html#purge>`_ API 호출방식은 간편하며 직관적인 장점인 반면 다음과 같은 단점도 존재한다.

- 대상 서버가 많아져 일일이 API를 호출하기 어려운 경우
- 클라우드 Auto-Scale 등으로 인해 서버 인스턴스가 지속적으로 변동되는 경우
- 점검등의 이유로 일시적으로 서버가 배제되었다 재투입된 경우 (배제된 시간동안은 API를 호출받지 못할 수 있다)

이런 경우 Publish-Subscribe 모델을 통해 문제를 간단히 만들 수 있다. 

.. figure:: img/pubsub_purge.png
   :align: center

이 모델은 관리자가 약속된 URL로 Purge 목록을 게시(Publish)하고, 각 서버들이 이를 수신(Subscribe)하여 반영하는 구조이다. 
각각의 서버가 능동적으로 목록을 수신하기 때문에 서버 대수가 늘어나면서 발생하는 관리의 어려움이 근본적으로 사라진다.
이 기능은 다음과 같은 목적을 가진다.

- 대형 서비스의 고속 컨텐츠 동기화
- 서비스 전 컨텐츠를 미리 캐싱해 두는 기능 (Pre-warming)
- TTL 수동관리 (TTL을 아주 길게 설정하고 바뀌는 콘텐츠 목록만 게시한다.)

::

   $ server.xml - <Server><Cache>

   <ActivePurge Timeout="5" Cycle="3">http://1.1.1.1/purgelist.html</ActivePurge>

-  ``<ActivePurge>`` 

   관리자가 Publish할 주소를 게시한다. 

   -  ``Timeout (기본: 5초)`` 소켓연결부터 HTTP Transaction이 완료될 때까지 유효시간

   -  ``Cycle (기본: 3초)`` 실행주기

STON은 설정된 URL을 ``Cycle`` 마다 갱신하여 반영한다. 
다음은 예제 XML이다. ::

   <StonFileUpdateList>
      <Policy Method="Purge">
      <List>
         <Url>example.com/logo.jpg</Url>
         <Url>example.com/logo.jpg</Url>
      </List>
   </StonFileUpdateList>

