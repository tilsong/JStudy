## 자바스크립트의 궁극적인 목적

- 사용자와 만나는 접점
- 사용자에게 콘텐츠를 제공
- 우선, 사용자를 생각해야..

---

## 기본 문법

- 들여쓰기 잘하자 : 기본적으로 2칸, 4칸 일괄되게 하기!6

- 변수 => "=" - 값을 변수에 "할당"하는 것

- 시맨틱(semantic) : 의미를 부여하여 변수 이름을 작명하는 것

- 주석=> //(한줄 주석), /* */ (블록주석), /** */(코드 주석)

- 콘솔 => api 있음. 참고, ctrl+ shift+i => 콘솔

- 정수, 실수 => js는 정수, 실수를 구분하지 않는다. 모두 정수로. 다만 1.0001 이면 실수로.

  IEEE 754표준 => 64bit 부동소수점 처리 => 123을 123.0으로 처리, 0.12+5 =5.12(실수변환)

  ES6에 정수, 실수 구분 추가

- 상수 => 바꿀 수 있으나 대문자로 시맨틱 선언함 EX) var MAX= 10

- typeof 연산자 => 데이터 타입 반환

- 데이터타입? 언어타입(js에서 사용가능)과 스펙타입(불가)

- number타입 .. nan(not a number,숫자가 아님) => 1*"a" => NaN으로 출력. 왠만하면 프로그램이 죽지 않게 하기 위한 것.

- undefined 타입 변수를 선언만 한것의 초깃값. 값 할당 안한 것을 나타내는 시맨틱

  변수에 undefined를 할당할 수도 있다.그러나 이 때는 null을 할당하는 것이 적합하다.

- null 타입 : undefined는 단지 변수만 선언,  null을 할당해야 값이  null이됨. 의도적으로 값을 할당한 것으로 코드를 수행한 것이 된다.

- 대문자 Object 타입 : {name: value} 형태

  프로퍼티 : name(프로퍼티 key, name)과 value(프로퍼티 값) 하나를 지칭

  Object는 프로퍼티 집합

- typeof null도 object가 나온다.. es6에서는 극복할 수 있는 방법이 나왔다

---

## 연산자, 표현식

- 표현식(expression)

  ex) 1+2 , var total = 1+2;

  이를 표현식을 '평가'한다고 한다.

  표현식을 평가하면 결과가 반환되면 이를 '평가 결과'라고 한다.

- 해석?

  js 코드를 기계어로 바꾸는 것. Compile

  engine엔진이 해석하고 실행한다고 한다.

- 숫자계산시 변환

  undefined => nan , null = +0 , boolean = true:1, false:0, 

  String : 숫자이면 숫자로.  다만 더하기(+)때는 연결해서 String 타입으로 변환됨

- IEEE 754 유동 소수점

  2.3*3; //6.8999999

  그러므로 실수를 정수로 변환하여 값을 구하고 다시 실수로 변환해야 함

  => 2.3 * 10 * 3/ 10;

- 단항 + 연산자

  값을 number 타입으로 변환 +value //-연산자 => 음수로 변환, (-)이 더 가독성 좋음

  Number()도 기능 같음 Number(value)  => 가독성은 이것이 더 좋음

- 전치 후치 연산자. 전치(계산 전에 하기) , 후치(계산 후에 하기)

- utf => 유니코드의 코드 포인트를 매핑하는 방법, 

  => utf-8, 8bit로 코드를 인코딩하겠다는 것

- 연산자 => 코드 포인트를 유니코드를 등록할 때 부여. 유니코드 등록 순서로 비교하게 됨

  이것은 정렬을 할 때 사용하게 된다.

- undefined, null은 값임. 따라서 ==(동등 연산자)로 비교하면 true, ===(일치 연산자)로 비교하면 타입이 다르므로 false를 반환하게 된다.

- &&, || 모두 결과되는 값을 반환하게 된다. ex) var artistb = ''; var artistB = (artistB || '무명아티스트'); var artistb = ''; var artistB = (artistB || {}); //빈 객체 생성 가능

---

