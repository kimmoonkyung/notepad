# react 설치
    설치할 폴더로 이동하여 'create-react-app .'
    . 은 현재경로

## 샘플 실행
    vscode terminal에서 'npm run start'
    --종료
    vscode terminal에서 'ctrl + c'

## bulid 실행 
> ( ** 공백 등 같은 불필요한 것들을 제거 하여 용량을 줄인다. -> 실제로 (서비스)배포시 
> 빌드안에 있는 파일을 배포한다. 실서버 환경)
>
    vscode terminal에서  'npm run build'

### npm으로 설치하는 간단한 웹 서버
    'npm install -g serve'
      -> 어디에서나 serve 명령어로 서버를 설치할 수 있다.
    'npx serve -s build'
      -> '-s build' 서브라는 웹서버를 받아서 실행시킬때 'build' 라는 생성한 디렉토리를 document 루트로 하겠다. 

### 이것은 js 문법이 아니고, jsx 문법이다.
    class App extends Component {
      render() {
        return (
          <div className="Subject">
            <Subject></Subject>
        </div>
        )
      }
    }

### 리액트 코드 작성시
    import React, { Component } from 'react';
    export default 'JS파일명'
    는 필수로 적어야 된다고 생각하면 된다.

### Component 만드는 법.
1. function으로 생성
```
    -> 
    function App() {
        return (
            코드 작성
        )
    }
```
2. class로 생성
```
    -> 
    class App extends Component {
        render() {
            return (
                코드 작성
            )
        }
    }
```


## props
> 사용자가 컴포넌트를 사용하는 입장에서 중요한것 
> 
    function에서는 {this.props.xxx} 사용 안됨
    class는 사용 가능. function에서는 어떻게 ?
* props are read only
* props can not be modified

## state
> 데이터를 갖다 쓰는 용도.
>
* state changes can be asynchronous
* state can be modified using this.setStae({  })
### setState
    this.setState({
      mode : "welcome"
    })


### key
```
```
### bind
    .bind(this)

### Immutable
    불변.
    immutable.js

### router
> React Router
```ReactRouter

```

### redux
```ReactRedux

```
### react server side rendering
```
```

> 컴포넌트 이름은 대문자로 시작한다.

#### index.js 와 App.js의 의미
```

```


## JSX 기본 규칙
> 태그는 꼭 닫혀 있어야 한다.

> 두개 이상의 태그는 하나로 감싸 있어져야 한다.

#### ex) 
```
<div></div> <hello/> -> 에러, <div> <div></div> <hello/> </div> 로 해결. 또는 상위 div 대신 <> </>를 사용한다.
  > return 시 괄호는 없어도 된다.
  > jsx 내부에서 js 사용법
    const name = '짐승내'; -> <div>{name}</div>
  > style과 class 설정 방법
    1. style은 객체를 만들어 사용 한다. (속성은 카멜케이스로 작성)
      ex)   const style = {
              backgroundColor: 'rgba(0,0,0, 0.5)',
              color: 'aqua',
              fontSize: 24,
              padding: '1rem'
            };
      <div style={style}></div>
    2. class 는 className 으로 사용한다.
      ex) <div className="hihi"></div>
    3. 주석
      중괄호로 감싸서 사용한다.
      { /*  */ }
      html 코드 내에서는 //로 사용 가능하다.
      ex) <Hello> '// 주석' </Hello>
```
### props (proerties 프로퍼티)
> 컴포넌트를 사용하게 될 때 특정 값의 전달이 필요할 때 사용
#### ex)
##### App.js
```
function App() {
  return (
      <Hello name="react" color="aqua"/> --> 이것들이 props 다 name, color
  );
}
```
##### Hello.js
```
/* function Hello(props) { */
function Hello({color, name}) {
  console.log(props); // {name: react}
  /* return <div style={{color: props.color}}>안녕 나는 짐승내! {props.name} </div>; */
  return <div style={{color}}>안녕 나는 짐승내! {name} </div>;
  // 이런 식으로 사용도 가능하다
}
console.log(props);
```
  
#### defaultProps (기본값) 사용법
##### Hello.js
```
    Hello.defaultProps = {
      name : "짐승균"
    }
    
    App.js
    return (
      <>
        <Hello name="react" color="red" /> name="react"
        <Hello color="black" /> // name="짐승균"으로 기본값이 들어간다.
      </>
    )
```
#### propsChildren (프롭스 칠드런)
#### ex) 
##### App.js
```
function App() {
  return (
    <Wrapper> ... </Wrapper>
  );
}  
```
##### Wrapper.js
```
function Wrapper({ children }) {
    const style = {
        border: '2px solid black',
        padding: 16
    };
    return (
        <div style={style}>{children}</div>
    )
}
```
#### 조건부 렌더링
    {isSpecial && <b>*</b>}

