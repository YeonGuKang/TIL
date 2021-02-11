# 4일차 - JS에 대해 더 배우다

자바스크립트에서 html을 다루는 좀 더 세부적인 부분에 대해서 배워보았다.


아래 코드는 자바스크립트에서 직접 element를 만들어서 이미 존재하는 html 엘레멘트에 추가하는 코드이다.
이를 활용하면 event가 있을경우 element를 보여주게 하도록 만들 수 있다.

```
const toDoForm = document.querySelector(".js-toDoForm"),  // html에 존재하는 js-toDoForm의 id를 가져옴
  toDoInput = toDoForm.querySelector("input"),  // toDoForm에 input type을 가져옴
  toDoList = document.querySelector(".js-toDoList"); 
  
const TODOS_LS = "toDos"; // TODOS_LS 
const toDos = [];   // toDO list를 위한 배열을 선언해줌 (객체들을 모아놓을 배열임)


function saveToDos() {
// local저장소에 저장을한다. 로컬 저장소는 모든걸 string으로 저장해야하기에 stringify로 모든 객체 정보를 string화 한다.
  localStorage.setItem(TODOS_LS, JSON.stringify(toDos));
}


function paintToDo(text) {
  // createElement - JS에서 html의 element를 직접만드는 코드이다
  const li = document.createElement("li");  // li를 만들고
  const delBtn = document.createElement("button"); // button을 만들었다.
  const newId = toDos.length + 1; // 각자 li에 ID를 준다. li의 식별을 위해서.
  delBtn.innerText = "❌"; // 버튼에 text를 추가해줌
  const span = document.createElement("span"); // span도 만들었다.
  span.innerText = text;  // span에도 text를 추가해줌
  li.appendChild(delBtn); // li에 그 버튼을 자식으로 추가해줌
  li.appendChild(span); // 역시나 li에 span을 자식으로 추가해줌
  li.id = newId;
  toDoList.appendChild(li); // 이제 그 통합 li를 이미 html에 존재하는 toDoList에 추가해준다. 이렇게 함으로써 event가 있을경우에 html에 보여주는 element가 달라진다.
  
  //  toDo 배열에 넣을 객체를 만든다
const toDoObj = {
    text: text,
    id: newId
  };
  toDos.push(toDoObj); // toDos 배열에 방금 만든 객체를 집어 넣는다
  saveToDos();
  }
  
// submit의 event가 감지되면 
function handleSubmit(event) {
  event.preventDefault(); // 페이지가 reset되는등 자동으로 실행되는 event를 방지한다.
  const currentValue = toDoInput.value; // Input value를 저장해주고
  paintToDo(currentValue); // 그 value를 함수로 넘겨준다
  toDoInput.value = ""; // 그 뒤에 value를 초기화 해줌으로써 display되는 value를 없앤다 ( 엔터를 눌렀을 때 보여지는게 사라짐)
  
  }

// 저장한 ToDos를 불러오는 함수
function loadToDos() {
  const loadedToDos = localStorage.getItem(TODOS_LS);
  if (loadedToDos !== null) {
    const parsedToDos = JSON.parse(loadedToDos); // parse는 아까 string으로 바꾼 객체 정보를 다시 객체로 바꾼다.
    parsedToDos.forEach(function(toDo) { // forEach를 이용해 각각의 toDo 배열 요소들에 대해서 함수를 실행한다.
      paintToDo(toDo.text);
    });
  }
  
  
  function init() {
  loadToDos();
  toDoForm.addEventListener("submit", handleSubmit);
}

```

이번에는 math를 이용해서 내가 가지고 있는 사진을 랜던으로 보여주는 코드이다.

```
const body = document.querySelector("body");

const IMG_NUMBER = 3; // 이미지의 총 개수를 저장해준다

function paintImage(imgNumber) {
  const image = new Image();
  // 생성된 랜덤숫자로 랜덤한 이미지를 
  image.src = `images/${imgNumber + 1}.jpg`; // 이미지 이름은 1.jpg , 2.jpg , 3.jpg ... 이다.
  image.classList.add("bgImage");
  body.prepend(image);
}

// 랜덤한 숫자를 만들어주는 함수
function genRandom() {
// math함수를 이용하여 랜덤 값을 생성한다. floor = 버림 , random = 랜덤한 숫자생성 
  const number = Math.floor(Math.random() * IMG_NUMBER);
  return number;
}

function init() {
  const randomNumber = genRandom();
  paintImage(randomNumber);
}

init();

```


