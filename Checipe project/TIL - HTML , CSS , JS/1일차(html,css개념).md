# 1일차 - HTML 과 CSS의 기초에 대해 알아가다

**이전에 웹페이지를 수업으로 제작한적이 있었지만 이는 JAVA를 이용한 Spring Frame Wokr였고 이번에 하는 프로젝트는 HTML과 CSS를 통해 제작을 해야했기 때문에 새로 공부를 시작했다.**

**일단 기초적인 코드를 따라가며 공부를 했다.**

 ``` <!DOCTYPE html>``` \
**문서처음에 이 언어는 html임을 알려주는 선언**

```<link href="style.css" rel="stylesheet" type="text/css" />``` \
**스타일을 불러오는 문장 css파일과 html파일을 연결해준다. head에 선언해야하는 필수적인 선언**

**hef - 파일의 위치
rel ,type - 어떤 타입인지 말함
meta - 정보를 알려주는 문장 주석같은 존재**

**class="box" 속성 - css 스타일링을 위한 문장 class를 지정해둔뒤 그 class에 대한 설정을 css로 해준다. 간편한 유지보수를 위해 필수적으로 해줘야함.**

 ```<p> ```  **- 한문단을 나타냄**\
 ```<img src="" /> ``` **- 이미지 불러오는 태그**\
 ```<video src="" controls /> ``` **- 비디오 불러오는 태그**\
 ```<a href="">~</a> ``` **- ~를 누르면 ""로 이동하는 링크**\
 ```<a href="" target="_blank">~</a>  ``` **- ~를 누르면 ""로 이동하는 링크 (새창으로 띄움)**\
```
<ul>
            <li><a href="http://brackets.io">Brackets.io</a></li>
            <li><a href="http://blog.brackets.io">Brackets 팀 블로그</a></li>
            <li><a href="https://github.com/adobe/brackets">Brackets 깃허브</a></li>
            <li><a href="https://brackets-registry.aboutweb.com">Brackets 확장 저장소</a></li>
            <li><a href="https://github.com/adobe/brackets/wiki">Brackets 위키</a></li>
            <li><a href="https://groups.google.com/forum/#!forum/brackets-dev">Brackets 개발자 메일 주소</a></li>
            <li><a href="https://twitter.com/brackets">@brackets 트위터</a></li>
            <li>IRC의 Brackets 개발자와 채팅 <a href="http://webchat.freenode.net/?channels=brackets&uio=d4">Freenode의 #brackets</a></li>
        </ul>
 ```

**목록을 나열하면서 url 링크를 연결한 예시**


**<div> </div> 영역나누기 보통 클래스(css)로 꾸며서 영역을 나눔 **
**<div class="">~</div> 이런식으로 사용**

**<span></span>도 같은경우인데 이경우에는 글씨만 해당 div는 영역을 해당**


**<input type="text" /> 인풋태크 - 로그인, 검색등을 위한 기본적인 텍스트 인식**
**<input type="checkbox" />**

**<textarea></textarea> - 여러문장을 받는 창**

**<select> </select> -마우스로 선택하는 폼**

**<form> </form> - 로그인창 만드는 폼**

**radio - 하나만 선택가능**
**checkbox - 여러개 선택가능**

**width -가로**
**height - 세로**

# CSS 파트

```
.nav {
        height: 70px; - 픽셀크기 설정
        border-bottom: 1px solid black; - 아래쪽 테두리 설정
        display: flex; - 메뉴들을 세로가 아닌 가로로 정렬
        align-items: center; - 메뉴들 가운데 정렬 (border기준)
      }

      .nav-right-items{ - 메뉴들을 오른쪽 정렬하는 기준
        display: flex;
        margin-left: auto; - 왼쪽 간격을 설정함
      }

      .nav-item{ - 메뉴들 서로 여백을 줌
        margin-left: 10px;
      }


   .btn{
            width:100px;
            height:36px;
            background-color:green; - 버튼의 색깔을 지정
            color:white;  - 버튼의 글씨 색깔을 지정
            text-align: center; - 버튼의 글씨를 가운데 정렬
            line-height: 36px; - 글씨의 크기를 지정
            cursor: pointer; - 버튼 커서의 모양을 결정
            border-radius: 3px; - 버튼을 둥글게 만들어줌
        }    


```

      결론 -
      
     첫날은 이런식으로 html과 css의 기본을 알고 무작정 홈페이지를 만들기 시작했다.
     하지만 역시나 무작정 만들기란 쉽지않았고 가장 문제였던것은 바로 element간의 배치였다. 
     홈페이지에서 가장중요한 배치가 무작정할려니 정말 어려웠고 마우스로 옮기면 그곳으로 element가 그냥 옮겨지면 좋겠다고 여러번 생각했다.
     도저히 배치가 어려워서 여러 영상을 보았고 나의 가장 큰 문제 점을 깨달았다. html과 CSS를 공부하면서 정말 중요한 깨달음이라고 생각한다.
     
     첫째 - 무작정 element만을 생각하고 만드는것이아닌 어떻게 element를 배치할지 생각을 한뒤, 그 element가 배치될 큰 layout을 결정해야한다.
     예를 들면 맨위에 로고 , 네비게이션 바+ 메뉴 , 로그인 창이 필요하다하면 이 세개를 무작정 만들어서 배치했었는데 그게 아닌 위에 header라는 큰 틀을 만들어서
     그 틀안에 element를 만들어 배치를 해야하는 것이 가장 중요한 핵심이다. 따라서 처음에 홈페이지의 큰틀을 먼저 정하고 ex) header , body , foot 
     그 큰틀안에 또 다른 틀을 만들고 그 틀에 어떻게 element를 설정하냐인 것이다. 이전처럼 무작정 margin을 남발하며 배치하는것이아닌 틀안에서 움직이니 정말 쉽게 배치가 가능했다.
     
     둘째 - HTML은 그저 글씨 , 도형 덩어리일뿐이다. 모든 스타일링과 배치 색상 등등 꾸미는것은 CSS에서 담당한다. 또한 홈페이지가 active하는것은 JS의 담당이다.
     
     
     많은 깨달음이 있었던 첫째날이였다. 
     
     
     # 한줄요약 - 처음 홈페이지를 제작할때에는 모든 틀을 생각하고 잡고 진행해야 한다.
     
  
