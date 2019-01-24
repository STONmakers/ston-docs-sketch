.. _imagelog:

Image Log
******************

On-the-fly 이미지 처리 결과를 로깅한다.

.. figure:: img/image_log1.png
   :align: center

Image.log는 Access.log와 Origin.log사이에 위치하며 다음과 같은 관계를 가진다.

-  ``Access.log`` 신규 가공일 경우(TCP_MISS)에만 Image.log에 기록된다.
-  ``Origin.log`` Image.log에만 기록되었다면 원본 이미지는 이미 캐싱되어 있는 상태이다.



설정
====================================

기존 로그 설정방식과 동일하며, Access.log, Origin.log와 동일하게 가상호스트별로 설정한다. ::

   # server.xml - <Server><VHostDefault><Log>
   # vhosts.xml - <Vhosts><Vhost><Log>

   <Image Type="time" Unit="1440" Retention="10">OFF</Image>

기본 값은 ``OFF`` 이다.




로그 형식
====================================

성공여부와 상관없이 모두 기록된다. ::

    #Fields: date time cs-uri sc-status x-convert-error-code x-convert-error-message x-origin-size x-convert-size time-convert time-taken x-session-id
    2012.06.27 17:40:00 357 899 192.168.0.13 GET i.example.com /t/2.gif 115.71.9.136 200 - - - 3874 197 271 3874 20 0 0 17 3 - gzip+deflate - 80 gzip 7 cache
    2012.06.27 17:40:00 357 900 192.168.0.13 GET i.example.com /ex1.gif 115.71.9.136 200 - - - 5673 223 272 5673 24 0 0 21 3 - - - 80 - 8 cache
    2012.06.27 17:40:00 357 901 192.168.0.13 GET i.example.com /exB.jpg 115.71.9.136 200 - - - 8150 189 273 8150 13 0 0 9  4 Bypass - - 80 - 7 cache
    #[ERROR:01] 2012.06.27 17:40:01 220.73.216.5 220.73.216.5 GET /web/nmb/img/main/v1/h1.gif 1824 Connect-Timeout - 11 cache
    2012.06.27 17:40:00 357 901 192.168.0.13 GET i.example.com /exB1.jpg 115.71.9.136 200 - - - 8150 189 273 8150 13 0 0 9 4 - max-age=3600 80 - 12 cache
    2012.06.27 17:40:00 357 901 192.168.0.13 GET i.example.com /exB2.jpg 115.71.9.136 200 - - - 8150 189 273 8150 13 0 0 9 4 - no-cache 80 - 35 cache
    2012.06.27 17:40:00 357 901 192.168.0.13 GET i.example.com /exB3.jpg 115.71.9.136 200 - - - 8150 189 273 8150 13 0 0 9 4 - - 80 - 35 cache

모든 필드는 공백으로 구분되며 각 필드의 의미는 다음과 같다.

-  ``date`` 이미지 가공이 완료된 날짜
-  ``time`` 이미지 가공이 완료된 날짜
-  ``cs-sid`` 이미지 가공을 요청한 클라이언트 세션 ID
-  ``cs-uri`` 클라이언트가 요청한 URI
-  ``x-result`` 이미지 가공 결과코드

   - ``200`` 성공
   - ``400`` 원본 이미지의 응답코드가 200이 아니다. ( ``x-error`` : 원본 HTTP 응답코드)
   - ``401`` 원본 이미지 크기가 유효 범위가 아니다. ( ``x-error`` : 원본 Content-Length)
   - ``402`` 원본 이미지가 100% 로딩되지 못했다.
   - ``500`` 이미지 가공 중 에러가 발생했다. ( ``x-error`` : 실패 사유)
   - ``501`` 이미지 가공은 완료되었으나 저장과정 중 에러가 발생하였다.

-  ``x-error`` 이미지 가공 에러 상세내용
-  ``x-origin-size (단위: Bytes)`` 원본 이미지 크기
-  ``x-processed-size (단위: Bytes)`` 가공된  크기
-  ``time-taken (단위: 밀리세컨드)`` 이미지 가공 HTTP 트랜잭션이 완료될 때까지의 전체 소요시간
-  ``time-processed (단위: 밀리세컨드)`` 이미지 가공 소요시간