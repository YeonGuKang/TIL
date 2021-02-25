# 5일차 - react 심화과정

이번에 프로젝트를 진행하면서 firebase를 사용하고싶었고, firebase를 react로
쉽게 구현한 강의가 있어서 그 강의를 따라가다보니 react를 자연스럽게 접하게되었다.
처음에 front쪽을 html과 css 그리고 javascript로 작업을했고 만족할만큼 결과물을 만들었다.
그 뒤에 backend작업을 시작했는데 아까 말했듯이 자연스럽게 react를 사용하며 JS로 작업을 하였다.
모든 작업을 끝내고 front와 연결을 할려니 여러가지 문제가 존재했다. 일단 VDOM인지라 우리는
JS에 코드를 작성하고 html은 껍데기일 뿐이였다. 하지만 아까 말했듯이 html작업은 이미 끝냈고
이를 해결하려 정말 많은 노력을 하였다. 결론은 html코드를 그대로 JS DOM코드로 바꾸는 것이였다.
여기까지는 괜찮았다. 금방 코드를 옮기고 맞게 코드를 바꿨지만 문제가 바로 생겼다. 바로 메인페이지는 OKAY
그러나 html처럼 페이지를 이동해가며 원하는 front를 보여주는것이 react에는 존재하지 않았다.
이게 무슨말이냐. react는 SPA로 Single Page Application에 특화돼있는 언어라는것을 이제야 깨달은 것이다.
하지만 여기서 프로젝트를 엎고 다시 다른 언어를 쓰자니 너무 아쉬웠고 힘들어서 어떻게든 정보를 찾고
머리를 굴렸다. 여기서 나와같은 고민을 한 사람이 많다는것을 알았고 Router가 그 해결책을 준다는것을 알았다.
그래서 바로 Router에대해 공부를 했고 결과는 성공적이였다.

아래 코드를 예시로 들으며 설명을 하도록 하겠다.

App.js -

아래에 <BrowserRouter>로 묶어줌으로써 이 안에서만 저 코드가
실행되도록 한다. 그 말은 즉슨 BrowserRouter은 프로젝트에서 통틀어서
여기에 하나만 존재하고 여기서만 모든 Router를 뿌려준다는 소리다. 이점을 헷갈려서
나는 route가 필요한 모든 부분에서 이를 해결하려고 하였고 매번 계속 오류가 났다.
하지만 이점을 깨닫고 한곳에서 route를 뿌려주니 이점이 해결되었다.
아래 Route는 path가 저 string일 경우에 component에 맞게 해당 JS가 보여지도록 해준다.
path가 / 즉 루트인 경우에는 MainPage.js 를 보여주고 /Loginform일 경우에
Loginform.js를 보여준다.

```
function App() {

  return(
    <BrowserRouter>
     <Route path="/" component = {Mainpage} exact />
     <Route path="/Loginform" component ={Loginform} />
            
  </BrowserRouter>

  );
  }  


export default App;
```

Mainpage.js-
여기서 더욱 AWESOME한 부분은 Router가 알아서 호출이 된다는 점이다.
이점은 정확하진 않지만 Mainpage에서 Link to를 이용하여 url을 바꿔주는 즉시
Router가 호출이 되어 Loginform.js를 보여준다는 점이다. 이점은 정말 너무너무 대단한것같다.
```
  <div className="login">
                                  
                              <Link to="/Loginform">
                                     <li>로그인</li>
                                </Link>
                               
                              </div>
```


그리고 react에 기본으로 구성되었는 필수요소들이 존재한다. 현재 안것으로는
index.js , index.html , App,js 이 세개는 필수로 존재해야하는 것으로 보인다. 파일들의
이름을 바꿔보고 기본 render위치를 바꿔보는등 해볼때 오류가 생긴 파일들이다.
index.html은 무조건 여기서 html이 로드된다. 따라서 VDOM은 무조건 index.html에서 이루어진다.
이와 마찬가지로 index.js 이것도 무조건 여기서 html VDOM이 여기서 실행된다. 그리고 이건 확실하진 않지만
reder역시 무조건 App.js로 넘겨줘야하는것으로 보인다. 따라서 이 셋은 필수요소로 현재 확인된다.