## 문장

- 화이트 스페이스(LF/CR) LF -> 다음 줄 같은자리, CR 맨 앞자리로.. ES5는 세미콜론이 없으면 삽입 후 LF/CR을 실행시킴

- debugger 위치에서 실행 멈춤  debugger;

  브라우저의 개발자 도구 창이 열려 잇을 때만 멈춤 아니면 멈추지 않음(es5부터 지원)

- try-catch-finally : java와 같은 듯, 통신을 할때, 서버에서 데이터를 가져올 때 이 구문을 써줄 수 있음.

- throw표현식 : 명시적으로 예외를 발생시킴. 예외가 발생하면 catch 실행

  ```javascript
  try{
  	throw{
  		msg:"예외 발생시킴",
  		bigo: "임의의 이름 사용" //throw를 문자열로 던짐
  	};
  } catch(error){
  	log(error.msg);
  	log(error.bigo);
  }
  
  ---------
   try{
       throw new Error("예외 발생시킴"); //throw를 오브젝트를 만들어서 던짐
   } catch(error){
       log(error.message);
   };
  ```

- strict 모드

  형태: "use strict"

  엄격하게 js 문법 사용의 선언, 작성한 위치부터 적용(es5부터 지원)

  var키워드를 선언하지 않는다? 에러 발생-> try catch문 필요

  => 코딩 실수를 예방하는 것.. 퍼포먼스, 자바스크립트 엔진에도 영향을 미친다. 

  이제는 use strict를 사용합시다.

- label문? 

  java에서도 목격한 것.. outter처럼 반복문의 이름 지정해놓으면 문장 실행시 해당 반복문으로 이동하는 것을 말한다.

  ```js
  var i, j;
  
  loop1:
  for (i = 0; i < 3; i++) {     
     loop2:
     for (j = 0; j < 3; j++) {   
         if (i === 1 && j === 1) {
           continue loop1; //이 문장이 실행되면, loop1으로 이동한다.
        }
        console.log('i = ' + i + ', j = ' + j);
     }
  }
  ```

- with문?

  ```js
  function doSomething(value, obj) { 
  	with (obj) { 
  		value = "which scope is this?";
  		console.log(value);
  	}
  } //이 때, value가 어디서 나온 것인지 모호하다. "Ambiguity"
  
  ```

---

## 함수

- 함수 코드는 짧을 수록 좋음. 이 때 주석이 있으면 완벽

- 주석? 코드를 작성하기 전에 먼저 주석으로 생각을 정리하기! 

  코드의 목적과 결과가 미치는 영향 작성

- ex

![image-20210327173601578](C:\Users\송은석\AppData\Roaming\Typora\typora-user-images\image-20210327173601578.png)

---

## 오브젝트

프로퍼티

- Property {name: value} 형태

- name에 프로퍼티 이름, 키를 작성

- value에 js에서 지원하는 타입 작성 => 하나의 value에 새로운 property 사용가능

- Object를 객체라고 부르지만 뉘앙스 다름.

  object는 실체가 있는 것. 객체는 없을 수도 있음.

- 오브젝트에 프로퍼티를 **추가, 변경**할 수 있다.

- var obj ={}; obj.abc = 123; //프로퍼티 이름으로 abc있으면 변경, 없으면 추가

  ```js
  //1. 점과 프로퍼티 이름으로 변경
  var book.k = "asdf";
  
  //2. 대괄호 사용
  var book["k"] = "asdf";
  
  // 3.변수이름으로 변경
  var book = {title:"js"};
  var varName = "title";
  book[varName] = "html";
  log(book); // {title:html}
  ```

프로퍼티 값 추출 -> .으로, [~]으로

- for~in

  for(변수 in 오브젝트) 문장;

  ```js
  var sports = {
  	soccer: "축구",
  	baseball: "야구"
  };
  for(var item in sports){
  	log(item); //프로퍼티 이름
  	logsports[item] //프로퍼티 값
  }
  // soccer 축구  
  // baseball 야구 출력
  
  ```

  es3까지는 순서 보장x,

  es5부터는 작성된 순서대로 읽혀짐.