# react에 대해서

react는 일단 virtual DOM이다 JS에서 html문법으로 작성을 하면
그것이 실제 html문서에는 적용되진 않지만 웹페이지 내에서는 적용이
되어있다. 따라서 이를 virtual DOM이라고 부른다. 아래는 예시 코드이다.

```
import React from 'react';

function App() {
	// 현재 js폴더에서 html 형태로 코드를 작성했다
	// component가 html을 리턴하는 형태
  return <div>hell</div>;
   
}

export default App;
```

이는 페이지에 들어가면 적용이 되어있다. 하지만 메인페이지의 html 문서를 들어가면

<div id="root"></div> 이런식으로 hell은 작성되지 않았다.

그런데 여기서 index.js 파일을 보면 아래에 root id로 DOM을 불러온것을 확인할 수 있다.
이처럼 이미 DOM이 실행되었고, html문서에는 보이지 않지만 홈페이지에서는 수정이 되는것이다.
이런식으로 눈에 보이지않는 DOM이라서 virual DOM의 동작을 하는것이 react이다.

```
import React from 'react';
import ReactDOM from 'react-dom';
import App from './App';

ReactDOM.render(
// component이다 component는 html을 반환하는 함수이다.
  <React.StrictMode>
    <App />
  </React.StrictMode>,
    document.getElementById('root')
);

```

component는 html처럼 작성하려고 할떄 필수로 필요하다.
이런 자바스크립트와 html의 조합을 jsx이라고 부른다.

import React from "react";
react를 사용할때 꼭 위에 선언해주어야한다. 그렇지 않으면 component를 사용할 수 없다

아래는 jsx를 사용하는 예시이다

```
Potato.js -
// 리액트를 사용하기위해 import
import React from "react";

// html함수를 return하는 함수를 만든다.
function Potato(){
    return <h3>I love potato</h3>;

}

// 이 component를 사용하기 위해서는 사용할곳에서 import를 해야하기떄문에
꼭 export를 해주어야한다.
export default Potato;
```


App.js -

```
import React from 'react';
import Potato from "./Potato"; // Potato를 import받아서 사용

function App() {
  return <div>
    <h1>hello</h1>
    <Potato /> // hello 아래에 Potato가 그대로 적용된다
  </div>
   
}

export default App;

```

아래처럼 App.js에 직접 함수를 정의해서 사용할 수 있다.

```
import React from 'react';


function Potato() {
  return <h1>I like potato</h1>;
}

function App() {
  return <div>
    <h1>hello</h1>
    <Potato /> // Potato component를 사용
  </div>
   
}

export default App;

```

이번엔 arg인자에 props가 들어오는 아주 신기한 기능에 대해서 다룬다.
아래 Food객체를 props로 받아서 log를 찍어보면 객체 정보가 그대로 찍힌다.
이는 arg로 쉽게 반환이 되었음을 뜻한다.
정확히 props는 component에 넣게되는 모든것을 뜻한다.
<Food 이 사이에 들어가는 모든것이 props다 />
이 props는 Food의 첫번째 argument로 들어간다. 핵심이다.

```
function Food(props) {
  console.log(props);
  return <h1>I like potato</h1>;
}

function App() {
  return <div>
    <h1>hello</h1>
// 보다 싶이 Food component 객체는 여러 정보를 담고 있다.
    <Food 
    fav="kimchi"
    somthing={true}
    papapapap={["hello",1,2,3,4,true]}
     />
  </div>
   
}

```

```
이 장점을 이용해서
function Food(props) {
아래처럼 props의 fav에 접근할수 있다. 결과는 kimchi
  console.log(props.fav);
  return <h1>I like potato</h1>;
}

function App() {
  return <div>
    <h1>hello</h1>
// 보다 싶이 Food component 객체는 여러 정보를 담고 있다.
    <Food 
    fav="kimchi"
    somthing={true}
    papapapap={["hello",1,2,3,4,true]}
     />
  </div>
   
}

```

더욱 놀라운것은 이런식으로도 응용이 가능하다는 것이다.
역시나 결과는 I like Kimchi

```
function Food({fav}) {
  return <h1>I like {fav}</h1>;
}

function App() {
  return <div>
    <h1>hello</h1>
    <Food 
    fav="kimchi"
     />
  </div>
}

```

