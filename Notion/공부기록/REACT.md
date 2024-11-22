### **JSX**

- **자바스크립트의 확장 문법으로 XML과 비슷하게 생김**
- **return을 해줄 때 하나의 요소로 감싸 주어야하는 이유 : Virtual DOM에서 컴포넌트의 변화를 감지해 낼 때 효율적으로 비교할 수 있도록**

### 함수형 컴포넌트 vs 클래스형 컴포넌트

```JavaScript
// 함수형 컴포넌트
function App() {
	const name = "리액트";
	return <div className="react">{name}</div>
}

export default App;
```

**⇒ state 기능 및 라이프사이클 기능을 사용할수 없음 ⇒ Hooks으로 해결**

**→ 클래스형보다 메모리 사용, 파일 크기가 작다**

```JavaScript
// 클래스형 컴포넌트
class App extends Component{
	render() {
		const name = "리액트";
		return <div className="react">{name}</div>;
	}
}

export default App;
```

**→ render함수가 꼭 있어야함**