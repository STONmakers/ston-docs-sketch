.. _dims_annotation:

DIMS
******************

.. note::

   Q> 멀티 annotation 정책이 궁금합니다. ::
   
      /annotation/maintext*subtext/resize/100x100
      /annotation/maintext/resize/100x100/annotation/subtext
      
   
   Q> ``<Text>`` 가 ``<Annotation>`` 하위에 위치하는 원칙이 궁금합니다. ::

      펜을 손에 드는 순간 <위치>와 <내용>를 제외한 모든 것이 결정된다고 생각합니다.
      오프라인에서는 <위치>를 직관적으로 쉽게 바꿀 수 있습니다.
      하지만 온라인에서는 그렇지 않기에 "설정"으로 고정합니다.
      결국 <내용>인 text만 남아 "변수"의 형태를 이룹니다.
      
      본 문서는 이 기능의 주제인 "텍스트를 넣는다" 를 부각하는 것을 최우선으로 기술되었습니다.
      그 외 (기술적으로 중요하지만 고객에겐 머리아픈) 설정은 단순 Key-Value 형태로 치부하였습니다.
      
      이 과정에서 <Text> 가 <Annotation> 으로 통합 되었습니다.



Annotation
====================================

Annotation은 이미지에 글씨를 입힐 수 있는 기능이다.
사전에 제작된 글자 이미지를 "합성" 하는 것이 아니라, 다양한 펜(글꼴, 크기, 색상, 위치 등)을 이용해 이미지에 텍스트를 타이핑 한다. ::

   # server.xml - <Server><VHostDefault><Options>
   # vhosts.xml - <Vhosts><Vhost><Options>

   <Dims Status="Active" Keyword="dims">
      <Annotation Name="maintext"> ... </Annotation>
      <Annotation Name="subtext"> ... </Annotation> 
      <Annotation Name="watermark"> ... </Annotation>
   </Dims>

각각의 ``<Annotation>`` 은 고유한 ``Name`` 으로 명명된다. 
여러 ``<Annotation>`` 을 미리 등록하고 다음과 같이 ``*`` 를 구분자로 조합하여 사용한다. ::

   // 메인 텍스트
   http:// ... /dims/maintext

   // 메인 텍스트 + 서브 텍스트
   http:// ... /dims/maintext*subtext

   // 서브 텍스트 + 워터마크
   http:// ... /dims/subtext*watermark

   // 메인 텍스트 + 서브 텍스트 + 워터마크
   http:// ... /dims/maintext*subtext*watermark




``<Annotation>`` 은 다양한 속성을 지원한다.

================= ============== ==============================
속성              기본 값         설명
================= ============== ==============================
Name
Font
Size
Color
BackgroundWidth
BackgroundHeight
BackgroundColor
Gravity
Geometry
Dissolve
================= ============== ==============================