### useState (동적 상태 관리 - Hooks)
```
const [number, setNumber] = useState(10); // useState(기본값 설정);
```
##### Counter.js
> ** import React, { useState } from 'react'; // React 패키지에서 useState 함수를 불러온다.
>
    function Counter() {
      const [number, setNumber] = useState(0); // useState를 사용하면 배열을 반환하며, 첫번째 원소는 현재 값, 두번째 원소는 값을 변경하는 함수로 사용할 것이다.
      const increase = () => {
        // setNumber(number + 1);
        setNumber(prevNumber => prevNumber + 1); // 함수형 업데이트 (성능 최적화)
      }
      const decrease = () => {
        setNumber(number - 1);
      }
      retrun (
        <div>
          <h1>{number}</h1>
          <button onClick={increase}>+1</button>
          <button onClick={decrease}>-1</button>
        </div>
      )
    }

##### App.js
    function App () {
      return (
        <Counter />
      )
    }

### useState (input 상태 관리)
##### InputSample.js
    import React, { useState } from 'react';
    function InputSample() {
      const [text, setText] = useState('');
      const onChange = (e) => {
        setText(e.target.value);
      }
      const onReset = () => {
        setText('');
      }
      retrun (
        <div>
          <input onChange={onChange} value={text}/>
          <button onClick={onReset}>초기화</button>
          <b>값 : </b>
          {text}
        </div>
      )
    }
### 여러개의 input 관리
    function InputSample(){
      const [inputs, setInputs] = useState({
        name : '',
        boyFriend : ''
      });
      const { name, boyFriend } = inputs;
      const onChange = (e) => {
        const {name, value} = e.target;
        setInputs({
          ...inputs,
          [name] : value,
        });
      const onReset = () => {
        setInputs({
          name : '',
          boyFriend : ''
        })
      }
    }
> 객체 상태를 업데이트 할 때는 ...(스프레드 문법)을 사용해서 객체를 복사하고 난 뒤 상태를 바꿔줘야한다.


### useRef (특정 DOM 선택하기)
    import React, { useState, useRef } from 'react';
    const nameInput = useRef();
    const onReset = () => {
      setInput({ .. });
      nameInput.current.focus();
    }
    <input ref={nameInput}>
    // 초기화 버튼 클릭시 ref 설정한 input 으로 포커스 이동

### 배열 렌더링 하기
    function Users( { user } ) {
      return (
        <div>
          <b>{user.name}</b> <span>({user.email})</span>
        </div>
      )
    }
    function UserList() {
      const users = [
        {id : 1, name: '승내', email: '1@mail.com'},
        {id : 2, name: '짐승내', email: '2@mail.com'}
      ]
      return (
        <div>
          { 
            users.map( (user,idx) => (<Users user={user} key={idx}/>) ) 
            // "(user, idx)" 파라미터를 가져와서 "=>" Users 라는 컴포넌트를 렌더링 해줄것("(<Users user={user} />)")
            // idx는 "key={idx}" key props로 사용한다.
              > 미사용 시 child in a list should have a unique "key" prop. > 고유값을 key 로 사용해줘야함.
                > ex) "key={user.id}"
            // key가 없다면 비효율적인 렌더링을 한다.
          }
        </div>
      )
    }

### useRef 로 컴포넌트 안의 변수 만들기
> 컴포넌트가 리렌더링 될 때마다 기억할 수 있는 값을 관리할 때도 사용할 수 있다.
#### ex) 
```
setTimeout, setInterval, 외부라이브러리를 사용해서 생성된 인스턴스를 담을때, scroll 위치 등 다양하게 사용한다.
```
> useRef로 관리하는 값은 바뀌어도 컴포넌트가 리렌더링 되지 않는다.
    
  
### 배열에 항목 추가하기
  App.js 에서 4개의 props를 받아온다.
##### App.js
```
function CreateUser( {username, email, onChange, onCreate} ) {
    <CreateUser username={username} email={email} onChange={onChange} onCreate={onCreate}/>
    > {username}, {email} -> "inputs" 로 관리
      const [inputs, setInputs] = useState({
        username: '',
        email: '',
      });
      const { username, email } = inputs;
    > {onChange} -> "e(이벤트)"를 받아와서 setInputs(useState) 사용. -> name과 value를 e.target에 담음 -> 
      const onChange = (e) => {
        const { name, value } = e.target;
        setInputs({
          ...inputs,
          [name] : value,  // name값을 value로 덮어 씌우겠다. ex) name이 username(input)이면 username의 value 값을,
        });
      };
```
> {onCreate} -> 클릭시 "user" 객체 생성 후 setUsers(useState)에 "...users" 로 복사 해온 뒤 생성한 "user" 객체를 더 해주는 로직 -> 이후 setInputs를 통해 inputs들 값을 비워 준다.

> 주의 할 점으로 객체를 복사해 올 땐, 기존의 배열을 건들지 않는다. push splice sort 같은 것은 사용 하지 않는다.
```
const onCreate = () => {
  const user = {
    id: nextId.current,
    username,
    email, // ...inputs 로 대체 가능
  };
  setUsers([...users, user]); //setUsers(users.concat(user)); 로 대체 가능
  setInputs({
    username: '',
    email : '',
  });
  console.log(nextId.current);
  nextId.current += 1;
}
```

### 배열에 항목 삭제하기
##### App.js
    const onRemove = (id) => {
      console.log("삭제버튼 클릭 : " + id);
      setUsers(users.filter(user => user.id !== id));
    }
    > return()
      <UserList users={users} onRemove={onRemove}/>
