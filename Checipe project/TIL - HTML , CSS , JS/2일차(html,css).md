# 2일차 - 홈페이지를 제작하다

2일차에 들어서서 1일차에 깨달은 개념을 토대로 다시 처음부터 홈페이지를 만들기 시작했다. 
그랬더니 확실히 레이아웃을 잡고 하나하나 생각해놓은대로 만들고 배치를 하니 정말 너무나도 쉽게도 1일차와 다르게
생각대로 진행이 되었다. 따라서 확실히 2일차에는 많은 성과가 있었고 여러가지 원화는 효과들도 넣을 수 있었다.

첫날에 생각한대로 header , midle , last 이렇게 세개로 나누어서 진행했고 , 헤더부분은 간단하게 해결하였다.
하지만 여러가지 디테일 부분에서 배운것이 있는데 일단 배치를할때 주로 margin을 이용했었다. 하지만 margin에는 큰 오류가 존재했는데
내가 설정해놓은 다른 element도 같이 margin에 의해 움직이는 경우가 생겼다는 것이다. 따라서 각각 개인의 element만을 움직이기 위해
다른 명령어를 사용하여야 했는데 종류가 많았지만 나는 주로 position : relative를 사용하였다.

```.header{
    position: relative;
        top: 50px;
    display: flex;
    justify-content: flex-end;
    height: 40px;
    background-color: white;
}

```


위 코드가 내가 설정한 헤더 부분인데 margin으로 했을때 bg 색도 같이 움직이는 문제가 있어서 position을 사용하여 헤더부분만 위에서 조금 내려오도록 하였다.
이렇게 position을 사용하여 더욱 쉽게 배치를 해나갈 수 있었다. 정말 좋은 얻음이였다.

이제 대망의 슬라이드 부분을 진행하였는데, 슬라이드가 여러가지 코드가 존재하지만 나는 자바스크립트를 이용하는 슬라이드를 사용하였다.

슬라이드는 이미 만들어진것을 사용해서 편하였지만 모든 코드가 그렇듯 자신의 입맛대로 바꾸는 것이 참 어렵다. 
슬라이드 또한 그랬는데 슬라이드가 잘 동작하긴 했으나 내가 원하는 위치에 그리고 원하는 크기로 설정하는 것 그리고 
글자 , 점 , 사진 이 세개가 같이 설정되어서 골머리를 많이 앓았다. 하지만 원래 코드에서 세개가 같이 묶여있어서 그런것을 확인했고
이를 수정함으로써 해결할 수 있었다. 아직까지 하나 모르겠는 점은 슬라이드의 크기가 height는 조정이 가능하지만 width는 조정이 안되고, height를 조정하면 맘대로 width도 같이 커진다는 것이다.
이 문제점은 지인을 통해 물어봐서 해결할 것 같다.


```
<!--            헤더부분 아래에 중간 부분을 위한 선언-->
            <div class="midle">
<!--                중간 부분에 있는 큰 슬라이드-->
                <div class="slideshow-container">
                    <div class="mySlides fade">
                        <img src="image2.jfif" style="width:100%">
                        <div class="text">우리가</div>
                        <div class="text">채식과 레시피를</div>
                        <div class="text">선택한 이유</div>
                    </div>

                    <div class="mySlides fade">
                        <img src="image2.jfif" style="width:100%">
                        <div class="text">우리가</div>
                        <div class="text">채식과 레시피를</div>
                        <div class="text">선택한 이유</div>
                    </div>
                    
                    <div class="mySlides fade">

                        <img src="image2.jfif" style="width:100%">
                        <div class="text">우리가</div>
                        <div class="text">채식과 레시피를</div>
                        <div class="text">선택한 이유</div>
                    </div>
                    
                <span class="dot"></span> 
                <span class="dot"></span> 
                <span class="dot"></span> 
                    
            </div>
                
<!--                중간 슬라이드 끝-->
```

그리고 홈페이지를 이쁘게 꾸미기 위해서 필수인 글꼴에 대해서도 이날 많이 배웠는데 글꼴의 그림자 , 종류 , 굵기 등등 많은 효과들을 공부해서 적용할 수 있었다.
따라서 홈페이지가 더욱 원하는대로 보기 이뻐지고 글씨도 가독성이 올라갈 수 있었다.

```
<!--      구글의 폰트를 위한 import-->
      <style>
            @import url('https://fonts.googleapis.com/css2?family=Gaegu:wght@300&family=Song+Myung&display=swap');
      </style>
 ```
 
head부분에 폰트를 위해 선언을 해주고 아래에 font-family를 이용하여 폰트를 적용하였다.

```
.about_vegan > li{
     text-shadow: 3px 3px 2px gray; -- 폰트의 그림자를 적용해준 모습이다. 
    font-family: 'Song Myung', serif;   
    font-weight: bold; -- 폰트의 굵기
    font-size: 40px;
    letter-spacing: 10px;  -- 글자 사이의 넓이를 설정해주었다.
    margin-bottom: 30px;
}
```

그리고 이날 마지막으로 가장 고생을 많이한 일반적인 슬라이드 방식이 아닌 좀 응용버전의 슬라이드를 구현하였다.
이 슬라이드는 slick이라는 오픈소스를 가져왔으며 이를 사용하기위해서 github에서 다운을 받고 라이브러리를 사용하였는데, 이 과정이 생각보다 복잡하고 원하는대로 되지 않았다.
하지만 워낙 slick이 원하는 슬라이드를 가지고 있었고 이를 사용하고 싶었기에 우여곡절 끝에 사용을 할 수 있었다.

섹션을 나누어서 설정을 하였고 계속해서 슬라이드가 흐르지만 총 4개의 사진들이 같이 보이며 넘어가면 다른 사진이 또 오른쪽에서 나오는 효과이다.

```
              <section class="visual">
                    <div id="link-image">
                       <img src="image2.jfif" alt="호박고구마" style="width:200px" border="3">
<!--                        마우스를 올리면 보이는 효과를 위해 글씨에도 클래스를 줌-->
                        <div class="title">
                            <a href="" class="more">호박고구마</a>
                            <a href="" class="more">+ 레시피 보기</a>
                        </div>
                    </div>
              
                </section>

```

위의 모든 설정만 해주고 이렇게 간단하게 라이브러리를 불러온것 만으로도 원하는 슬라이드를 구현할 수 있었다.
CSS도 정말 간단했기 때문에 생략하도록 하겠다.

```
$('.visual').slick({
  slidesToShow: 4,
  slidesToScroll: 1,
  autoplay: true,
  autoplaySpeed: 2000,
});
```

이렇게 둘째날에는 원하던 기능을 모두 구현하고 (디테일적인것 제외) 잠을 잘 수 있어서 너무나도 행복했다.
이 모든것이 첫째날에 고생을 하며 깨달은것이 존재하기 떄문이라고 생각한다. 항상 새로운 언어를 공부할때 이런식으로 하는데, 무엇을 할때 시간이 얼마나 걸리든 얼마나 고생을 하든
그것은 결국 뒤에 큰 거름이 되어 빠른 시간단축과 많은 깨달음을 준다고 다시한번 느꼈다. 많은 얻음이 있었던 첫째날과 둘째날이였다.


# 결론 - 둘째날은 여러가지 디테일과 원하던 슬라이드 효과를 사용할 수 있었고, 라이브러리 사용에대해 배울 수 있었다.




