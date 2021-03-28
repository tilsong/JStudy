자바스크립트 오브젝트

- 오브젝트 구분
  - 빌트인 오브젝트(Built-in Object)
  - 네이티브 오브젝트(Natice Object)
  - 호스트 오브젝트(Host Object)

- 빌트인 오브젝트
  - 사전에 만들어놓은 오브젝트 => 빌트인 Number 오브젝트, String 오브젝트 포함 11개
- 네이티브 오브젝트
  - js스펙에서 정의한 오브젝트 
  - 빌트인 오브젝트 포함, 여기에 js 코드를 실행할 때 만드는 오브젝트 ex) Argument 오브젝트
- 호스트 오브젝트
  - 빌트인, 네이티브 오브젝트를 제외한 오브젝트 ex) window, DOM오브젝트
  - js는 호스트 환경에서 브라우저의 모든 요소 기술을 연결하고 융합하며 이를 제어



- 오브젝트와 인스턴스 

  - var abc = new Object();  => 인스턴스, 실체 있음

  - var obj ={}; => 오브젝트, 실체는 없음

    

- 프로퍼티 리스트

![image-20210328002824066](C:\Users\송은석\AppData\Roaming\Typora\typora-user-images\image-20210328002824066.png)

es3 => 인스턴스 만든 모든 오브젝트에 6개 함수 모두 포함됨

new Object

```js
    var newNum = new Number(123);
    console.log(typeof newNum); //object
    console.log(newNum + 100); //223 , primitive 값으로 계산됨(Number오브젝트이므로)


    var nNum = new Object(123);
    console.log(typeof nNum); //object 
    console.log(nNum + 100); //223 => "new" Object(123)의 형태로 생성자 호출하면, 매개변수의 타입에 따라 해당하는 인스턴스를 생성한다.

    //파라미터 작성x
    var num = new Object();
    console.log(num); //{}  => 이는 undefined를 작성한 것과 같다. 따라서 값을 갖지 않은 Object 인스턴스를 생성함
```

---



참고 =>  https://webclub.tistory.com/38

Object와 Object()의 차이?

- Object()는 new Object와 같다. 

  ```js
  // 빌트인 Object 객체를 obj1에 할당, 여기에는 prototype: Object가 있다.
  var obj1 = Object;
  console.dir(obj1);
  
  // Object()로 새로운 Object를 생성하여 obj2에 할당, 여기에는 __proto__:Object가 있다.  prototype: Object을 복사한 것.
  var obj2 = Object();
  console.dir(obj2);
  ```

  https://medium.com/%EC%98%A4%EB%8A%98%EC%9D%98-%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D/%EC%9E%90%EB%B0%94%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8%EC%97%90%EC%84%9C-object-object-%EA%B0%80-%EB%8C%80%EC%B2%B4-%EB%AD%98%EA%B9%8C-fe55b754e709 도 참고

---

Object()

- new를 쓰지 않은 것.

- ```js
  var obj = Object({name:"JS"}); //var obj = {name: "js"}  같음
  console.log(obj) //{name:"JS"} => 파라미터 입력? Object 인스턴스 생성
  							
  
  var emptyObj = Object();
  console.log(emptyObj) //{}
  ```

  => 파라미터를 작성하지 않으면 new Object()와 같다.



Object 생성 방법

- var abc ={};
  - var abc = Object()와 같음
  - 즉, var abc = {}를 실행하면 Object 인스턴스가 생성됨
- {} 표기를  오브젝트 리터럴이라고 부름

- Object()와 Object 리터럴{} 모두 Object 인스턴스를 생성한다. 그래서 {}를 쓴다.. 왜 나중에 알려주는 거야 힘들게 ㅠㅠㅠ

  var obj = {name: "js"} 이렇게!! 만든다고 함!!

valueOf()

- data 위치에 작성한 Object 인스턴스의 프리미티브 값 반환.

  ```js
  var obj = {key: "value"};
  log(obj.valueOf());//{key: "value"}
  ```

  