##### UserList.js
###### User 컴포넌트
```
function User({ user, onRemove }) {
  const {username, email, id} = user;
  > return()
    <button onClick={() => onRemove(id)}>삭제</button>
    {/* <button onClick={onRemove(id)}>삭제</button -> 이래 쓰면 렌더링시점에 삭제된다. */}
```
> onClick 은 함수를 "() =>" 를 넣어서 사용해야함.

### 배열에 항목 수정하기
##### App.js
```
const onToggle = (id) => {
  console.log("수정버튼 클릭 : " + id);
  setUsers( users.map( user => user.id === id ? { ...user, active: !user.active } : user ) );
  // 파라미터로 가져온 id 값이 일치한다면 active 값을 바꿔준다.
  // "users.map"의 파라미터를 "user"로 사용 하고 user.id의 값과 onToggle을 통해 가져온 id의 값이 일치한다면, 
  // "? { ...user, active: !user.active }" "...user"로 객체를 복사해오고 ",active:" 로 active(boolean 값임.) 값은 반대로 바꿔준다. !user.active
  // ": user" 일치하지 않는다면 기존의 값을 그대로 사용하겠다.
};
```
##### UserList.js
###### User 컴포넌트
```
function User({ user, onRemove, onToggle }) {
  const {username, email, id, active} = user;
> return
  <b 
    style={{
      color: active ? 'green' : 'black', // active값이 true 면 "green" false 면 "black"
      cursor: 'pointer'
    }}
    onClick={ () => onToggle(id) }
```
###### UserList 컴포넌트 onRemove 때와 마찬가지로
```
function UserList( {..... onToggle 추가 } )
  > return ()
    <div>
      { users.map( (user) => ( <User user={user} key={user.id} onRemove={onRemove}onToggle={onToggle}/> ) ) }
    </div>
```
### useEffect 사용하여 마운트언마운트 업데이트할 작업 설정.
  > 컴포넌트가 마운트 됐을 때 (처음 나타났을 때), 언마운트 됐을 때 (사라질 때), 그리고 업데이트 될 때 (특정 props가 바뀔 때)


### useMemo
> 컴포넌트 최적화시 사용..
>

### useCallback
> 리렌더링시 컴포넌트 최적화
```
  > 사용법
    export default React.memo(컴포넌트);
```

### useReducer
```
useState -> useReducer 로 변경
  import React, { useReducer } from 'react';
    > reducer 함수 생성
      function reducer(state, action) {
          switch (action.type) {
              case 'INCREMENT' :
                  return state + 1;
              case 'DECREMENT' :
                  return state - 1;
              default:
                  throw new Error('Unhandled action');
          }
      };
```
```
    > useState 방식 변경
      const onIncrease = () => {
        setN(prevNumber => prevNumber + 1);
      }
        > useReducer
          const [number, dispatch] = useReducer(reducer, 0);
          const onIncrease = () => {
              dispatch({
                  type : 'INCREMENT'
              })
          }
```

## useReducer VS useState
    정해진 답은 없다. 상황에 따라 불편할때도, 편할때도 있다.
    예를들어 컴포넌트에서 관리하는 값이 하나, 혹은 단순한 값 (문자열, boolean, 숫자 등)이면 useState로 관리하는 것이 편할 것이다.
    맘에 드는 방식을 사용 하면 될 것이다.
    간단한거다 싶으면.. useState / 복잡할 것 같다.. 그럼 useReducer

### custom Hook
```
```

### contextAPI
```
```

### IMMER (개인적으로 맘에든다.)
    불변성 관리
      불변성을 해치는 코드를 작성해도 대신 불변성 유지를 해준다.
    ex ) const arr = [ 
                        { id: 1, text: 'hello'},{ id:2, text: 'bye'},{ id:3, text: '9ood'}
                    ] 
        const nextArr = produce(arr, draft => {
            draft.push({id:4, text: '안녕'});
            draft[0].text = draft[0].text + ' world';
        });
    성능 -> 유의미한 차이가 날정도로 느리다고 볼 순 없는 듯 하다.
            구형 브라우저나 리액트 네이티브 환경에서는 이 기능(proxy)이 지원되지 않는다. -> 느려짐.

### 클래스형 컴포넌트
> hooks 가 나오기 전까지 함수형 컴포넌트보다 기능이 잘 먹어서 사용함.
> 

### LifeCycle 메서드
    https://react.vlpt.us/basic/25-lifecycle.html
    https://codesandbox.io/s/hungry-river-5hgu5?file=/src/LifeCycleSample.js:1050-1055

### componentDidCatch / Sentry
    componentDidCatch(error, info){
        console.log('에러 발생');
        console.log({
            error,
            info
        });
        this.setState({
            error: true,
        })
        if(process.env.NODE_ENV === 'production'){
            Sentry.captureException(error, {extra: info});
        }
    }


### scss 
    classnames
        > yarn add classnames
          > import classNames from 'classnames'; 
            > 혹은 import classNames from 'classnames/bind'; -> css module 을 좀 더 쉽게 사용 하게 해주는
    .button{
      &:hover{
        > & 는 자기 자신을 가리킨다. 즉 여기서는 button
      }
    }

### ...rest props
```
```

