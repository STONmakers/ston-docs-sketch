.. _pattern-webpage:

웹페이지 서비스 패턴
******************

웹페이지 구성시 도움이 되는 패턴들 모음.


반응형 상품기술서
====================================

아직 작성 전입니다.


혼합 콘텐츠 (Mixed Contents)
====================================

해결하고 싶은 문제
------------------------------------
``HTTPS`` 웹페이지에서 (외부에서 제공되는)``HTTP`` 리소스를 참조할 경우 해당 콘텐츠가 차단된다.

.. figure:: img/rsc001.png
   :align: center

.. figure:: img/rsc002.png
   :align: center

-  `혼합 콘텐츠란? - Google <https://developers.google.com/web/fundamentals/security/prevent-mixed-content/what-is-mixed-content?hl=ko>`_
-  `What is mixed content? - Clourflare <https://www.cloudflare.com/learning/ssl/what-is-mixed-content/>`_


솔루션/패턴 설명
------------------------------------
``<HTML>`` 내에 존재하는 혼합 콘텐츠 문제를 클라이언트에게 전송하기 전 필터링한다. 

.. figure:: img/dgm005.png
   :align: center

외부 리소스는 ``M2`` 를 통해 단일 ``HTTPS`` 도메인으로 제공될 뿐만 아니라 ``<iframe>`` 등으로 ``http`` 를 참조하는 경우 일관되게 처리된다.


구현
------------------------------------
-  ``M2`` 리소스 스토리지 앞에 배치한다. (=HTTP 통신이 가능하다.)
-  ``M2`` 혼합 콘텐츠를 필터링할 엔드포인트를 생성한다. ::
   
      # vhosts.xml - <Vhosts><Vhost><M2><Endpoints><Endpoint>

      <Model>
         <Source>https://foo.com/#model</Source>
      </Model>
      <View>
         <Source>https://bar.com/#view</Source>
      </View>
      <Control>
         <Path>/item-detail</Path>
      </Control>


-  ``M2`` View파일에 nunjucks 필터를 적용한다. ::
   
      {{ model.__raw | toHttps('/item-detail/mixed') }}


-  ``M2/STON`` 혼합 콘텐츠 게이트웨이용 가상호스트를 생성하고 이미지툴 기능을 활성화한다. ::
   
      # vhosts.xml - <Vhosts>

       <Vhost Name="mixed.example.com" Status="Active">
          <Origin ByClient="ON" ByClientKeyword="byclient" Protocol="HTTP"/>
       </Vhost>

   외부주소를 동적으로 입력하도록 ``ByClient`` 기능을 확설화한다.


-  ``M2/STON`` 혼합 콘텐츠가 리소스 ``mixed.example.com`` 을 찾을 수 있도록 URL 전처리를 규칙을 추가한다. ::

      <URLRewrite AccessLog="Replace">
         <Pattern><![CDATA[www.example.com/item-detail/mixed/(.*)]]></Pattern>
         <Replace><![CDATA[mixed.example/byclient/#1]]></Replace>
      </URLRewrite>


-  혼합 콘텐츠가 포함된 URL을 ``M2`` URL로 변경한다. ::

      /item-detail?model=ITEM001&view=...


장점/효과
------------------------------------
-  통제할 수 없는 외부 리소스를 포함한 사이트 전체를 ``HTTPS`` 로 제공한다.
-  추후 보안수준이 강화되더라도 ``M2`` 를 통해 정책개선이 가능하다.


주의점
------------------------------------
현재(2020.06) 이미지는 차단되지 않는다.
추후 보안검사 수준이 상향되는 경우 이미지에 대해서도 이 패턴의 사용이 가능하다. 
이 경우 발생하게되는 데이터 트래픽 처리비용에 대해 고려해야 한다.


기타
------------------------------------
SSL/TLS Offloading을 제공하는 CDN과 같이 활용되는 경우가 많다.


