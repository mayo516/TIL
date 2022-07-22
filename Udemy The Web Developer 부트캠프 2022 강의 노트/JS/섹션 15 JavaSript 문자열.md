<h1> 섹션 15 JavaSript 문자열 </h1>

<h2> Strings </h2>

자바스크립트의 다른 원시타입. text(문자)를 나타낸다. 인용구("")감싸서 표현해야함. 

<h3> 문자열은 인덱스가 있다 </h3>

0부터 시작하는 인덱스가 있음


<h3> 문자열 함수 </h3>
내장 함수임. 

```
thing.method() 형과
thing.method(arg)형이 있다. 

```

<h4> 1)  toUpperCase() / toLowerCase() </h4>

<h4> 2) Trim() </h4>

```
let greeting = '   leave me alone plz    ' ; 
greeting.trim() // 'leave me alone plz'
---> 양옆의 공백을 없애줌 
```

<h4> 3) indexOf(arg) </h4>

```
let tvShow = 'catdog' ;

tvShow.indexOf('cat'); //0
tvShow.indexOf('dog'); //3
tvShow.indexOf('z'); // -1 (not found)

--->해당 문자가 나타나는 인덱스 번호를 반환함

```



<h4> 4) slice </h4>

```
let str = 'supercalifragilisticexpialidocious'
str.slice(0,5); //'super'
str.slice(5); //'califragilisticexpialidocious'

---> 잘라냄 ( 시작 , 끝 +1 ) 
```


<h4> 5) replace </h4>

```
let annoyingLaugh = 'teehee so funny! teehee!';
annoyingLaugh.replace('teehee', 'haha') // 'haha so funny! teehee!'

---> 다른 텍스트로 대체한다. 처음 인자만 바꿔줌 

```

<h3> 템플릿 리터럴 </h3>

```
`I counted ${ 3 + 4 } sheep`; // "I counted 7 sheep

---> `백틱을 쓰는게 포인트 

```

<h3> Math 객체 </h3>

![image](https://user-images.githubusercontent.com/70703716/180371587-265a2724-7ae8-4606-a2c3-59fcd6b49e53.png)


<h4> 랜덤 숫자 </h4>

![image](https://user-images.githubusercontent.com/70703716/180371663-fe3aa2e5-c7c9-4d7d-ba80-f43cff4b9964.png)
<br>
<h4> 랜덤 정수 </h4>

![image](https://user-images.githubusercontent.com/70703716/180371697-94beaf2e-4b6e-4e6b-b353-913e41e56480.png)

---> 랜덤 숫자 *10 하고 내렴(floor)

