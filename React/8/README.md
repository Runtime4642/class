
# 8장: React의 고급 개념

React는 컴포넌트 기반 아키텍처를 통해 다양한 기능을 제공하며, 복잡한 애플리케이션을 효율적으로 구축할 수 있습니다. 이 장에서는 React의 고급 개념들을 다루어, 더 나은 설계와 확장성을 가지는 애플리케이션을 만드는 방법을 배웁니다.

## 1. Context API로 전역 상태 관리하기

Context API는 컴포넌트 간 전역적으로 데이터를 공유할 수 있는 방법을 제공합니다. props 드릴링을 피하고, 컴포넌트 트리 깊숙한 곳에서도 데이터를 쉽게 사용할 수 있게 해줍니다.

### Context API 사용 예시

```jsx
const ThemeContext = React.createContext('light');

class App extends Component {
    render() {
        return (
            <ThemeContext.Provider value="dark">
                <Toolbar />
            </ThemeContext.Provider>
        );
    }
}

function Toolbar() {
    return (
        <div>
            <ThemeButton />
        </div>
    );
}

class ThemeButton extends Component {
    static contextType = ThemeContext;
    render() {
        return <button>{this.context} mode</button>;
    }
}
```

- **Context 생성**: `React.createContext()`를 사용하여 Context를 생성합니다.
- **Provider**: Context의 값을 설정하고 자식 컴포넌트들이 이를 사용할 수 있게 합니다.
- **Consumer**: `contextType`을 사용하거나 `Consumer` 컴포넌트를 사용하여 Context 값을 가져올 수 있습니다.

## 2. Higher-Order Components (HOC)

Higher-Order Component는 컴포넌트를 인수로 받아 새로운 컴포넌트를 반환하는 함수입니다. 이는 코드 재사용, 로직 공유, 상태 및 행동을 캡슐화하는 데 유용합니다.

### HOC 사용 예시

```jsx
function withLogging(WrappedComponent) {
    return class extends Component {
        componentDidMount() {
            console.log('Component mounted');
        }

        render() {
            return <WrappedComponent {...this.props} />;
        }
    };
}

class MyComponent extends Component {
    render() {
        return <div>Hello, world!</div>;
    }
}

const MyComponentWithLogging = withLogging(MyComponent);
```

- **HOC 정의**: HOC는 원래의 컴포넌트를 확장하여 추가 기능을 제공하는 컴포넌트를 반환합니다.
- **Props 전달**: HOC에서 원래 컴포넌트로 props를 전달하여 컴포넌트의 기능을 유지합니다.

## 3. Portals와 React의 가상 DOM

Portals를 사용하면 현재 컴포넌트의 DOM 계층 구조 밖에 있는 DOM 노드로 자식을 렌더링할 수 있습니다. 주로 모달, 툴팁, 팝업 등의 UI 요소를 구현할 때 유용합니다.

### Portals 사용 예시

```jsx
import ReactDOM from 'react-dom';

class Modal extends Component {
    render() {
        return ReactDOM.createPortal(
            <div className="modal">
                {this.props.children}
            </div>,
            document.getElementById('modal-root')
        );
    }
}
```

- **ReactDOM.createPortal()**: 첫 번째 인자로 렌더링할 요소를, 두 번째 인자로 렌더링할 DOM 노드를 받습니다.
- **Modal 구현**: 모달과 같은 UI 요소를 DOM의 다른 위치에 렌더링할 수 있어 레이아웃에 영향을 주지 않습니다.

## 4. React.memo와 성능 최적화

React.memo는 함수형 컴포넌트에서 props가 변경되지 않으면 리렌더링을 방지하여 성능을 최적화합니다. 이는 PureComponent와 유사하게 동작합니다.

### React.memo 사용 예시

```jsx
const MyComponent = React.memo(function MyComponent({ name }) {
    console.log('Rendering:', name);
    return <div>{name}</div>;
});
```

- **React.memo**: 고차 함수로, 컴포넌트를 감싸고 props가 변경되지 않으면 컴포넌트를 리렌더링하지 않습니다.

## 5. Error Boundaries

Error Boundaries는 컴포넌트 트리 내에서 발생한 JavaScript 오류를 포착하여, 애플리케이션이 죽지 않고 대체 UI를 렌더링할 수 있게 합니다. 클래스 컴포넌트에서만 구현할 수 있습니다.

### Error Boundary 구현 예시

```jsx
class ErrorBoundary extends Component {
    constructor(props) {
        super(props);
        this.state = { hasError: false };
    }

    static getDerivedStateFromError(error) {
        return { hasError: true };
    }

    componentDidCatch(error, info) {
        console.log('Error:', error, 'Info:', info);
    }

    render() {
        if (this.state.hasError) {
            return <h1>Something went wrong.</h1>;
        }
        return this.props.children;
    }
}
```

- **getDerivedStateFromError**: 오류가 발생하면 상태를 업데이트하여 대체 UI를 렌더링합니다.
- **componentDidCatch**: 오류 로그를 기록하거나 오류 처리 로직을 실행할 수 있습니다.

## 6. React의 Forwarding Refs

Forwarding Refs는 부모 컴포넌트에서 자식 컴포넌트로 ref를 전달하여 자식의 DOM 요소에 접근할 수 있게 합니다.

### Forwarding Ref 예시

```jsx
const FancyButton = React.forwardRef((props, ref) => (
    <button ref={ref} className="fancy-button">
        {props.children}
    </button>
));

const ref = React.createRef();
<FancyButton ref={ref}>Click me!</FancyButton>
```

- **`React.forwardRef()`**: 컴포넌트를 감싸 ref를 전달받고, 이를 하위 DOM 요소에 연결할 수 있습니다.

이와 같이 React의 고급 개념들을 사용하여 더 나은 설계와 기능을 가진 애플리케이션을 개발할 수 있습니다.