### CSS Module
    레거시 프로젝트에 리액트롤 도입 할 때,
    CSS 클래스 네이밍 규칙 만들기 귀찮을 때
    사용 하면 좋음.

### Styled-components
    yarn add styled-components
    import styled from 'styled-components';
      마켓 플레이스 vscode-styled-components 확장프로그램 설치
> styled-components를 사용 하면 

> 스타일을 선언과 동시에 컴포넌트를 생성해 낼 수 있다.

> *Tagged Template Literal을 사용하여 생성한다.
 
    ex) const Example = styled.div`
          weight: 100px;
          height: 100px;
          background: pink;
        `
> props를 받아서 설정도 가능하다.

      ex) const Example = styled.div`
            weight: 100px;
            height: 100px;
            background: ${props => props.color || 'black'};
          `
          function App() {
              return <Example color="blue">
          }

### Polished 스타일 유틸 함수 사용
    yarn add polished
    import { darken, lighten } from 'polished';

### ThemeProvider
    import styled { ThemeProvider } from 'styled-components';
      <ThemeProvider theme={{}}></ThemeProvider>

### styled-components 내 변수 사용
    App.js
      const palette = {
        blue: '#228be6',
        gray: '#496057',
        pink: '#f06595'
      }
      function App() {
        return( 
                <ThemeProvider theme={{ palette }}> 
                  ...
                </ThemeProvider>
              )
      }
    기존 코드(컴포넌트.js)
      background: ${(props) => props.theme.palette.blue};
        &:hover {
            background: ${(props) => lighten(0.1, props.theme.palette.blue)};
        }
        &:active {
            background: ${(props) => darken(0.1, props.theme.palette.blue)};
        }
    > ThemeProvider 사용 후 변경 코드(컴포넌트.js)
      import styled, { css } from 'styled-components';
      ...
        ${props => {
          const color = props.theme.palette.blue;
          return css`
            background: ${color};
            $:hover {
              background: ${lighten(0.1, color)};
            }
            $:active {
              background: ${darken(0.1, color)};
            }
          `
        }}
    > default Props 설정
      컴포넌트.defaultProps = {
        color: 'blue',
      }
      > styled components 수정
        기존 ${props => {
                const color = props.theme.palette.blue; .....
        수정 ${props => {
                const color = props.theme.palette[props.color]; .....
      function 컴포넌트({ children, color, ...rest }){
        return (
          <Styled컴포넌트 color={color} {...rest }>
            {children}
          </Styled컴포넌트>
        )
      }

    > 트랜지션 구현 transition
    import styled, { keyframes } from 'styled-components';
    Dialog.js


# TODO LIST 투두리스트 프로젝트
    npx create-react-app 프젝명
    yarn add styled-components react-icons

> 글로벌 스타일 지정
>
    import { createGlobalStyle } from 'styled-components';
    const GlobalStyle = createGlobalStyle`
      body {
        background: #e9ecef;
      }
    `;

### Context Api를 활용한 상태관리
> TodoContext.js

### API 연동
```
```

### react-async
    yarn add react-async

### Context 활용한 비동기 작업 상태 관리
> UsersContext.js

### react-router
    yarn add react-router-dom

### SPA Single Page Application
    라우팅을 클라이언트가 담당한다.
    라우팅이란 ? 어떤 주소에 어떤 UI 를 보여줄지.
    보통은 서버에서 처리하는 로직이지만 spa 에서는 클라이언트가 관리한다.

    import { HashRouter } from 'react-router-dom';
      index.js
        > <HashRouter> 
            ....
          </HashRouter>
            > url에 #(해시태그가 붙는다.)
              > ex ) http://localhost:3000/#/
#### MemoryRouter
> url에 변화가 없다. (가상의 주소)

#### exact
    <Route path="/" component={Home} exact />
      > exact default 값 true
        > exact 가 있으면 url이 path와 일치해야만 화면에 보여준다.

#### Link
1. a 태그는 사용하지 않는다. 
2. a 태그를 사용하면 페이지를 새로 불러온다.
```
import { Route, Link } from 'react-router-dom';
```

#### 파라미터와 쿼리
> 파라미터
> 
    props "match" { match } 
      > Route 컴포넌트에서 넣어주는 프롭스, 따로 설정할 필요 없이 자동으로 받아온다.
        > const { username } = match.params;
        > <Route path="/profiles/:username" component={Profile} />
          > path대로 조회 > /profiles/kmk

> 쿼리
> 
    props "location"
    { location } 
      > http://localhost:3000/about?a=1
        > {
              "pathname": "/about",
              "search": "?a=1",
              "hash": ""
          }
        location은 이러한 오브젝트를 뱉어낸다.
> qs라는 라이브러리를 사용하여 파싱한다

```
      yarn add qs
        import qs from 'qs';
        const query = qs.parse(location.search, {
            ignoreQueryPrefix: true, // <- ?를 걸러준다.
        });
          > http://localhost:3000/about?b=2&c=4
            > {
                  "b": "2",
                  "c": "4"
              }
            qs를 사용하면 이러한 오브젝트를 뱉어낸다.
      const detail = query.detail === 'true'; 
        // -> query 안의 detail이라는 값이 true일때만 해당 값을 true로 하겠다. 
        (문자열로 가져오기 때문에 'true'로 비교해야한다.)
      const b = query.b; // -> http://localhost:3000/about?b=paka99
      console.log(b); // -> paka99
```
> SubRoute (서브 라우트)
##### Profiles.js
```
    <h3>사용자 목록</h3>
    <ul>
        <li>
            <Link to="/profiles/nsn">노승내</Link>
        </li>
        <li>
            <Link to="/profiles/ask">짐승균</Link>
        </li>
    </ul>
    <Route
        path="/profiles"
        exact
        render={() => <div> {a} 사용자를 선택해주세요</div>}
    />
    <Route path="/profiles/:username" component={Profile} />
```
#### 라우터 부가기능
> history 객체

> {history} props 로 받아온다.
```
      const goBack = () => {
        history.goBack();
          // goBack => 뒤로가기
      };
      const goHome = () => {
          history.push('/');
          // push => 특정경로 이동
      };
```
```
      const replactToHome = () => {
          history.replace('/');
          // goHome은 방문한 페이지를 기록에 남기지만
          // replace는 남기지 않는다.
      };
```
```
      useEffect(() => {
          console.log(history);
          const unblock = history.block('나갈거임 ?');
          return () => {
              unblock();
              // 컴포넌트가 언마운트 될 때
              // 이탈 방지 하는 기능을 비활성
              // alert 창 뜸.
          };
      }, [history]);
```
#### withRouter
> 라우터 컴포넌트가 아닌 곳에서 match, location, history props 들을 사용할 수 있게 해줌.
```    
import { withRouter } from 'react-router-dom';
function WithRouterSample({ location, match, history }) {
  return (
          <div>
              <h4>location</h4>
              <textarea value={JSON.stringify(location, null, 2)} readOnly />
              <h4>match</h4>
              <textarea value={JSON.stringify(match, null, 2)} readOnly />
              <button onClick={() => history.push('/')}>홈으로 이동</button>
          </div>
      );
  }
  export default withRouter(WithRouterSample);
  > withRouter match
      현재 자신이 렌더링 된 위치를 기준으로 match 값을 받아옴.
        > 위의 예제를 기준으로는 withRouter는 Profiles.js 에서 렌더링 되고 있고
        > url parameter를 따로 받아오고 있지 않기 때문에 (App.js 에서)
          {
            "path": "/profiles",
            "url": "/profiles",
            "isExact": false,
            "params": {}
          } => match 오브젝트는 params를 빈객체로 뱉는다.
        > Profiles.js 가 아닌 Profile.js 에서 렌더링한다면
          {
            "path": "/profiles/:username",
            "url": "/profiles/ask",
            "isExact": true,
            "params": { "username": "ask" }
          } => 정상적으로 받아옴.
```
```
  withRouter
    location은 어디에서 렌더링 되던 똑같은 정보를 가져오지만,
    match는 렌더링 된 기준으로 가져온다.
    조건부로 성공할 때 사용한다.
      > ex) 로그인 성공 했을 때 특정경로, 실패 시 가만히있고 싶다. 같은
```
#### Switch
> 여러 라우트 중 가장 먼저 매칭 된 하나만 보여줌
```
      > App.js
        import { Route, Link, Switch } from 'react-router-dom';
        <Switch>
            <Route path="/" component={Home} exact={true} />
            <Route path="/about" component={About} />
            <Route path="/profiles" component={Profiles} />
            <Route path="/history" component={HistorySample} />
            <Route
                    render={({ location }) => (
                        <div>
                            <h2>이 페이지는 존재하지 않습니다.</h2>
                            <p>{location.pathname}</p>
                        </div>
                    )}
                /> => 404 페이지 구현시 사용하면 좋을 듯 하다.
        </Switch>
```     
#### NavLink
> 현재 주소와 일치한다면 스타일 바꾸기.
 
##### Profiles.js
```
  import { NavLink, Route } from 'react-router-dom';
    <NavLink
        to="/profiles/nsn"
        activeStyle={{ background: 'black', color: 'white' }}
    >
        노승내
    </NavLink>
``` 
#### <Prompt>, <Redirect>
```      
```
#### useReactRouterHook 사용
    yarn add use-react-router

### Redux 리덕스
> 리액트 생태계에서 가장 사용률이 높은 상태 관리 라이브러리. 리덕스를 사용하면 컴포넌트의 상태 관리 로직들을 다른 파일로 분리시켜서 더욱 효율적으로 관리할 수 있으며 글로벌 상태 관리도 손 쉽게 할 수 있다.
  
> useReducer 와 유사하다.
```
1. Context 사용과의 차이점
    1. 미들웨어
        1. 특정 조건에 따라 액션이 무시되게 만들 수 있다.
        2. 액션을 콘솔에 출력하거나, 서버쪽에 로깅할 수 있다.
        3. 액션이 디스패치 됐을 때 이를 수정해서 리듀서에게 전달되도록 할 수 있다.
        4. 특정 액션이 발생했을 때 이에 기반하여 다른 액션이 발생되도록 할 수 있다.
        5. 특정 액션이 발생했을 때 특정 자바스크립트 함수를 실행시킬 수 있다.
        6. 비동기 작업을 더욱 체계적으로 관리 가능하다. (주사용 용도)
    2. 유용한 함수와, Hooks를 지원 받을 수 있다.
      ex) connect, useSelector, useDispatch, useStore 등...
    3. 기본적인 최적화가 이미 되어 있다.
    4. 하나의 커다란 객체에 넣어서 사용한다.
        1. 매번 컨텍스트를 만드는 수고로움을 덜어준다.
    5. 리덕스는 아주 유용한 개발자도구가 있다.
        1. 현재 상태를 한눈에 볼 수 있다.
        2. 지금까지 어떠한 변화가 있었는지 볼 수 있다.
        3. 특정 시점으로 상태를 되돌릴 수도 있다.
    6. 이미 사용중인 프로젝트가 많다.

2. 언제 써야하는가 ?
    1. 프로젝트의 규모가 큰가 ?
      Redux Y / Context API N
    2. 비동기 작업을 자주 하는가 ?
      Redux Y / Context API N
    3. 리덕스가 편하게 느껴지는가 ?
      Redux Y / Context API or MobX N
```
> *리덕스에서 사용되는 키워드 숙지
```
  1. 액션 (Action)
    상태에 어떠한 변화가 필요할 때 액션이라는 것을 발생 시킨다.
    액션 객체는 { type: 'ADD', data : { id:1, text:'추가추가' } } 이런 식으로 이루어져 있다.
  2. 액션 생성함수 (Action Creator)
    export function addTodo(data) {
      return { type: 'ADD_TODO', data };
    }
      > 화살표 함수로도 만들 수 있다.
        export const changeInput = text => ({
          type: "CHANGE_INPUT",
          text
        });
  3. 리듀서 (Reducer)
    변화(상태를 바꿔주는)를 일으키는 함수. 두 가지 파라미터를 가져온다 (action, state)
      1. switch (action.type) 에 따라 state 값을 변경해준다.
      2. 불변성을 유지해줘야 함. (스프레드 연산자 사용 등)
      3. default 로 반환 하는 것은 보통 에러를 발생시키는게 일반적이지만
        리덕스의 리듀서는 기존의 state를 반환 시킨다.
        리덕스를 사용 할 땐 여러개의 리듀서를 만들고 root reducer라는 것을 만들 수 있다.
        ?
  4. 스토어 (Stroe)
    한 애플리케이션 당 하나의 스토어를 만들게 된다.
    스토어에는 현재의 앱의 상태와, 리듀서가 들어있고 내장 함수 등이 들어 있다.
    ( ex: dispatch[액션을 발생시키는 것] )
    구독(subscribe)
      > 스토어의 내장 함수 중 하나, 호출 할 때 파라미터로 특정 함수를 넣어주면
      > 액션이 디스패치 될 때 마다 우리가 설정한 함수가 호출 된다.
      > 스토어의 상태가 업데이트 될 때 마다 특정 함수를 호출 할 수 있다는 것.
```
> *리덕스의 3가지 규칙
```
  1. 하나의 애플리케이션엔 하나의 스토어가 있다.
    스토어를 한개 이상 만들면 안 된다. (가능은 하나 권장되지 않는다.)
    스토어가 여러개가 되면 개발자 도구를 제대로 활용하지 못한다.
  2. 상태는 읽기전용이다. (불변성을 지켜야 한다.)
    스프레드 연산자, concat, filter, map, slice 등 내장 함수 사용
    좋은 성능을 지켜내기 위함.
    불변성을 지켜야 컴포넌트들이 제대로 리렌더링 된다.
  3. 변화를 일으키는 함수 리듀서는 순수한 함수여야한다.
    리듀서 함수는 이전 상태와, 액션 객체를 파라미터로 받는다.
    이전의 상태는 절대로 변경하지 않고, 변화를 일으킨 새로운 상태 객체를 만들어 반환.
    똑같은 파라미터로 호출된 리듀서 함수는 언제나 똑같은 결과값을 반환해야 한다.
    > 동일한 인풋 -> 동일한 아웃풋
      > new Date(), Math.random(), axios.get() 사용 하면 안 됨.
```
#### 실습
> yarn add redux

#### Ducks 패턴
> ducks 패턴을 사용할 땐,
```
1. 액션타입 선언시 문자열 앞에 접두사를 붙인다.
2. 다른 모듈과 중복되지 않게 하기 위함.
3. 액션 생성 함수 작성시는 export 키워드를 붙인다.
4. 내보 낸 뒤 불러와서 사용 할 것임.
```

> 루트 리듀서를 만들 때는 combineReducers를 불러와서 사용한다.
##### modules/index.js
        import { combineReducers } from 'redux';
        import counter from './counter';
        import todos from './todos';

        const rootReducer = combineReducers({
            counter,
            todos,
        });

        export default rootReducer;

        리액트에 리덕스를 적용하자.
          > 패키지 설치
            yarn add react-redux
          > src/index.js
            import { Provider } from 'react-redux';
            import { createStore } from 'redux'; 
            import rootReducer from './modules';

            const store = createStore(rootReducer);
            console.log(store);
            console.log(store.getState());

            ReactDOM.render(
                <Provider store={store}>
                    <App />
                </Provider>,
                document.getElementById('root'),
            );

##### /components/Counter.js
      프레젠테이션 컴포넌트에서는 UI에 집중한다.
      상수나 필요 한 값은 props로 받아와서 사용한다.

##### /containers/CounterContainer.js
      컨테이너 컴포넌트는 리덕스에 있는 상태를 조회하거나
      액션을 디스패치할 수 있는 컴포넌트를 의미한다.
        리액트 컴포넌트에서 리덕스를 연동할 땐, useSelector, useDispatch 훅을 사용 한다.
        useSelector => 상태 조회 훅 
        useDispatch => 액션 디스패치 
      
> 상태를 조회 할때는 useSelector를 사용 한다.
> 
          import { useDispatch, useSelector } from 'react-redux';
          import { decrease, increase, setDiff } from '../modules/counter';

          function CounterContainer() {
              // 상태를 조회 할때는 useSelector를 사용 한다.
              const { number, diff } = useSelector((state) => ({
                  // state => store.getState() 반환 객체
                  number: state.counter.number,
                  // number 값은 state > counter > number 값.
                  diff: state.counter.diff,
              }));

              const dispatch = useDispatch();

              const onIncrease = () => dispatch(increase());
              const onDecrease = () => dispatch(decrease());
              const onSetDiff = (diff) => dispatch(setDiff(diff));

              return (
                  <Counter
                      number={number}
                      diff={diff}
                      onIncrease={onIncrease}
                      onDecrease={onDecrease}
                      onSetDiff={onSetDiff}
                  />
              );
          }
redux devtools
```    
    구글 크롬 웹스토어 다운로드 후
    yarn add redux-devtools-extension
    index.js
      import { composeWithDevTools } from 'redux-devtools-extension';
      const store = createStore(rootReducer, composeWithDevTools());
```
    
  
### **리덕스 미들웨어
    리덕스가 지닌 핵심기능, mobx/contextAPI 와 비교 했을 때 차별화 될 강력한 기능
    만약, 리덕스를 사용하는데 미들웨어를 사용하지 않는다면 그냥 contextApi나 useReducer를 사용 하는게 나을 수 있다.

> 미들웨어를 사용하면
> 
      액션 -> 미들웨어 -> 리듀서 -> 스토어
      1. 액션이 디스패치 될 때 미들웨어에서 액션의 특정 조건에 따라 무시처리 되도록 할 수도 있다.
      2. 액션이 리듀서에게 전달되기 전에 특정코드를 실행 할 수 있다.
        > 액션을 처리하는 과정을 콘솔에 출력
        > 리듀서에 전달되기 직전에 액션을 수정할 수도 있다.
        > 어떤 액션이 디스패치 되었을 때 또다른 액션을 만들어서 새로 디스패치 할 수도 있다.
      3. 리덕스에 관련 된 작업이 아니여도 뭐든 할 수 있다.
        > 액션이 디스패치 되는 과정 중, 특정 조건에 따라 라우터에서 다른 곳으로 이동.
        > 액션에 기반 해서 비동기 작업
      4. 주로 비동기 작업을 처리할 때 사용
        > API 요청
      5. 일반적으로 만들어진 라이브러리 사용
        > redux-thunk, redux-saga, redux-observalble, redux-promise-middleware

> 프로젝트 준비
   
    yarn add redux react-redux
      src/ module 디렉토리 생성
##### counter.js
          // 타입
          const INCREASE = 'counter/INCREASE';
          const DECREASE = 'counter/DECREASE';

          // 액션 생성 함수
          export const increase = () => ({ type: INCREASE });
          export const decrease = () => ({ type: DECREASE });

          // 초기 상태
          const initialState = 0;

          // 리듀서
          export default function counter(state = initialState, action) {
              switch (action.type) {
                  case INCREASE:
                      return state + 1;
                  case DECREASE:
                      return state - 1;
                  default:
                      return state;
              }
          }

> 루트 리듀서 생성. 
##### modules/index.js
          import { combineReducers } from 'redux';
          import counter from './counter';
          const rootReducer = combineReducers({ counter });
          export default rootReducer;

> ** 프로젝트에 리덕스 적용
            
      1. 프로바이더(react-redux)를 불러오고 스토어(redux)도 불러온다.
        index.js
        import { Provider } from 'react-redux';
        import { createStore } from 'redux';
        import rootReducer from './modules';
        const store = createStore(rootReducer);
      2. App 컴포넌트를 프로바이더로 감싸고 프롭스로 store를 넣어준다.

> 컴포넌트 작성 
##### components/Counter.js
            function Counter({ number, onIncrease, onDecrease }) {
                return (
                    <div>
                        <h1>{number}</h1>
                        <button onClick={onIncrease}>+1</button>
                        <button onClick={onDecrease}>-1</button>
                    </div>
                );
            }
> 컨테이너 작성 
##### containers/CounterContainer.js
            function CounterContainer() {
              const number = useSelector((state) => state.counter);
              const dispatch = useDispatch();

              const onIncrease = () => {
                  dispatch(increase());
              };
              const onDecrease = () => {
                  dispatch(decrease());
              };

              return (
                  <Counter
                      number={number}
                      onIncrease={onIncrease}
                      onDecrease={onDecrease}
                  />
              );
          }

#### 리덕스 미들웨어 작성 예
      > const middleware = store => next => action => {
          // 하고 싶은 작업..
          // 함수를 만드는 함수를 만드는 함수......
        }
          > function middleware(store){
              retrun function (next) {
                return function (action) {
                  
                }
              }
            }
      > *next는 미들웨어에서 액션을 받아 왔을 때,
      다음 미들웨어에게 액션을 전달 하는 함수
      만약에 다음 미들웨어가 없다면 넥스트를 통해 리듀서에게 액션을 전달.

> 미들웨어 작성
##### myLogger.js
```
const myLogger = (store) => (next) => (action) => {
    console.log(action);          // 액션 디스패치 될때 콘솔 출력
    const result = next(action);  // 액션 다음 미들웨어 혹은 다음 리듀서에 전달 하겠다.
    console.log('\t', store.getState());  // 액션이 리듀서에서 처리가 모두 된 후 그 다음 상태를 가져와서 콘솔에 출력.
    return result;                // 컨테이너에서 디스패치 되었을 때
};
// 내보내줌.
export default myLogger;          // 이 과정이 미들웨어를 벌써 다 만든거다. 진짜 ?
```

> 스토어/리덕스에서 applyMiddleware를 불러온다.
##### index.js
```
import { createStore, applyMiddleware } from 'redux';
// 작성한 미들웨어(myLogger)를 apllyMiddleware 함수에 불러와서 넣어줌.
const store = createStore(rootReducer, applyMiddleware(myLogger));
```
    1. 미들웨어 > redux-logger 사용 및 미들웨어와 DevTools 함께 사용
      yarn add redux-logger
      yarn add redux-devtools-extension
      > index.js
        import  { composeWithDevTools } from 'redux-devtools-extension'
        import logger from 'redux-logger';
        const store = createStore(
            rootReducer, // logger를 composeWithDevTools에 넣어준다
            composeWithDevTools(applyMiddleware(logger)),
        );

    2. 미들웨어 > redux-thunk 사용
      리덕스 떵크 작동 원리
        const thunk = store => next => action =>
          typeof action === 'function'
            ? action(store.dispatch, store.getState)
            : next(action)
        ;
          사용 예시
            > const getComments = () => (dispatch, getState) => {
              // 이 안에서는 액션을 dispatch 할 수도 있고
              // getState를 사용하여 현재 상태도 조회 할 수 있다.
              const id = getState().post.activeId;

              // 요청이 시작했음을 알리는 액션
              dispatch({type: 'GET_COMMENTS'});

              // 댓글을 조회하는 프로미스를 반환하는 getComments가 있다고 가정.
              api
                .getComments(id) // 요청!
                .then(comments => dispatch({ type: 'GET_COMMENTS_SUCCESS', id, comments })) // 성공시
                .catch(err => dispatch({ type: 'GET_COMMENTS_ERROR', error: err })); // 실패시
              };
              // 컴포넌트에서
              dispatch(getComments());

> 리덕스 떵크 설치
      
      yarn add redux-thunk
##### index.js
        > import ReduxThunk from 'redux-thunk';
          const store = createStore(
              rootReducer,
              composeWithDevTools(applyMiddleware(ReduxThunk, logger)),
          ); // logger 는 뒤에 넣어 준다.
      
> redux-thunk Promise 다루기
> 
        참고) https://learnjs.vlpt.us/async/
              http://bit.ly/MDNPromise
      
> action 생성 함수, 생략 가능 -> thunk에서 직접 작성하여 디스패치하는 형태로 작성해도 상관 없음
> 
##### module/posts.js
          export const getPosts = () => async (dispatch) => {
              // 요청이 시작 됨
              dispatch({ type: GET_POSTS });

              // API 호출
              try {
                  const posts = await postsAPI.getPosts();
                  // 성공 했을 때
                  dispatch({
                      type: GET_POSTS_SUCCESS,
                      posts,
                  });
              } catch (error) {
                  // 실패 했을 때
                  dispatch({
                      type: GET_POSTS_ERROR,
                      error: error,
                  });
              }
          };
      
> redux-thunk promise 다루기 라우터 연동
      
      yarn add react-router-dom
##### index.js
        import { BrowerRouter } from 'react-router-dom';
        // Provider 를 감싸준다.
        ReactDOM.render(
            <BrowserRouter>
                <Provider store={store}>
                    <App />
                </Provider>
            </BrowserRouter>,
            document.getElementById('root'),
        );

> json-server
>
    npx json-server ./data.json --port 4000

> CORS 와 Webpack DevServer Proxy
>
      현재 상황
        webpack 개발 서버 http://localhost:3000/
                 api 서버 http://localhost:4000/posts
        cors에서는 이것을 따로 설정해줘야 webpack 개발 서버에서 api서버를 사용 할 수 있다.
        json-server 는 이미 이것이 되어 있다.
          Access-Control-Allow-Origin : *
          Access-Control-Allow-Origin : http://localhost:3000
        
> Proxy 설정
##### package.json
    맨 아래 -> "proxy": "http://localhost:4000"
          



## 기타
> open color
>
    https://yeun.github.io/open-color/#gray
> react-icons
> 
    htpps://react-icons.netlify.com
    yarn add react-icons