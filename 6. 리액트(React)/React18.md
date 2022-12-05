## 🐬 React 18의 핵심 변경점 

1. 자동 배치(Automatic Batching)
2. 동시성(Concurrent) 기능 
   : startTransition이나 선택적(Selective) Hydration 등의 동시성(Concurrent)기능이 추가되었습니다.
3. 서스펜스(Suspense)를 지원하는 새로운 서버사이드 렌더링 아키텍처
  : 새로운 서버 사이드 렌더링 아키텍처가 도입되었습니다. 이 아키텍처에서는 <Suspense>와 React.lazy를 지원하며, 기존 서버사이드 렌더링의 근본적인 문제를 해결했습니다. 
4. ReactDOM.render()가 Deprecated되고 새롭게 ReactDom.createRoot() API가 그 자리를 이어갑니다. 

<br>
<br>
  
  
## 🐬 자동 배치 (Automatic Batching)
리액트의 배치란, 리액트가 더 나은 성능을 위해 여러 개의 상태 업데이트를 한번의 리렌더링(re-render)으로 묶는 작업을 의미한다.

  <br>
  
```
function App() {
 const [count, setCount] = useState(0);
 const [flag, setFlag] = useState(false);

 function handleClick() {
 setCount(c => c + 1); // 아직 리렌더링 되지 않습니다.
 setFlag(f => !f); // 아직 리렌더링 되지 않습니다.
 // 리액트는 오직 마지막에만 리렌더링을 한 번 수행합니다. (배치 적용)
 }

 return (
 <div>
 <button onClick={handleClick}>Next</button>
 <h1 style={{ color: flag ? "blue" : "black" }}>{count}</h1>
 </div>
 );
}
```
<br>
  
위의 handleClick 이벤트 핸들러 함수에서는 상태 업데이트를 두 번 수행한다. 하지만, 리액트는 언제나 배치를 수행하여 이 두번의 상태 업데이트를 한번의 리렌더링으로 처리한다. 이를 통해 불필요한 여러 번의 리렌더링을 방지하고 의도치 않은 버그를 예방할 수 있다. 
하지만 배치가 수행되지 않는 예외가 존재한다. 

  <br>
  
```
function App() {
 const [count, setCount] = useState(0);
 const [flag, setFlag] = useState(false);

 function handleClick() {
 fetchSomething().then(() => {
 // 리액트 17 및 그 이전 버전에서는 배치가 수행되지 않습니다. 왜냐하면
 // 이 코드들은 이벤트 이후의 콜백에서 실행되기 때문입니다.
 setCount(c => c + 1); // 리렌더링 
setFlag(f => !f); // 리렌더링
 });
 }

 return (
 <div>
 <button onClick={handleClick}>Next</button>
 <h1 style={{ color: flag ? "blue" : "black" }}>{count}</h1>
 </div>
 );
}
```
  
  <br>
  
리액트 17 이전의 기존 리액트에서는 위와 같이 이벤트 핸들러 함수 내에서 실행되는 상태 업데이트가 아닌 경우 배치가 동작하지 않는다. 

하지만 리액트 18부터 자동 배치(Automatic Batching)라는 것이 추가되었다. 자동 배치란, 일반적인 이벤트 핸들러 함수 스코프에서 상태 업데이트가 발생하지 않더라도 자동으로 배치를 적용해주는 것을 뜻한다. 

  <br>
  
```
setTimeout(() => {
 setCount(c => c + 1);
 setFlag(f => !f);
 // 리액트는 오직 마지막에만 리렌더링을 한 번 수행합니다. (배치 적용)
}, 1000);

fetch(/*...*/).then(() => {
 setCount(c => c + 1);
 setFlag(f => !f);
 // 리액트는 오직 마지막에만 리렌더링을 한 번 수행합니다. (배치 적용)
})

elm.addEventListener('click', () => {
 setCount(c => c + 1);
 setFlag(f => !f);
 // 리액트는 오직 마지막에만 리렌더링을 한 번 수행합니다. (배치 적용)
});
```
  
  <br>

이 자동 배치를 사용하기 위해서는 컴포넌트 트리를 기존의 ReactDOM.render 함수 대신 새로운 ReactDOM.createRoot 함수를 사용해야 한다. 

한편, 매우 드문 경우이기는 하나 상태 업데이트에 배치가 적용되지 않았으면 하는 경우가 있다. 그 경우에는 새롭게 추가된 ReactDOM.flushSync 함수를 사용하면 해결할 수 있다. 

  
  <br>
