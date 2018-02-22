.. _dims_annotation:

DIMS
******************


Annotation
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


