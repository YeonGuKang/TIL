# 3일차 - Vanila JS로 Javascript의 기본을 배우다.

자바스크립트에 대한 개념이 거의 없기때문에 이참에 가장기본인
바닐라 자바스크립트로 자바스크립트의 개념을 확립해보았다.

가장 기초인 변수부분부터 기초를 잡았는데,
항상 궁금했던 let과 var의 차이를 이제야 깨달을 수 있었다. 참고로 const와 let을 ES6문법으로
var이 가지고 있던 여러가지 단점을 보완하기 위해서 나왔다고 한다.

**const - 상수 , 도중에 변수의 값을 수정할 수 없다
let - 도중에 변수의 값을 수정할 수 있다.**

**var - let과 동일하지만 변수가 도중에 다시 선언되는것을 잡아내지 못한다.
즉 let은 중간에 다시 선언되는것을 잡아낸다.**

**Array - [] 우리가 익히 알고있는 배열과 같다. 하지만 딱히 배열선언을
해줄필요없이 그냥 []안에 값을 넣으면 배열이된다.**

ex) const daysOfWeek = ["Mon", "Tue", "Wed", "Thu"];

3번째 값을 알고싶을때 daysOfWeek[2] C언어와 같다.

**Object - {} 일반적인 배열과 다른 배열이다. 일반적인 배열은 그냥 값을 나열하지만
Object는 각 value에 이름을 줄 수 있다. 마치 하나의 객체와 비슷하다고 생각하면된다.**

```
ex ) const yeonguinfo ={
	name: "Yeongu",
	age:24,
	gender: "Male",
	isHandsome:true
}

console.log(yeonguinfo.isHandsome);
```

이런식으로 value의 이름으로 값을 읽어올 수 있다.
console도 하나의 오브젝트다. log는 console안에 존재하는 함수

### html의 객체로 자바스크립트로 넘기는 개념 - DOM

html에 id를 주어서 그 id를 토대로 자바스크립트에서 control

```
ex) <h1 id="title">This works!</h1> - html

#title{
~~~
} - CSS

const title = document.getElementById("title"); - JS
title.innerHTML = "Hello"; -JS

```

Document 객체는 웹 페이지 그 자체를 의미합니다.

웹 페이지에 존재하는 HTML 요소에 접근하고자 할 때는 반드시 Document 객체부터 시작해야 한다.

document.getElementById(아이디).onclick = function(){ 실행할 코드 }


document.querySelector("#아이디") - 해당 아이디를 가진 첫번째 엘리멘트에만 해당한다.


아래는 html에 존재하는 title이라는 id의 객체를 클릭했을때 색을 바꾸는 자바스크립트 코드다.
```
const title = document.querySelector("#title");

function handleClick(){
	title.style.color = "blue";
}

title.addEventListener("click", handleClick);
```

마우스클릭 이벤트 핸들러.

자바스크립트에서는 "" '' 둘다 그냥 같은 string이다.

test.event("test", function()); 과 test.event("test", function); 의 차이는
event 에 상관없이 전자는 fuction이 호출되고 후자는 event가 있을때만 호출을 한다.

==과 ===의 차이

==은 두 피연산자의 유형이 상관없이 비교가능
하지만 === 두 피연산자의 유형까지 비교한다

ex) 0 == falese -> true
0 === false -> false

우리는 자바스크립트에서 html의 class name을 바꿈으로써 함수의 기능을 줄 수 있다.
아래는 classname을 바꿈으로써 css적용 또한 바뀌게해서 색을 바꿔주는 예의 코드이다.

 <h1 id="title" class="btn">This works!</h1> - html 코드
 title id를 가졌으며 class로 현재 btn을 가졌다.
 
 
 JS코드
 
 ```
 const title=document.querySelector("#title"); // title id를 가진 첫번째 element를 title로 const선언

const CLICKED_CLASS = "clicked"; // clicked로 변화를 주기위한 변수 선언

// 클릭이 있었을 때 실행
function handleClick(){ 
  const hasClass = title.classList.contains(CLICKED_CLASS); // 클릭했을 때 클래스가 clicked인지 판단을 위한 변수 선언

  if(!hasClass){ // 클래스가 clicked가 아니면
    title.classList.add(CLICKED_CLASS); // 클래스에 clicked를 추가하여 css값으로 변하게 해줌 아래 clicked css참고할것
    
  }else { // 이미 클래스가 clicked인 경우 clicked를 클래스에서 뺌으로써 css적용을 막음
    title.classList.remove(CLICKED_CLASS);
  }
}

// 클릭 event를 위한 함수 선언
function init()
{
title.addEventListener("click", handleClick ); // title의 클릭 이벤트처리

}
init();
```

CSS 파일 -

```
.btn{
  cursor: pointer;
}

.clicked{ // 클래스가 clicked면 색을 red로 바꿈 clicked가 아닌 클래스면 이를 적용하지 않는다는 소리
이를 이용해서 title의 색을 계속 바꿔나간다.
  color: red;
}

```

**이처럼 html , css , javascript가 셋이서 함께 작용할 수 있는 간단한 방법을 알아보았다. 
이전에는 정말 세가지가 함께 함수로 움직이고 변수로 움직이는게 막막했는데 조금씩 이해가 가기 시작했다. 
곧 백엔드와 프론트엔드를 연결할 수 있을것 같다. 빨리 둘을 연결해서 원하는 웹페이지를 마음껏 만들어나가고 싶다.**
