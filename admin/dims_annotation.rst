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
      

   Q> 폰트 예제가 더 필요합니다. ::

       사용할 수 있는 폰트 예제와 색을 디테일하게 지정하는 예제가 더 필요해 보입니다.
       참고할만한 링크가 있다면 더 좋을 것 같습니다.
      

   Q> 멀티라인 지원은 이번 버전에 포함되나요? ::

       우선 문서에는 주석으로 넣긴 했지만 Align기능이 필요해 보입니다.
      

   Q> 한글깨짐에 관하여  ::

       IE의 이슈라기 보다는 한글은 클라이언트 호환성이 확보되지 않으므로 서버 사이드에서 인코딩해서 노출하라는 식의 가이드가 어떨까요?
       권장 가이드가 있으면 좋을 것 같습니다.




Annotation
====================================

Annotation은 이미지에 글씨를 입힐 수 있는 기능이다.
사전에 제작된 텍스트 이미지를 "합성" 하는 것이 아니라, 다양한 펜(폰트, 색상, 위치 등)을 이용해 이미지에 텍스트를 타이핑 한다. ::

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

기본 텍스트는 ``<Annotation>`` 의 값이지만 약속된 QueryString을 통해 텍스트를 입력받을 수 있다.



● Text
        - 실제 이미지에 표시될 Text를 지정한다.
        - 값이 반드시 있어야 한다.
        - Value에 예약어 형태로 key 값을 지정한다. ($QUERYSTRING[], 없는 경우 Plain Text)

    ex)
        <Dims>
            <Annotation Name="...">
                <Text>TEST$QUERYSTRING[textValue]$REQ[host]</Text>
            </Annotation>
        </Dims>


.. note::

   텍스트 줄 바꿈은 ``\n`` 을 이용해 할 수 있다.



``<Annotation>`` 은 다양한 속성을 지원한다.

================= ======================== ====================================================
속성              기본 값                   설명
================= ======================== ====================================================
Name              (없음)                     ``<Annotation>`` 이름
Font              none (System Font)        폰트를 지정한다. (ttf, otf, woff 지원)   
Size              10                        텍스트 크기
Color             black                     텍스트 색상
BackgroundColor   none (투명)                배경 색상
BackgroundWidth   (텍스트 크기에 맞춤)        배경 폭 
BackgroundHeight  (텍스트 크기에 맞춤)        배경 높이
Gravity           c                         텍스트 위치 기준
Geometry          +0+0                      Gravity로부터 거리
Dissolve          50                         텍스트 투명도
================= ======================== ====================================================

- ``Color`` 와 ``BackgroundColor`` 는 다음과 같이 표현한다. ::

      // 키워드
      black, red, orange ...

      // RGB
      ??


- ``BackgroundWidth`` 와 ``BackgroundHeight`` 값이 0이면 텍스트에 맞추어진다. ``Origin`` 을 지정할 경우 대상 이미지의 폭과 넓이를 사용한다.

- ``Gravity`` , ``Geometry`` , ``Dissolve`` 는 <합성>과 동일하다.
