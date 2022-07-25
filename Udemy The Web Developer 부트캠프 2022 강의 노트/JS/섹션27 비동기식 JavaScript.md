<h1>섹션27 비동기식 JavaScript</h1>

<h2> The Call Stack </h2>

콜 스택 = JS가 함수호출을 관리하는 방식. 
책 속의 손가락 같은 것. 
스택 = 자료구조 ( 후입선출 )  , 팬케이크가 쌓여있는 것 같다. 
가장 최근에 추가한 것을삭제함 

- 콜 스택은 JS가 사용하는 매커니즘으로 여러 함수를 호출하는 스크립트에서 해당 위치를 호출한다. 
스크립트가 함수를 호출하면 해석기는 콜 스택에 추가합니다. 

- 첫 번째 함수가 호출한 다른 함수도 콜 스택에 추가되어 호출되면 실행됩니다. 현재 함수가 완료되면 
해석기는 콜 스택에서 함수를 제거하고 마지막 코드 목록의 멈춘 곳에서 계속 실행합니다. 

![image](https://user-images.githubusercontent.com/70703716/180751475-8874fdce-a28f-4a96-ae32-9ab559b6bf5f.png)

스택이 쌓였다가 사라지는 과정을 이해해야한다. 

---> loupe라는 도구, 도구-Soures 에서 그 과정 확인 가능. 

<h2>WebAPI와 단일스레드</h2>

JS는 단일 스레드이다. 
---> 멀티 테스킹을 할 수 없다. 따라서 최대 한 줄의 코드만 실행한다. 

```
setTimeOut(()=> 
  console.log('서버에 보내는 중...')
{},3000);

console.log('마지막파일입니다')

---> 이 경우에 서버에 보내는 중 이전에 마지막 파일입니다가 나온다. 왜?그럴까?

```
이유 : 자바스크립트가 아니라 브라우저가 작업하고 있다. 브라우저는 c++와 같은 다른 언어로 만들어 져서 
자바스크립트가 할 수 없는 것들을 한다. 브라우저는 WebAPI를  가지고 있고 이는 배후에서 일어난다. 
브라우저로 작업을 넘긴다. 
브라우저는 3초라는 공백을 계산해서 *콜스택*에 추가한다. 

<h2> 콜백이라는 지옥 </h2>

함수들을 중첩시키면 콜백 지옥이 만들어진다. 

![image](https://user-images.githubusercontent.com/70703716/180755088-3d835402-c7f6-4412-b5cf-458bf89c8c36.png)

![image](https://user-images.githubusercontent.com/70703716/180755559-a516b35e-b414-4476-ab78-60ca7e9e5555.png)1, 

하나 이상의 콜백이 있는 경우는 흔하다. 

![image](https://user-images.githubusercontent.com/70703716/180756072-efbfd435-2a47-4f25-bfb3-e6d8cf88ac6f.png)

가상의 함수이다. 콜백을 전달한다. 
이 경우 자바스크립트의 문제인 콜백 지옥이 나타날 수 있다. 정해지지 않은 시점의 일을 하려고 할 때 발생.

---> Promise와 비동기 함수로 해결할 수 있다. 


<h2> PROMISES </h2>

Promise는 단지 하나의 객체이다.  최종 값이나 작동 여부에 대한 약속이다. 

![image](https://user-images.githubusercontent.com/70703716/180762882-294b0820-9e39-4e28-b2f1-b6bc2953a85d.png)

.then 과 .catch 가 중요하다. 
둘다 콜백을 받는다. then은 promise가 성공했을 때, catch는 실패했을때이다. 
 
![image](https://user-images.githubusercontent.com/70703716/180764356-e2bb85ab-55aa-469e-b959-1102ef59a554.png)

2단계로 연쇄해서 만들 수도 있다. 

![image](https://user-images.githubusercontent.com/70703716/180764412-548bf9f0-de6d-413c-a2c7-3d6c125e6fa2.png)

이런식으로 말이다. 

하지만 아직은 promises가 낭비같아 보일 수 있다. 중첩같아보이고.. 

하지만 여기서 마법같은 일이 나온다. 
return이다.! 

![image](https://user-images.githubusercontent.com/70703716/180765485-ccabd763-b8e0-4171-839d-c592d83f60ac.png)

이런식으로 적을 수 있게된다. 단 하나의 catch만 필요해진다. 
.then과 .catch를 쓰지만 훨씬 깔끔하다. 
종속적 비동기 동작에서 발생하는 이 Promise 연쇄를 이해하는 것이 중요하다. 
<h3> Promise 작성법 </h3>

```
new Promise((resolve, reject) => {
  })
  
```
작성법은 아래와 같다. 
```
const fakeRequest = (url ) => {
  return new Promise ((resolve, reject)=>{
     const rand = Math.random();
     setTimeout( ()=> {
      if(rand <0.7){ resolve('해결됐다.') ;
      }
      rejcet('에러입니다');
     },1000)
     
  })
}

```
첫째는 Promise를 reslove할 함수입니다. 둘째는 reject할 함수입니다. 

![image](https://user-images.githubusercontent.com/70703716/180770886-bcd53b18-97b3-4425-aa76-71881b9a69c4.png)

처음의 콜백지옥 함수를 이렇게 만들 수 있다. Promise의 대단함! 또한 reject가 문법의 필수는 아니다. 

<h2> 비동기 키워드 </h2>

비동기 함수는 자바스크립트의 새로운 기능이자, 기존 구문의 개선된 방식이다. 
IE에선 지원되지 않지만 아주 유용하다. 비동기 코드를 아주 깔끔하게 하도록 돕는다. 
Promise위에 적용되기 때문에 구문에 뿌리는 설탕같은 것! 

2가지 키워드
- ASYNC
- AWAIT

둘은 같이 쓰인다. 

<h3> async </h3>

함수를 비동기 함수로 선언하면 함수는 자동으로 Promise를 반환한다. 
<b>Promise를 반환하라고 하지 않아도(return new Promise를 안써도) 암시적으로 반환함.  </b>
(신기하다)
비동기 함수에서 오류가 있으면 rejected를 반환함. 

![image](https://user-images.githubusercontent.com/70703716/180776283-c91253cb-ae51-4e30-bc48-8e80583da686.png)

이 경우 return은 실행되지 않는다. throw로 오류를 던진 오류가 있는 함수여서.

<b>여기까지 배우면서 든 의문, 그래서 비동기 함수를 왜 만드는가-> 찾아봐야겠다. </b>


<h3> await </h3>

이 키워드는 비동기 키워드를 쓰면서 동기적으로 보이게 해 준다. 
역할 = 기다리게 하는 것 
Promise가 값을 반환할 때까지 기다리기 위해 비동기 함수의 실행을 일시 정지 시킨다. 
비동기 함수에서만 작동하기 때문에 async와 한쌍이다. 
![image](https://user-images.githubusercontent.com/70703716/180777805-af236c17-adf7-4a71-b1ef-7cedba01498e.png)

훨씬 깔끔해졌다. 

<h3> 비동기 함수가 reject됐을때  </h3>
try catch를 써서 다음 코드가 실행되지 않는 문제를 해결하면 된다. 
catch는 실행되지 않았을 때 에러 정보를 보여줄 수 있다. 
