# 6일차 - AWESOME한 react와 이를 더 AWESOME하게 만들어주는 HOOK에 대해 공부하다

**react에서 function을 component라고 부른다**

리액트 컴포넌트가 Instance로 생성되어 DOM tree에 삽입되어 브라우저 상에 나타나는것을 마운트라고 합니다.
componentDidMount
컴포넌트가 DOM tree에 삽입된 직후에 호출되는 메서드 입니다. 외부에서 데이터를 불러와야 할때 사용하기 적절합니다.

이때 사용하는것이 useEffenct()


리액트 컴포넌트가 업데이트되는것을 업데이트라고 합니다. 
컴포넌트가 업데이트가 될때는 props,state, 부모컴포넌트가 리렌더링될때 업데이트가 됩니다.
componentDidUpdate
리렌더링을 완료한 후 실행되는 메서드입니다. 최초렌더링에서는 호출되지 않습니다. 컴포넌트가 업데이트 되었을시에 DOM을 조작하기 위해 사용합니다.

컴포넌트가 mount되는 것과 render가 되는것은 다르다!, 맨처음 컴포넌트가 렌더될때는 component가 mount 되지만, 다시 props나 state가 변경 되어 render될때는 mount가 되지 않는다!
react의 state나 props 변화가 있을때는 렌더될때 컴포넌트가 다시 마운트 되는 게 아니므로, shouldComponentUpdate(nextProps, nextState) 나, componentWillRecieveProps(nextProps) 쪽에서 그 변화를 감지해 관련 작업을 해줘야하는것이다.



훅은 사실 react를 접하면서 같이 접한 개념이라 그렇게 생소하지는 않았다. 하지만
react를 공부할때 state를 사용해야하고 state를 사용하기위해서는 class, extends를
사용해야하며 state의 정보를 바꾸기 위해 this와 함수를 섞어서 해야하는걸 배웠다.

하지만 class를 만들 필요도 없이 fuction으로 동작하고 위에 필요한 모든 조건을 모두다
무시해버리는 어마무시한 Hook이라는것을 이번에야 알았다. 오늘은 이 HOOK에 대해서
더 자세히 알아보고 공부해보도록 하겠다.

useState에 대해서 먼저 공부하도록 하겠다.
아래와 같이 선언하면 우리는 email이라는 state를 선언과 동시에 값을 넣어주었고
setEmail이라는 함수로 email의 state를 손쉽게 변경할수있다. useState는 Array형태로
처음 인자는 state이고 그 다음인자는 그 state의 값을 변경해주는 함수이다.

```
const Auth = () => {

	// email의 state를 처음에 ""으로 설정
    const [email, setEmail] =useState("");
    const [password, setPassword] = useState("");

};
```

useEffect는 모든 변화를 감지하고 그 변화에 맞춰 실행하는 함수이다.
따라서 이를 잘 사용하면 언제 , 무엇이 변경됐을때 어떻게 실행할지를 모두 결정할 수 있는
아주 강력한 함수이다.

useEffect(sayHello, [number]);

이런식으로 사용한다면 sayHello라는 함수를 실행하는데 이는 nuber이라는
변수가 변경되었을때 실행하라는 뜻이다. (sayHello 함수는 따로 만들어준 함수)


이번에는 useRef에 대해서 알아보겠다 useRef는 마치 우리가 JS에서
DOM을 사용하는듯이 html의 element를 변경할수있는 강력한 함수이다.
아래예시를 보여주겠다. getElementByid() 라고 생각하면 편하다.

```
const potato = useRef();
// ref를 이용하여 input tag에 접근하여 실행해준 모습
  setTimeout(() => potato.current.focus(), 5000);
  return(
    <div className="dd"> 
// ref를 이용하여 이 input을 밖에서 변경해주고 사용할 수 있다.
    <input ref={potato} placeholder="name" />
    </div>
```
