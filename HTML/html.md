##TIL
###HTML

원래 velog에 썼던 TIL였는데, 깃허브로 옮기기로 해서 정리중

---
HTML에 대한 설명과 다양한 태그들에 대해 배우고 
단순히 검색에 잘 걸리는걸 넘어서 의미를 갖는 것들을 표현하려는 움직임을 알게 되었다. 


###새롭게 알게 된 점들 

1. `<!doctype html>` 해당 문서를 브라우저가 HTML로 렌더링 할 수 있게 알려주는 태그
 
2. 호환성 관련 태그 
    인터넷 익스플러러에서 최신 표준 모드로 렌더링되도록 하는 설정이 있다. 
    `<meta http-equiv="X-UA-Compatible" content="ie=edge>`
   
3.META
  charset 문자 인코딩 설정, utf-8 유니코드 
  name 메타 정보 이름
  
4.반응형 웹 관련 태그들

  `meta name="vierport"`설정으로 초기 뷰포트에 대한 설정을 할 수 있다. 
  
  
<strong>5.Semantic Web</strong>
처음 알게된 개념. 
웹 페이지 각 요소에 의미를 부여함. 새로웠다. 
'header,nav,aside,section,article,footer'가 있고 
필수는 아닌듯하다. 부분을 지정하는데만 사용되고, 위치나 표현등은 css로 따로 구현한다. 

5. 호환성 관련 내용들 
  - HTML 버전에 따라 deprecated되는 태그나 속성이 있다. 표준에 부합하는지는 
  W3C validator에서 검사할 수 있음. 
  - 접근성도 자가진단 가능. 

6. WEBP라는 이미지 포맷 
  동영상, 투명도 지원되는 포맷, 구글에서 개발, 일부 브라우저 미지원, 손실/비손실압축 모두 지원. 
  
