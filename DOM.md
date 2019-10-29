# DOM

## DOM(Document Object Model)

텍스트 파일로 만들어져 있는 웹 문서를 브라우저에 렌더링하려면 웹 문서를 브라우저가 이해할 수 있는 구조로 메모리에 올려야 한다. 브라우저의 렌더링 엔진은 웹 문서를 로드한 후, 파싱하여 웹 문서를 브라우저가 이해할 수 있는 구조로 구성하여 메모리에 적재하는데 이를 DOM이라 한다. 즉 모든 요소와 요소의 어트리뷰트, 텍스트를 각각의 객체로 만들고 이들 객체를 부자 관계를 표현할 수 있는 트리 구조로 구성한 것이 DOM이다. 이 DOM은 자바스크립트를 통해 동적으로 변경할 수 있으며 변경된 DOM은 렌더링에 반영된다.

 ![브라우저 동작 원리](https://poiemaweb.com/img/client-server.png) 

이러한 웹 문서의 동적 변경을 위해 DOM은 프로그래밍 언어가 자신에 접근하고 수정할 수 있는 방법을 제공하는데 일반적으로 프로퍼티와 메소드를 갖는 자바스크립트 객체로 제공된다. 이를 DOM API(Application Programming Interface)라고 부른다. 달리 말하면 정적인 웹페이지에 접근하여 동적으로 웹페이지를 변경하기 위한 유일한 방법은 메모리 상에 존재하는 DOM을 변경하는 것이고, 이때 필요한 것이 DOM에 접근하고 변경하는 프로퍼티와 메소드의 집합인 DOM API이다.

```
HTML 문서에 대한 모델 구성
브라우저는 HTML 문서를 로드한 후 해당 문서에 대한 모델을 메모리에 생성한다. 이때 모델은 객체의 트리로 구성되는데 이것을 DOM tree라 한다.

HTML 문서 내의 각 요소에 접근 / 수정
DOM은 모델 내의 각 객체에 접근하고 수정할 수 있는 프로퍼티와 메소드를 제공한다. DOM이 수정되면 브라우저를 통해 사용자가 보게 될 내용 또한 변경된다.
```

## DOM tree

DOM tree는 브라우저가 HTML 문서를 로드한 후 파싱하여 생성하는 모델을 의미한다. 객체의 트리로 구조화되어 있기 때문에 DOM tree라 부른다.

```
<!DOCTYPE html>
<html>
  <head>
    <style>
      .red  { color: #ff0000; }
      .blue { color: #0000ff; }
    </style>
  </head>
  <body>
    <div>
      <h1>Cities</h1>
      <ul>
        <li id="one" class="red">Seoul</li>
        <li id="two" class="red">London</li>
        <li id="three" class="red">Newyork</li>
        <li id="four">Tokyo</li>
      </ul>
    </div>
  </body>
</html>
```

 ![DOM tree](https://poiemaweb.com/img/dom-tree.png) 

DOM에서 모든 요소,어트리뷰트,텍스트는 하나의 객체이며 Document객체의 자식이다.요소의 중첩관계는 객체의 트리로 구조화하여 부자관계를 표현한다.DOM tree의 진입점은 document객체이며 최정점은 요소 텍스트를 나타내는 객체이다.

- 문서노드 : 트리의 최상위에 존재한다.
- 요소노드 : 요소 노드는 HTML요소를 표현한다.HTML요소는 중첩에 의해 부자관계를 가지며 이 부자관계를 통해 정보를 구조화한다. 어트리뷰트, 텍스트 노드에 접근하려면 먼저 요소 노드를 찾아 접근해야 한다.
- 어브티뷰트 노드 : 어트리뷰트 노드는 HTML 요소의 어트리뷰트를 표현한다. 어트리뷰트 노드는 해당 어트리뷰트가 지정된 요소의 자식이 아니라 해당 요소의 일부로 표현된다. 따라서 해당 요소 노드를 찾아 접근하면 어트리뷰트를 참조, 수정할 수 있다.
- 텍스트 노드 : 텍스트 노드는 HTML 요소의 텍스트를 표현한다.텍스트 노드는 DOM tree의 최종단이다.

 ![Element Node](https://poiemaweb.com/img/HTMLElement.png) 

## DOM Query / Traversing (요소에 접근)

### 하나의 요소 노드 선택 ![select an individual element node](https://poiemaweb.com/img/select-an-individual-element-node.png) 

**document.getElementById(id)** 

- id 어트리뷰트 값으로 요소 노드를 한 개 선택한다.
- Return: HTMLElement를 상속받은 객체
- 모든 브라우저에서 동작

**document.querySelector(cssSelecotor)**

- CSS셀렉터를 사용하여 요소 노드를 한개 선택한다.
- Return : HTMLElement를 상속받은 객체
- IE8 이상의 브라우저에서 동작

**아래는 `ul`에 접근하여 직접적으로 조작하는 코드이다**

```html
<!DOCTYPE html>
<html lang="ko">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Document</title>
</head>
<body>
  <ul id="myId" class="class1 class2" style="color:red">
    <li>html</li>
    <li>css</li>
    <li>javascript</li>
  </ul>
  <script>
    const $ul = document.querySelector("#myId");
    $ul.style.color = 'blue'; //ul의 색을 blue로 변경
    console.log($ul.className)
    console.log($ul.classList.add('class3')) //class3를 추가함
    console.log($ul.classList.remove('class3')); //class3를 지움
  </script>
</body>
</html>
```

### 여러개의 요소 노드 선택

 ![select multiful elements](https://poiemaweb.com/img/select-multiful-elements.png) 

**document.getElementsByClassName(class)**

- class 어트리뷰트값으로 요소 노드를 모두 선택한다.
- Return : HTML.Collection (live)
- IE9 이상의 브라우저에서 동작

**document.querySelectorAll**

- 지정된 CSS선택자를 사용
- Return:NodeList(non-live)
- IE8이상의 브라우저에서 동작

```
// querySelectorAll는 Nodelist(non-live)를 반환한다. IE8+
const elems = document.querySelectorAll('.red');

// 배열메소드들이 더 다양하기 떄문에 배열로 변경하여 사용하면 좋다.
[...elems].forEach(elem => elem.className = 'blue');
```

### DOM Traversing (탐색)

 ![traversing](https://poiemaweb.com/img/traversing.png) 

**firstChild,lastChild**

- 자식 노드를 탐색한다
- Return : HTMLElement를 상속받은 객체
- IE9 이상의 브라우저에서 동작

```
const elem = document.querySelector('ul');

// first Child
elem.firstChild.className = 'blue';
// last Child
elem.lastChild.className = 'blue';
```

**previousElementSibling,nextElementSibling**

- 형제 노드 중에서 Element type요소만을 탐색한다.
- Return : HTMLElement를 상속받은 객체
- IE9이상의 브라우저에서 동작

```
const elem = document.querySelector('ul');

elem.firstElementChild.nextElementSibling.className = 'blue';
elem.firstElementChild.nextElementSibling.previousElementSibling.className = 'blue';
```

## DOM Manipulation(조작)

### 텍스트 노드에 접근/수정

 ![nodeValue](https://poiemaweb.com/img/nodeValue.png) 

**nodeValue**

- 노드의 값을 반환한다.
- Return : 텍스트노드의 경우는 문자열,요소 노드의 경우 null반환
- IE6이상의 브라우저에서 동작한다.

### 어트리뷰트노드에 접근/수정

 ![nodeValue](https://poiemaweb.com/img/nodeValue.png) 

**classList**

- add,remove,item,contains,replace 메소드를 제공한다.
- IE10 이상의 브라우저에서 동작한다.

**hasAttribute(attribute)**

- 지정한 어트리뷰트를 가지고 있는지 검색
- Return:Blooean
- IE8 이상의 브라우저에서 동작한다.

**getAttribute(attribute)**

- 어트리뷰트의 값을 취득한다.
- Return : 문자열
- 모든 브라우저에서 동작한다\

**setAttribute(attribute,value)**

- 어트리뷰트와 어트리뷰트 값을 설정한다.
- Return : undefined
- 모든 브라우저에서 동작한다.

**removeAttribute(attribute)**

- 지정한 어트리뷰트를 제거한다.
- Return : undefined
- 모든 브라우저에서 동작한다.

### HTML콘텐츠 조작

 ![innerHTML](https://poiemaweb.com/img/innerHTML.png) 

**innerHTML**

- 해당 요소의 모든 자식 요소를 포함하는 모든 콘텐츠를 하나으 ㅣ문자열로 취득할 수 있다.이 문자열은 마크업을 포함한다.

