.. _dash:

DRM
******************

콘텐츠를 암호화하여 전송한다. 

.. figure:: img/drm1.png
   :align: center

::

   # server.xml - <Server><VHostDefault><Options>
   # vhosts.xml - <Vhosts><Vhost><Options>

   <Drm Status="Inactive" Keyword="drm">
      <Algorithm>AES_128_CBC</Algorithm>
      <IV> ... </IV>
      <Key> ... </Key>
   </Drm>

-  ``<Drm>`` DRM 방식을 설정한다. ``Status="Active"`` 로 설정되면 활성화된다. 
   서비스 주소 뒤에 ``Keyword`` 를 suffix로 붙여 DRM을 구동한다. ::

      // URL
      www.example.com/music.mp3

      // DRM 처리된 URL
      www.example.com/music.mp3/drm


-  ``<Algorithm> (기본: AES_128_CBC)`` 
   암호화 알고리즘을 선택한다.
   사용가능한 알고리즘은 다음과 같다.

   ================== ============
   <Algorithm>        Bits
   ================== ============
   AES_128_CBC        128
   AES_256_CBC        256
   RC4_128            128
   ================== ============

-  ``<IV>`` Initial Vector.

-  ``<Key>`` 암호화 키

``<IV>`` 와 ``<Key>`` 를 평문(Plain Text)으로 제공하면 보안적으로 취약하다.
이를 아래 API를 이용해 암호화한 뒤 설정할 것을 권장한다. ::

   /command/encryptpassword?plain=abcdefghijklmnop

암호화된 ``<IV>`` , ``<Key>`` 설정을 위해 ``Type="enc"`` 속성을 추가한다. ::

   # server.xml - <Server><VHostDefault><Options>
   # vhosts.xml - <Vhosts><Vhost><Options>

   <Drm Status="Active" Keyword="drm">
      <Algorithm>AES_128_CBC</Algorithm>
      <IV Type="enc">RokyekMd0IjDnRGKjVE7sQ==</IV>
      <Key Type="enc">x4KHA1b+AirBOIoaeEBHmg==</Key>
   </Drm>


.. note::

   암호화 API는 인증서에 기반하여 동작한다. 
   따라서 인증서가 다르면 암/복호화 결과가 다르다.