---

## 빌트인

- Built-in이란? ==> 내장객체말하는 것
  - 값 타입, 연산자, 오브젝트(Object)를 사전에 만들어 놓은 것. js 코드를 처리하는 영역에.
  - 장점은 사전 처리를 하지 않고 즉시 사용하는 것임. 자바 스크립트의 특징임.
- 빌트인 값 타입
  - undefined, null, boolean, number, String Object
- 빌트인 오브젝트?
   - 빌트인 Number 오브젝트
     	- 123과 같은 숫자, 상수, 지수를 처리하는 오브젝트, 여기서 오브젝트는 소문자 object
     	- 대문자는 키 밸류로 저장하는 것이 목적, 소문자는 데이터를 처리하는데 중점. 따라서 소문자 오브젝트는 함수가 있다.  

---

Number 오브젝트

숫자처리를 위한 함수와 프로퍼티 포함, 함수를 호출하여 숫자 처리함.

![image-20210327203419629](C:\Users\송은석\AppData\Roaming\Typora\typora-user-images\image-20210327203419629.png)



- Number()  => 파라미터 값을 Number 타입으로 변환

- new 연산자 

  ```js
  var obj = new Number();
  log(typeof obj); //object로 반환!
  
  var oneObj = new Number("123");
  log(typeof obj); //인스턴스마다 다른 값을 가지게 됨. 이것이 인스턴스 만드는 목적
  ```

- 인스턴스 

  파라미터를 넣어 생성했을 때, prototype에 있는 메소드만 가지고 온다. 나머지는 가려서 복사하는 것.  => 인스턴스를 만드는 기준은 프로토타입에 연결된 함수를 연결해 주는 것. 나머지는 복사x _prototype을 오브젝트에 넣어서 주겠다. 그것이 인스턴스이다.

- 프리미티브 값

  언어에 있어 가장 낮은 단계의 값. var book="책" "책"은 더이상 분해, 전개 불가

  Number, String Boolean : 인스턴스 생성 가능

  Null, Undefined : 인스턴스 생성 불가

  Object는 프리미티브 값을 제공하지 않음

  단지 key value로 하나의 값을 가지는 것.. 이것이 프리미티브 값.

  펼쳤을 때 다른 프로터티가 있는 것은 프리미티브가 아니다.

  [[  ㅁㄴㅇㄹ ]] =>대괄호 2개 => 자바스크립트 엔진이 만들었다는 것

  인스턴스를 생성하면 파라미터 값을 인스턴스의 프리미티브 값으로 설정. 이렇듯 프리미티브 값을 갖는 오브젝트는 Boolean, Date, Number, String 이 있다.

  ```js
  var obj = new Number(123);
  log(obj+12);
  //obj가 인스턴스 임에도 값이 더해질 수 있는 것은, 123을 인스턴스의 프리미티브 값으로 설정하기 때문이다. 프리미티브 값을 갖는 인스턴스에 값을 더하면 인스턴스의 프리미티브 값에 값을 더한다.
  ```

- valueOf() => Number 인스턴스의 프리미티브 값을 반환.

- String 타입으로 변환 =>  data를 String 타입으로 변환함

  ```js
  var value = 20;
  log(value.toString());
  log(20..toString())//유동 소수점 사용될 수 있음에 주의!! 이경우 20.을 처리함
  
  ```

- toLocaleString() => 숫자를 브라우저가 지원하는 지역화 문자로 변환

  브라우저 개발사에 일임. 지역화 지원하지 않으면 toString()으로 변환됨

  es5는 사용불가, es6는 파라미터에 언어 타입 사용 가능(한국꺼 어케하는지는 안나옴. 찾아볼것)

- toExponential() => 숫자를 지수 표기로 변환하여 문자열로 반환

  변환 대상의 첫 자리만 소수점 앞에 표시, 나머지는 소수 아래에 표시. e(지수) 다음에 정수에서 소수로 변환된 자릿수 표시. 몰겠다.

  그외 toFix등!

  

  

  

  

  

  



