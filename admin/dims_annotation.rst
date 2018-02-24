.. _dims_annotation:

DIMS
******************

Annotation
====================================

Annotation은 이미지에 글씨를 입힐 수 있는 기능이다.
사전에 제작된 글자 이미지를 "합성" 하는 것이 아니라, 다양한 펜(글꼴, 크기, 색상, 위치 등)을 이용해 이미지에 동적으로 텍스트를 타이핑 할 수 있다. ::

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
   http:// ...(생략)... /dims/maintext

   // 메인 텍스트 + 서브 텍스트
   http:// ...(생략)... /dims/maintext*subtext

   // 서브 텍스트 + 워터마크
   http:// ...(생략)... /dims/subtext*watermark

   // 메인 텍스트 + 서브 텍스트 + 워터마크
   http:// ...(생략)... /dims/maintext*subtext*watermark


   
텍스트 전달
-----------------------

aaaa


속성
-----------------------

bbbbb
