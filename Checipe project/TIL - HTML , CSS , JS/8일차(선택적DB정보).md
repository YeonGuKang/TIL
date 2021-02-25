# DB 선택적 정보 보여줌

우리 프로젝트의 핵심 기능이라고 할 수 있는 선택적 정보를 거르는 작업을 구현하였다.\
이전에 DB를 홈페이지에 연결해서 데이터를 전부 받아오는 것은 해놨으니 이제 그 정보를 사용자가 선택하는 것에 따라서 보여주는것이 핵심이다.

따라서 아래처럼 각각의 채식주의자의 레시피를 담을 배열을 hook으로 선언해 주었다.

```
  // 각각 채식 type에 맞게 데이터를 불러오기 위함
    const [Lacto, setLacto] = useState([]);
    const [LactoOvo, setLactoOvo] = useState([]);
    const [Ovo, setOvo] = useState([]);
    const [Pesco, setPesco] = useState([]);
    const [Pollo, setPollo] = useState([]);
    const [PolloPesco, setPolloPesco] = useState([]);
    const [Flexi, setFlexi] = useState([]);
    const [Vegan, setVegan] = useState([]);
    
 ```
 
 선언해준 hook들 getChecipes에서 각 타입 collection에서 정보를 불러와 채워주었다.\
 getChecipes는 useEffect에서 실행되도록 하였다.
 
 ```
 const getChecipes = async () =>
    {
      // 파이어베이스에 있는 컬렉션으름으로 각각의 db정보를 받아옴
      const dbLacto = await dbService.collection("락토").get();
      const dbLactoOvo = await dbService.collection("락토오보").get();
      const dbOvo = await dbService.collection("오보").get();
      const dbPesco = await dbService.collection("페스코").get();
      const dbPollo = await dbService.collection("폴로").get();
      const dbPolloPesco = await dbService.collection("폴로페스코").get();
      const dbFlexi = await dbService.collection("플렉시테리언").get();
      const dbVegan = await dbService.collection("비건").get();

      // dbLacto에 존재하는 모든 각각의 document에 대해서 실행
      dbLacto.forEach((document) => {
        const LactoObject = {
          ...document.data(),
          id: document.id,
        };
        // Lacto 객체에 파이어베이스에 있는 정보를 set해줌 (set 함수인자에 함수를 넣어준 형태)
        // prev => []  형태는 모든 이전의 document에 대해서 배열을 리턴한다
        // 가장 최근 document인 Object를 보여주고 그 뒤로 이전 documnet를 보여줌
        setLacto((prev) => [LactoObject, ...prev]);
      });

      dbLactoOvo.forEach((document) => {
        const LactoOvoObject = {
          ...document.data(),
          id: document.id,
        };
        setLactoOvo((prev) => [LactoOvoObject, ...prev]);
      });

      dbOvo.forEach((document) => {
        const OvoObject = {
          ...document.data(),
          id: document.id,
        };
        setOvo((prev) => [OvoObject, ...prev]);
      });

      dbPesco.forEach((document) => {
        const PescoObject = {
          ...document.data(),
          id: document.id,
        };
        setPesco((prev) => [PescoObject, ...prev]);
      });

      dbPollo.forEach((document) => {
        const PolloObject = {
          ...document.data(),
          id: document.id,
        };
        setPollo((prev) => [PolloObject, ...prev]);
      });

      dbPolloPesco.forEach((document) => {
        const PolloPescoObject = {
          ...document.data(),
          id: document.id,
        };
        setPolloPesco((prev) => [PolloPescoObject, ...prev]);
      });

      dbFlexi.forEach((document) => {
        const FlexiObject = {
          ...document.data(),
          id: document.id,
        };
        setFlexi((prev) => [FlexiObject, ...prev]);
      });

      dbVegan.forEach((document) => {
        const VeganObject = {
          ...document.data(),
          id: document.id,
        };
        setVegan((prev) => [VeganObject, ...prev]);
      });
    }


    // 처음에 mount 됐을때 실행해줌으로써 데이터를 불러옴
    useEffect(()=>{
      getChecipes();

    },[]);
    
        
 ```
 그 뒤에 버튼을 만들어서 그 버튼을 클릭했을때 getChosen이라는 함수를 실행하고 value값으로 각 타입의 이름을 전달 해 주었다.
 
  ```
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
   ```
    
   모든 데이터를 hook으로 각 타입에 맞게 저장해놨으니 사용자에게 어떤 정보를 보여줄지 정해야한다.\
   따라서 chosen이라는 hook을 새롭게 선언해주고 그 배열에 사용자가 선택한 타입에 맞는 배열을 넣어주었다.
    
   ```
    // 사용자가 선택한 type에 맞게 보여주기위함
    const [chosen, setchosen] = useState([]);
    
    // 사용자가 선택한 type에 맞게 데이터를 선택하는 함수
      const getChosen = async (event) => {
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

    }
   ```
    
  그렇게 chosen에 사용자가 선택한 정보가 들어갔으므로 그 chosen을 map으로 돌며 모든 정보를 출력하였다.
    
     ```
      {/* 사용자가 클릭한 type에 맞는 객체 정보를 쭉 나열해서 보여줌 */}
            <div>
              {chosen.map((Show)=>(
                <div key={Show.id}>
                  <h1>{Show.id}</h1>
                  <img
                    src={ Show.img }
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
