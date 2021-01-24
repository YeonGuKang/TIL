# 7일차 - 본격적으로 react에서 firebase의 데이터 연결작업을 하다.



일단 우리가 원하는 작업은 DB에 존재하는 정보를 사용자가 원하는 정보만 보여주는 작업이 필요하다.
따라서 이 작업을 오늘 하였고, 이전에 배워온 지식을 토대로 정말 깔끔히 해냈다. 기분이 참 좋은 하루였다.

일단 DB에 넣을 데이터가 아직 정리되지 않았기에 내가 직접 넣어서 작업해보았다.

아래처럼 각 필요한 정보들을 하나하나 담을 객체를 hook을 이용하여 선언해주었다.

```
  // 파이어베이스에서 데이터를 가져오는 과정
  // 각각 채식 type에 맞게 데이터를 불러오기 위함
    const [Lacto, setLacto] = useState([]);
    const [LactoOvo, setLactoOvo] = useState([]);
    const [Ovo, setOvo] = useState([]);
    const [Pesco, setPesco] = useState([]);
    const [Pollo, setPollo] = useState([]);
    const [PolloPesco, setPolloPesco] = useState([]);
    const [Flexi, setFlexi] = useState([]);
    const [Vegan, setVegan] = useState([]);



    그리고 사용자에게 어떤 객체를 보여줄지 담는 객체를 선언하였다.
    
      // 사용자가 선택한 type에 맞게 보여주기위함
    const [chosen, setchosen] = useState([]);
    
    그 뒤에 DB에 존재하는 데이터를 받아오는 작업을 하였는데 이작업이 좀 복잡하고 여러가지 개념이 쓰였기에 
    복습하고 또 복습해도 부족하지 않은 부분이다.
    
    DB를 받아오는 작업을하는 함수를 선언해주었다. 이 함수는 뒤에 나오지만 UseEffect안에서 호출이 되는데,
    이전에 공부했듯이 useEffect는 didMount이기에 처음 데이터를 받아올때 사용해주면 좋은 함수이다.
   
   const getChecipes = async () =>
    {
    
    위에서 선언한 객체들에 DB collection에 존재하는 정보를 알맞게 넣어주었다.
      // 파이어베이스에 있는 컬렉션으름으로 각각의 db정보를 받아옴
      const dbLacto = await dbService.collection("락토").get();
      const dbLactoOvo = await dbService.collection("락토오보").get();
      const dbOvo = await dbService.collection("오보").get();
      const dbPesco = await dbService.collection("페스코").get();
      const dbPollo = await dbService.collection("폴로").get();
      const dbPolloPesco = await dbService.collection("폴로페스코").get();
      const dbFlexi = await dbService.collection("플렉시테리언").get();
      const dbVegan = await dbService.collection("비건").get();
    
    forEach문을 사용하여 해당 객체에 존재하는 document에 대해 모두 실행해주었다.
    또한 그 객체들에 대해 데이터를 모두 set해주어서 데이터를 받아오는 과정이다.
      // dbLacto에 존재하는 모든 각각의 document에 대해서 실행
      dbLacto.forEach((document) => {
      // 임시로 객체를 하나 선언해서 그 객체에 모든 존재하는 데이터와 id를 추가해서 넣어줌
        const LactoObject = {
          ...document.data(),
          id: document.id,
        };
        // Lacto 객체에 파이어베이스에 있는 정보를 set해줌 (set 함수인자에 함수를 넣어준 형태)
        // prev => []  형태는 모든 이전의 document에 대해서 배열을 리턴한다
        // 가장 최근 document인 Object를 return해서 set해주고 그 뒤로 이전 documnet를 return해서 set해줌 (implict return 형식)
        setLacto((prev) => [LactoObject, ...prev]);
      });

      dbLactoOvo.forEach((document) => {
        const LactoOvoObject = {
          ...document.data(),
          id: document.id,
        };
        setLactoOvo((prev) => [LactoOvoObject, ...prev]);
      });
      ...... 이런식으로 모든 객체에 대해서 반복
      
      
      위에서 설명했듯이 useEffect를 통하여 didMount된 순간에 데이터를 불러옴 
      
        // 처음에 mount 됐을때 실행해줌으로써 데이터를 불러옴
    useEffect(()=>{
      getChecipes();
 
    },[]);
    
    
    
    그렇게 사용자가 선택한 event에 맞게 name을 지정해주고 그 name에 맞게 
    Chosen객체에 데이터를 set해주는 과정이다.
    
    // 사용자가 선택한 type에 맞게 데이터를 선택하는 함수
      const getChosen = async (event) => {
       // event안에 존재하는 target의 value를 name으로 넘긴다.
      const {
        target: {name},
      } = event;

      // 아래 name으로 판단해서 chosen 객체에 앎맞는 데이터를 주입
      if(name == "Lacto"){
        setchosen(Lacto);
      } 
      else if(name == "Ovo"){
        setchosen(Ovo);
      }
      else if(name == "LactoOvo"){
        setchosen(LactoOvo);
      }
      else if(name == "Pollo"){
        setchosen(Pollo);
      }
      else if(name == "Pesco"){
        setchosen(Pesco);
      }
      else if(name == "PolloPesco"){
        setchosen(PolloPesco);
      }
      else if(name == "Flexi"){
        setchosen(Flexi);
      }
      else if(name == "Vegan"){
        setchosen(Vegan);
      }

      console.log(chosen);
    }
    
    
    
    그리고 마지막으로 사용자가 button을 눌렀을 때 그 target value를 넘겨주도록 name을 설정해줌
    
     {/* 버튼을 클릭했을때 name의 값을 getChosen으로 넘겨줌 */}
            <div>
               <button onClick={getChosen} name="Lacto">Lacto</button>
               <button onClick={getChosen} name="Ovo">Ovo</button>
               <button onClick={getChosen} name="LactoOvo">LactoOvo</button>
               <button onClick={getChosen} name="Pesco">Pesco</button>
               <button onClick={getChosen} name="Pollo">Pollo</button>
               <button onClick={getChosen} name="PolloPesco">PolloPesco</button>
               <button onClick={getChosen} name="Flexi">Flexi</button>
               <button onClick={getChosen} name="Vegan">Vegan</button>
            </div>

            {/* 사용자가 클릭한 type에 맞는 객체 정보를 쭉 나열해서 보여줌 */}
            <div>
             {/* chosen객체에 존재하는 모든 document에 대해서 Show로 각각 지정해주고 , 그 값들을 나열해준다. key값은 위에서 넣어준 id값 */}
              {chosen.map((Show)=>(
                <div key={Show.id}>
                  <h1>{Show.id}</h1>
                  <img
                    src={ Show.img }
                    alt = "보이지않는 이미지입니다."
                    width='300px'
                    height='300vh'
                 />
                  <h2>{Show.part}</h2>
                  <h3>{Show.way}</h3>
                  <h5>{Show.detail}</h5>
                  <h6>{Show.number}</h6>
                  </div>
              ))}
            </div>
            
            
            ```
            
            
            추가로 ES6로 implicit return을 하는 법과 예시를 아래 블로그에서 참고해서 공부했다. 
            https://velog.io/@nowhhk/%EC%9E%90%EB%B0%94%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8-es6-arrow-function-implicit-return
            
            implicit return
    name이라는 배열에 "😍"를 더한 새로운 배열을 만드는 함수를 작성해본다면,
    기존 방식으로는 이렇게 작성할 수 있다.

const names = ["hk", "js"]

const hearts = names.map(function(item) {
  return item + "😍"
});
ES6의 arrow function으로 작성한다면,

const hearts = names.map(item => item + "😍"
item이라는 argument를 가지고 implicit return하는 함수이다.
implicit return이란 같은 줄에 뭘 적던지 간에 return된다는 뜻이다.

console.log 해보면 새로운 배열이 생성된다.

[ 'hk😍', 'js😍' ]
const hearts = names.map((item,idx) => {
console.log(idx);
return item + "😍"
});
함수가 복잡해진다면 function의 body를 만들기 위해 {}를 추가하게 될 것이고,
{} 를 추가하는 순간 implicit return은 사라진다.
위에서 return을 지운다면 이 함수는 아무것도 리턴하지않는다.

0
1
[ undefined, undefined ]
            
