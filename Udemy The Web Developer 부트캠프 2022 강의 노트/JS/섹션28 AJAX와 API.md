<h1>섹션28 AJAX와 API</h1>

우리는 늘 요청을 한다. 클릭하는 등의 행동으로 할 수 있다. 
하지만 코드로도 요청을 할 수 있다. 이걸 AJAX라고 한다. 
AJAX는 비동기식 자바스크립트와 XML이다. 

<h2>AJAX</h2>
자바스크립트를 사용해서 앱을 만드는 기술. 데이터를 올리거나 꺼낼 수 있고 어디론가 보낼 수 있다. 
진행 과정을 저장하거나 데이터베이스에 저장해야하기 때문. 새로고침 없이 요청 가능. 

<h2>API</h2>

자바스크립트로 AJAX요 청을 할 때, HTML CSS JS가 아닌 순수한 정보를 원한다. 
사람의 편의를 위한 코드는 필요하지 않다. 이때 필요한게 API이다. (Application Programming Interface)
컴퓨터가 여러 소프트웨어와 상호 작용하거나 소통하는 모든 인터페이스를 의미하는 광범위한 용어. 
소프트웨어끼리 작용하는 인터페이스. 웹과 상관 x 
하지만 대부분 개발자들이 사용할땐 webAPI를뜻함 
WebAPI는 웹, HTTP를 기반으로 하는 인터페이스. WebAPI는 다른 애플리케이션이나 데이터베이스로 가는 입구인것. 
-> 무슨 소리지? 

엔드포인트로 요청을 보낸다. 
-> 엔드포인트가뭐지 

<h2>JSON</h2>

포맷. 경량화된 포맷. 정보 자체인 데이터만을 위해 고안된 포맷. 
- XML (과거에 많이 사용)
- JSON ( 계속해서 데이터를 전송하거나 정보를 전송하는 포맷 ) 
JavaScript Object Notation 
사용자끼리 전송하거나 api에서 브라우저로 전달. "키":"값"쌍의 형태를 가진다. 자바스크립트랑 비슷해보이지만 
차이가 있다. 일단 undefined가 없다. 

api 엔드포인트로 요청을 보내면 정보가 엄청 많이온다. 
이걸 JS로 바꾸는 방법(파싱)은 
``` JSON.parse(data) ```
JS를 JSON형식으로 바꾸는 방법은 
``` JSON.stringify(data)```
이다. 

<h2>API에 요청을 보내는 방법, Postman </h2>

postman이란? 요청을 보내는 코드를 작성하기 위한 무료 앱. 

get으로 얻을 수 있다. 
HTTP상태코드(satus) - 200,201,202 (좋은 상태) , 3으로 시작 ( 리디렉션 코드), 4로 시작 ( 좋은 의미x, 클라이언트 오류) 
500번대 ( 서버 오류 ) 

헤더 - 응답과 요청을 위한 메타데이터이다. 키-값 쌍에 대한 설명을 보여준다. 


<h2> 문자열 및 쿼리 헤더 </h2>

쿼리 문자열 : 입력해야 하는 것 , URL의 한 부분으로서 우리가 입력해야 하는 정보이고, 우리가 얻는 결과에 영향을 준다. 
하나 이상의 문자열을 넣을 수도 있다. &을 사용해서 연결한다. 
``` 
q=:query

:query이 내가 입력해야 하는 것이다. 
```

<h2> XHR 객체 만들기 </h2>

XHRhttprequest는 굉장히 오래된 것. Promise도 안된다. 


![image](https://user-images.githubusercontent.com/70703716/180929797-e36817be-056c-4761-b588-32a2c514a949.png)

![image](https://user-images.githubusercontent.com/70703716/180929984-524da109-add8-4be2-91a9-637d85e39ec5.png)

이런식으로 가격을 가져올 수 있다. 

<h2> Fetch API </h2>
자바스크립트를 이용해서 HTTP요청을 만드는 최신 방식. 
Promise사용 가능-> then catch 사용가능. IE에선 사용 불가하다. 
Promise는 불완전한 응답 객체로 resolve되고 데이터는 계속 들어오고 파싱은 되지 않는다. 
fetch의 단점 중 하나 JSON으로 변환해주는 과정 필요합니다. --> axios라는 라이브러리가 있는 이유
```
JSON()함수 ---> 비동기 함수가 다 작동한 후에 Promise를 보여준다. 
```
그래도 XML보단 뛰어나다. 콜백을 중첩하지 않아도 됨. 

![image](https://user-images.githubusercontent.com/70703716/180931098-5a052c44-e173-4fe6-9d0a-d440edd293aa.png)


![image](https://user-images.githubusercontent.com/70703716/180931146-eb717e6a-b43c-435d-83cd-7b55340bd10b.png)

이건 비동기 함수를 이용한 짧게 만든 버전이다. async 함수 ->promise를 반환한다. 

<h2> Axios 라이브러리 </h2>

Fetch를 기반으로한다. 링크를 HTML문서에 붙여서 사용할 수 있다. 

<h3> Axios.get </h3>
![image](https://user-images.githubusercontent.com/70703716/180931851-059b4e14-2727-4407-ac43-37f7bee21027.png)

구문은 똑같다. 다만 JSON으로 변환하는 과정이 필요 없다. 

![image](https://user-images.githubusercontent.com/70703716/180932068-a43cdf38-9dae-457a-b881-9cc83b226337.png)
비동기 함수로 만드는 과정 

<h3> 헤더 세팅하기  </h3>

![image](https://user-images.githubusercontent.com/70703716/180932975-bd5f2c9f-da0e-4a10-b131-8e731f919f9b.png)
![image](https://user-images.githubusercontent.com/70703716/180933090-3a0b7357-aa52-455c-af9d-a11892045226.png)
이렇게 두번째 인자를 헤더로 지정해주면 된다. 