아래 예시대로 수정하면 I like하고 믿에 선언한 모든 음식들이 쭉 찍힌다
총 4줄이 찍힌다는 소리다 AWESOME!!
하지만 이는 정적데이터라는 단점이 존재한다. 아래에 동적데이터에 대해서 다루겠다.

```
function Food({fav}) {
  return <h1>I like {fav}</h1>;
}

function App() {
  return <div>
    <h1>hello</h1>
    <Food  fav="kimchi"/>
    <Food  fav="ramen"/>
    <Food  fav="samgiopsal"/>
    <Food  fav="chukumi"/>
  </div>
}

```

일단 map에 대해서 다루겠다. map은 array에 저장된 정보들을
하나하나 function을 실행할 수 있는 강력한 함수이다.
아래 예시 코드를 들겠다.

const friends = ["dal", "mark", "lynn", "japan guy"];

map으로 friends의 요소 하나하나 함수를 실행한다.
그 결과 하나하나 요소에 good이 붙어서 찍히게된다.

```
friends.map(function(friend){
	return console.log(friend + "good");
})

```
자 이제 위에 공부한 정보들을 토대로 동적으로
프로그래밍한 코드를 아래 나열하겠다.


이번에는 두개의 props를 가지므로 두개를 불러와서 사용한다.

```
function Food({ name, picture }) {
  return (
    <div>
      <h2>I like {name}</h2>
      <img src={picture} alt={name} />
    </div>
  );
}
```

음식들의 정보를 담고 있는 배열을 선언한다
id값은 key값을 위해 필수로 지정해주어야한다

```
const foodILike = [
  {
    id:1,
    name: "Kimchi",
    image:
      "http://aeriskitchen.com/wp-content/uploads/2008/09/kimchi_bokkeumbap_02-.jpg"
  },
  {
    id:2,
    name: "Samgyeopsal",
    image:
      "https://3.bp.blogspot.com/-hKwIBxIVcQw/WfsewX3fhJI/AAAAAAAAALk/yHxnxFXcfx4ZKSfHS_RQNKjw3bAC03AnACLcBGAs/s400/DSC07624.jpg"
  },
  {
    id:3,
    name: "Bibimbap",
    image:
      "http://cdn-image.myrecipes.com/sites/default/files/styles/4_3_horizontal_-_1200x900/public/image/recipes/ck/12/03/bibimbop-ck-x.jpg?itok=RoXlp6Xb"
  },
  {
    id:4,
    name: "Doncasu",
    image:
      "https://s3-media3.fl.yelpcdn.com/bphoto/7F9eTTQ_yxaWIRytAu5feA/ls.jpg"
  },
  {
    id:5,
    name: "Kimbap",
    image:
      "http://cdn2.koreanbapsang.com/wp-content/uploads/2012/05/DSC_1238r-e1454170512295.jpg"
  }
];

```

위에서 공부한 map을 토대로 보면 처음 실행에서 dish에는 김치와 김치의 이미지 정보가 들어있다.
그 정보를 Food의 함수에 props를 넘겨주어서 출력을한다.
map의 특성대로 이 과정을 foodLike의 모든 인자에 대해서 진행한다.
따라서 foodILike가 가지고 있는 모든 인자의 정보가 찍히게 된다. 

```
function App() {
  return <div>
    {foodILike.map(dish => (
        <Food name={dish.name} picture={dish.image} />
      ))}
  </div>
}

```
react에는 propTypes이라는 것이 존재한다. 이는 우리가
올바른 props을 넘겨주었는지, 값을 가지고있는지 확인할때 유용하다.
아래는 예시코드이다.

만약 name,picture이 string이 아니거나 rating이 nuber이 아니면 오류를 알려준다.
또한 뒤에 isRequired는 값을 무조건 가져야 한다는 뜻으로 값이 없는경우에 오류를 알려준다.

```
Food.propTypes = {
  name: PropTypes.string.isRequired,
  picture: PropTypes.string.isRequired,
  rating: PropTypes.number.isRequired
};

```

아주 많이쓰이는 ES6의 화살표함수에 대해서 잠깐 알아보자
아래는 화살표함수의 예시 코드이다.

```
// 이 문장은 배열을 반환함: [8, 6, 7, 9]
elements.map(function(element) {
  return element.length;
});

// 위의 일반적인 함수 표현은 아래 화살표 함수로 쓸 수 있다.
elements.map((element) => {
  return element.length;
}); // [8, 6, 7, 9]

```
