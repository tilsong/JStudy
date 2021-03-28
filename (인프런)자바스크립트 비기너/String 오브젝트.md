String 오브젝트

- "abc"처럼 문자처리를 위한 오브젝트. 이를 위한 프로퍼티와 함수가 포함됨.

![image-20210327212814442](C:\Users\송은석\AppData\Roaming\Typora\typora-user-images\image-20210327212814442.png)

- String() 

  => 파라미터 값을 String 타입으로 변환하여 반환. 안쓰면 빈 문자열 반환 (""+123)도 가능함

  ​	파라미터 값이 프리미티브 값이 되는 것.

  valueOf () => 프리미티브 값 반환

  length 프로퍼티 => 문자 수 반환

  그런데, 단순히 var value = "asd";를 했을 때도 length 프로퍼티를 사용할 수 있다. 어떻게?

  => 엔진이 value.length를 만나면 

  	- value가 String 타입이므로, 
  	- 내부에서 new String("asd")으로 오브젝트를 만들게 되며, ==> 내부 wrapper 객체 생성, 
  	- 이후 프리미티브밸류를 보고 3으로 length값을  생성하여 반환하게 된다. => 반환후 내부 wrapper 객체 삭제

  만약 var value = new String("asd");를 해서 String 오브젝트를 만들게 되면, 

  프리미티브밸류는 [[PrimitiveValue]]:"asd"로 내부에 엔진에 의해 저장된다. 또한 대괄호 두개는 외부에서 사용하지 않고 내부에서 사용하겠다는 뜻이다. 

   length는 [[]]없다. 이 말은 자바스크립트 엔진에 의해 만들어지기는 하지만, 외부에서도 개발자 코드로 사용할 수 있는 것이다. 따라서 length는 .length하면 쓸 수 있고, PrimitiveValue는 valueOf를 통해서 알아낼 수 있는 것이다.

  또한 내부적으로 문자열을 인덱스별로 구분한다. ex) 0:"a" , 1:"s", 2:"d" 키밸류로 프로퍼티로 저장한 것!

  ![image-20210327215047782](C:\Users\송은석\AppData\Roaming\Typora\typora-user-images\image-20210327215047782.png)



​	trim() 화이트 스페이스 삭제. // value.trim().length => .으로 연결된 메소드=> 메소드 체인이라 함

### 함수 호출 구조

​	toString() => data값을  String 타입으로 변환

​	String 타입을 String 타입으로 변환? 굳이 왜? 의미?

만약

```js
var value = new String("123");
```

을 생성하고 

```js
var oneProto = value.__proto__;
var oneString = oneProto.toString;
```

이라면, 이는 String 내장 함수, 빌트인의 toString을 실행하게 되는 것이다. 

그러나

```js
var twoProto = value.__proto__.__proto__;
var twoString = twoProto.toString;
```

여기에선, 더 아래에 있는 object의 toString을 실행하게 된다.

String 오브젝트에 toString()이 없으면 Object의 toString()이 호출되는 것이다. 

"123"을 Object 타입으로 인식하여 변환하기 때문에 String 오브젝트에 toString이 있는 것이다.

우선, 데이터 타입으로 오브젝트를 결정하고 오브젝트의 함수를 호출한다. 

만약

```js
var result = toString(123);
log(result);
```

이라면, Object 오브젝트의 toString이 호출된다. 123을 오브젝트로 간주하므로 Object 형태를 문자열로 반환하는 것이다. 그러므로 반환되는 값은 [object Undefined]가 된다. Object는 키밸류로 구성되어 있기 때문에(프리미티브밸류가 있는 다른 오브젝트와는 달리) 결과가 반환하게 될 수 없는 것이다. 그러므로 이와 같은 값이 표현되게 하지 않기 위해서 빌트인 함수에 String, Number 등과 같은 오브젝트가 있는 것이다.

정리: 단순히 var result = toString(123); 이와 같이하여 123의 값을 얻고자 한다면, 이는 123의 올바른 타입을 인식하지 못한 채 단순히 Object의  toString을 통해 결과를 반환할 것이다. 이 경우 toString은 Object의 프로퍼티를 반환하고자 할것인데, Object에는 대응하는 프리미티브밸류의 값(value)이 없으므로 [object Undefined]을 반환하게 된다.

따라서 자바스크립트는 Number, String과 같은 프리미티브밸류를 가진 오브젝트들을 제공했고, 이를 통하여 해당하는 프리미티브밸류를 toString을 통해 반환할 수 있도록 했다.

마지막으로 처음 이야기했던 "123".toString()을 함수 호출과정에 따라 되돌아보도록 한다.

"123"은 단순히 String 타입으로 존재했지만, .toString()함수가 호출되기 위하여 내부적으로 var instance = String("123")이 실행되었다고 할 수 있다. 그러므로 String 오브젝트 내에 __ proto __로  Object 오브젝트에서 복사된 내장함수를 통해 instance의 프리미티브밸류를 가져와 반환할 수 있게된 것이다.

++ 모던 자바스크립트https://ko.javascript.info/native-prototypes

=> Object 내부에 새롭게 Number, String을 만든 줄 알았는데, 그게 아니라 Number, String 함수가 Object를 상속한 것이다! 

그래서  A.__ prototype__ 에서는 String의 toString이 사용되고, A.__ prototype__ .__ prototype__ 에서는 Object의 toString이 사용된 것이다. 상속 개념으로 설명을 해주었으면 좀 더 이해가 빨랐을뻔했다ㅋ

```js
var result = toString(123);
console.log(result);//Object의 toString을 이용 => undefined

var re = "123".toString();
console.log(re);//"123"이 String 빌트인이므로 String의 toString을 이용 => 123

var rr = toString("123");
console.log(rr);//이것도 마찬가지? => undefined
```



- charAt()

  ```js
  var value = "asdf";
  value.charAt(12);//빈 문자열 반환
  value[12];//undefined 반환
  ```

- indexOf()

  왼쪽에서 오른쪽으로 검색해서 파라미터와 일치하면 인덱스 반환, 없으면 -1 반환

- lastIndexOf()

  오른쪽에서 왼쪽으로 검색

- substring() 

  시작 인덱스부터 파라미터의 직전 까지 반환

- match()

  매치 결과를 배열로 반환 / 일치가 하나의 개념이라면 매치는 다수의 개념

- replace()

  ```
  var value = "abcabc";
  value.replace("a", "바꿈"); //바꿈bcabc
  value.replace(/a/, "바꿈"); //바꿈bcabc
  value.replace(/a/g, "바꿈"); //바꿈bc바꿈bc
  ```

- search() 

  index는 하나의 조건만, search는 정규표현식 통해 복잡한 결과 반환시킬 수 있다.

- split() => 분리자로 분리하여 배열로 반환





