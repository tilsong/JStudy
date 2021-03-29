-  live NodeList와 static Node

  배열과 유사해보이지만, 컬렉션(Collection)타입의 객체이다.

  이는 또한 live NodeList와 static NodeList로 나뉘는데, 대부분 live NodeList이고, querySelector로 시작하는 메서드들이 정적 노드리스트 객체를 반환한다. 라이브 노드리스트는 스크립트를 이용하여 페이지를 수정할 때는 NodeList 객체의 요소들도 동시에 수정된다.  그러나 정적 노드리스트 객체를 이용하여 페이지를 수정하면, 스트립트에 의한 변경의 영향을 받지 않는다. 이들은 쿼리가 실행되는 시점의 문서구조를 반영하고, 스크립트로 인해 페이지의 내용이 변경되면 NodeList 객체는 이 변경 사항을 반영하지 않는다.

  - 무슨 말일까? 검색을 해보았다 => https://im-developer.tistory.com/110

  ```js
  const $li = document.querySelectorAll('.list li'); //NodeList객체로 반환
  const $li = document.querySelector('.list').children; //HTMLCollection객체로 반환(라이브객체)
  
  ```

  >
  >
  >### **HTMLCollection**
  >
  >HTMLCollection **인터페이스는 요소의 문서 내 순서대로 정렬된 일반 컬렉션**을 나타내며 NodeList와 마찬가지로 **유사 배열**이다. HTMLCollection은 현대적인 DOM의 이전 세대부터 존재하던 구성요소로 element.children과 같은 속성 또는 
  >
  >document.getElementsByClassName(), document.getElementsByTagName()과 같은 메소드에 의해 반환된다. HTMLCollection은 모두 문서가 바뀔 때 실시간으로 업데이트되는 **라이브(Live) 콜렉션**이다.

  그런데 이와 같이 live컬렉션의 내용을 수정하면, 문제가 발생할 수가 있다.

  ```js
  const $li = document.getElementsByClassName('txt-blue');
  for (let i = 0; i < $li.length; i++) {
  $li[i].className = 'txt-red';
  }
  ```

  이와 같이 태그를 변경하려 했을때 , li는 3개 다 바뀌지 않고, 앞과 뒤만 바뀌게 된다. 이는 getElementsByClassName 메소드가 dom의 변경사항을 실시간으로 반영하는 Live Collection이기 때문이다. txt-blue에서 txt-red로 변경하는 순간, 변경된 txt-blue는 삭제되고, 다음 i를 찾을 때 인덱스가 하나씩 앞으로 가게 되기 때문에 그렇다. 블로그에 기록된 설명사진을 보자.

![img](https://blog.kakaocdn.net/dn/bCgOnI/btqv7ZQDu7A/uTFyHvmstMdaabiuKdbNk1/img.png)

이러한 문제는 어떻게 해결될 수 있을까?

1. 루프를 돌릴 때, class명을 txt-red로 바꾼 후 i 변수를 1 감소시킨다.

   ```js
   const $li = document.getElementsByClassName('txt-blue');
   for (let i = 0; i < $li.length; i++) {
   	$li[i].className = 'txt-red';
   	i--;
   }
   ```

   이 경우 모든 요소를 바꿀 수 있으나, 반복문 종료 후 $li를 출력하면 모든 요소가 제거된 상태이다. 

   반대로 뒤부터 값을 변경하는 방법도 있으나, 이 또한 $li의 모든 요소가 제거된다는 점은 동일하다.

   

2. 정적인 컬렉션(Static Collection)으로 반복을 실행한다.

   > document.querySelectorAll() 메소드로 반환되는 NodeList는 정적 컬렉션으로
   >
   > 변경 사항이 실시간으로 반영되지 않기 때문에 우리가 원하는 대로 동작한다.
   >
   > 이 경우, 반복문이 종료된 후에도 $li에는 원래의 요소가 그대로 존재하며
   >
   > 단지 클래스명만 바뀐 상태로 저장되어있다.

   ```js
   const $li = document.querySelectorAll('.txt-blue');
   for (let i = 0; i < $li.length; i++) {
   	$li[i].className = 'txt-red';
   }
   ```

   그렇다. 이 경우 querySelector(All)문을 사용해주게 되면, 이는 정적 컬렉션의 노드리스트를 반환하기 때문에 반복문이 종료된 후에도 $li의 원래 요소가 삭제되지 않고 그대로 존재한다. 

   다만 클래스명만 변경되어 저장되어 있다.

많이 돌아왔다. 

결론적으로 말하자면 live NodeList는 스크립트가 읽혀지는 즉시 실행되기 때문에 빠르지만, 그렇기 때문에 위와 같이 원하는 결과를 가져오지 못하게 될 수도 있다. 따라서 위와 같이 값을 변경하는데 사용하는 것은 지양해야겠다는 생각이 들었다. 

한편으로 static NodeList는 live NodeList에 비해 (매우) 조금은 늦을 수 있지만, 쿼리가 시행되는 시점에서 문서구조를 반영하기 때문에 보다 적은 오류를 발생시킬 수 있을 것이라는 생각이 들었다. 

정리: 

​	live Collection의 배열을 반복문을 통해 변경할 때 오류가 발생할 수 있다. 따라서

​	요소를 선택하거나 값 추가할 때 => live NodeList, 즉 getElementById, getElementsByClassName, getElementsByTagName

​	요소의 값을 변경해야할 때 => static NodeList, 즉 querySelector, querySelectorAll

​	로 정리해서 사용하는 것이 좋겠다. (사실 위 경우 아니면 크게 상관없을 것 같기도 하다^^)