<br>

## 🐬 동시성 (Automatic Batching) 기능 
지금까지 Concurrent Mode라고 알려졌던 리액트의 차기 핵심 기능 중 일부가 React 18에 추가된다. 

동시성 기능을 이해하기 위해 상태 업데이트를 어떻게 분류할 수 있는지 생각해봐야 함. 

  <br>
  
### 💡 상태 업데이트 
	- 긴급 업데이트 : 직접적인 상호 작용 반영 (타이핑, 오버, 스크롤링 등) 
	- 전환 업데이트 : 하나의 뷰에서 다른 뷰로의 UI 전환 

  <br>

긴급 업데이트는 사용자의 입력에 따라 즉각적으로 업데이트 되지 않으면 (화면 멈춤, 렉 등) 문제가 있다고 느끼는 영역입니다. 반면 전환 업데이트는 화면에 즉시 나타나는 걸 기대하지 않는 영역입니다. 

  <br>
  
#### 긴급 업데이트
검색 기능에서 사용자가 검색하기 위해 직접 리액트를 입력한다고 가정해보겠습니다. 'ㄹ','ㅣ','ㅇ','ㅐ','ㄱ','ㅌ','ㅡ' 각각의 키를 입력할 때, 키 입력이 올바르게 되었다는 결과는 즉각적으로 보여줘야 합니다. 사용자가 그렇게 되길 기대하기 때문입니다. 만약 이때 렉이나 화면 멈춤 등이 발생한다면 사용자는 부정적인 경험을 하게 됩니다. 

  
  <br>
  
#### 전환 업데이트
반면 하단의 추천 검색어로 뜨는 자동 완성 영역의 경우 그렇지 않습니다. 만약 디바이스의 성능이 권장 사양보다 낮아 렌더링 성능이 낮거나, 네트워크 속도가 느린 상황 등의 이유로 업데이트가 늦어질 수도 있다. 중요한 건 전환 업데이트 때문에 긴급 업데이트가 방해되면 안된다. 

  <br>
  
### 문제 
하지만 React 17까지는 상태 업데이트를 긴급 혹은 전환으로 명시하는 방법이 없었다. 모든 상태 업데이트는 긴급 업데이트였다. 그래서  setTimeout이나 throttle, debounce 등의 테크닉을 써서 긴급 업데이트 방해를 우회하는 것이 최선.

하지만 React 18 부터는 startTransition API를 제공함으로써 전환 업데이트를 명시적으로 구분하여 상태 업데이트를 진행할 수 있게 되었다. 

  <br>
  
```
import { useTransition } from 'react';

function SearchBar() {
 const [isPending, startTransition] = useTransition();

 // ...

 function handleChange(e) {
 const input = e.target.value;

 // 긴급 업데이트: 타이핑 결과를 보여준다.
 setInputValue(input);

 // 이 안의 모든 상태 업데이트는 전환 업데이트가 된다.
 startTransition(() => {
 // 전환 업데이트: 결과를 보여준다.
 setSearchQuery(input);
 });
 }

 // ...
}

```
  
  <br>

참고로, 소수의 케이스에 대응하기 위해 Hook을 거치지 않고 React.startTransition을 사용할 수도 있다. 

startTransition 

	- 느린 렌더링 : 작업량이 많아 결과를 보여주기 위한 UI 전환까지 시간이 걸립니다. 
	- 느린 네트워크 : 네트워크로부터 데이터를 기다리기 위한 시간이 걸립니다. Suspense와 연계. 

<br>
<br>
  
## 🐬 서스펜스(Suspense)를 지원하는 새로운 서버 사이드 렌더링 아키텍처 

React 18에서는 새로운 서버 사이드 렌더링(SSR) 아키텍처가 적용되었다. 새롭게 pipeToNodeWritable API가 추가되었고, 이 API를 사용하면 SSR을 통해 <Suspense>를 사용할 수 있게 되었다. 

즉, React.lazy를 서버 사이드 렌더링에서 사용할 수 있게 되었다. 

	1. 서버에서 전체 앱의 데이터를 받는다 (Data Fetching)
	2. 그 후, 서버에서 전체 앱을 HTML로 렌더링한 후 Response로 전송한다. 
	3. 그 후, 클라이언트에서 전체 앱의 자바스크립트 코드를 로드한다. 

