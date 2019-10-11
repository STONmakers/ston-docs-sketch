.. _multisession:

원본 멀티세션 다운로드
******************

이 기능은 `원본서버 - Range요청 <https://ston.readthedocs.io/ko/latest/admin/origin.html#range>`_ 의 확장으로 동작한다. 이유는 다음과 같다.

 - 원본에서 한 세션이 다운로드 받는 크기를 제한(설정)한다.
 - 다운로드 시점에 서로 다른 Range로 여러 세션을 생성한다.


멀티세션 다운로드
====================================

다운로드 크기와 해당 크기만큼 동시에 다운로드 받을 세션 수를 설정한다. ::

   # server.xml - <Server><VHostDefault><OriginOptions>
   # vhosts.xml - <Vhosts><Vhost><OriginOptions>

   <PartSize Session="0" Continue="On">0</PartSize>


``<PartSize> (단위: MB)`` 만큼을 다운로드 받는 세션을 ``Session (단위: 개)`` 수 만큼 만들어서 다운로드를 진행한다. 
``Continue (기본: ON)`` 설정이 ``ON`` 이면 파일의 끝까지 멀티세션 다운로드가 진행된다. ``OFF`` 인 경우 1회만 다운로드를 진행하고 멈춘다.

예를 들어 1MB씩 15개의 세션으로 완전한 다운로드를 진행하려면 다음과 같이 설정한다. ::

   <PartSize Session="15">1</PartSize>


반면 1MB씩 15개의 세션으로 15MB만 다운로드를 진행하려면 다음과 같이 설정한다. ::

   <PartSize Session="15" Continue="Off">1</PartSize>



.. note::

   디스크 공간 절약등의 목적이 아닌 경우 ``Continue`` 설정은 항상 ``ON (기본값)`` 으로 유지해야 속도 향상을 기대할 수 있다.


