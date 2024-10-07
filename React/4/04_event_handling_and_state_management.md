
# 4장: 이벤트 처리와 상태 관리

React에서 이벤트는 HTML의 이벤트 처리 방식과 유사하지만, React만의 특별한 규칙과 방식이 있습니다. 이 장에서는 이벤트 처리와 상태 관리 방법에 대해 다룹니다.

## 1. React에서 이벤트 처리

React의 이벤트는 DOM 요소에서 발생하는 이벤트를 기반으로 하며, `onClick`, `onChange`와 같은 속성을 사용합니다. 하지만 JSX에서는 이벤트 이름이 카멜 표기법(camelCase)으로 작성되어야 하며, 이벤트 핸들러는 함수로 전달됩니다.

```jsx
class ClickButton extends Component {
    handleClick = () => {
        console.log('Button was clicked!');
    };

    render() {
        return <button onClick={this.handleClick}>Click Me</button>;
    }
}
```

- **카멜 표기법**: HTML의 `onclick`은 React에서 `onClick`으로 표기합니다.
- **함수 전달**: 이벤트 핸들러로 함수를 전달해야 하며, 함수 호출이 아니라 함수 자체를 전달해야 합니다.

## 2. 이벤트 핸들러에서 `this` 바인딩

클래스 컴포넌트에서는 `this`가 현재 인스턴스를 가리키도록 바인딩해야 합니다. 이벤트 핸들러를 메서드로 정의할 때, `bind`를 사용하거나 화살표 함수를 이용해 `this`를 자동으로 바인딩할 수 있습니다.

### `bind`를 사용한 예시

```jsx
class ToggleButton extends Component {
    constructor(props) {
        super(props);
        this.state = { isOn: true };
        this.handleToggle = this.handleToggle.bind(this);
    }

    handleToggle() {
        this.setState(prevState => ({ isOn: !prevState.isOn }));
    }

    render() {
        return <button onClick={this.handleToggle}>{this.state.isOn ? 'ON' : 'OFF'}</button>;
    }
}
```

### 화살표 함수를 사용한 예시

```jsx
class ToggleButton extends Component {
    state = { isOn: true };

    handleToggle = () => {
        this.setState(prevState => ({ isOn: !prevState.isOn }));
    };

    render() {
        return <button onClick={this.handleToggle}>{this.state.isOn ? 'ON' : 'OFF'}</button>;
    }
}
```

## 3. 상태 관리 (State Management)

클래스 컴포넌트에서 `state`는 컴포넌트의 동적인 데이터를 저장하고 관리하는 객체입니다. `setState()` 메서드를 사용하여 `state`를 업데이트하며, 업데이트될 때마다 컴포넌트는 다시 렌더링됩니다.

```jsx
class Counter extends Component {
    state = { count: 0 };

    increment = () => {
        this.setState(prevState => ({ count: prevState.count + 1 }));
    };

    decrement = () => {
        this.setState(prevState => ({ count: prevState.count - 1 }));
    };

    render() {
        return (
            <div>
                <p>Count: {this.state.count}</p>
                <button onClick={this.increment}>+</button>
                <button onClick={this.decrement}>-</button>
            </div>
        );
    }
}
```

- **`setState()` 메서드**: 비동기적으로 상태를 업데이트하며, 현재 상태에 따라 새로운 상태를 계산할 수 있습니다.
- **prevState**: 이전 상태를 기반으로 업데이트를 수행할 때 사용됩니다.

## 4. 폼 요소와 상태 관리

React에서 폼 요소(`input`, `textarea`, `select` 등)의 값은 컴포넌트의 state와 연결하여 제어할 수 있습니다. 이를 제어 컴포넌트(Controlled Component)라고 합니다.

```jsx
class Form extends Component {
    state = { name: '' };

    handleChange = (event) => {
        this.setState({ name: event.target.value });
    };

    handleSubmit = (event) => {
        event.preventDefault();
        alert(`Submitted name: ${this.state.name}`);
    };

    render() {
        return (
            <form onSubmit={this.handleSubmit}>
                <input type="text" value={this.state.name} onChange={this.handleChange} />
                <button type="submit">Submit</button>
            </form>
        );
    }
}
```

- **제어 컴포넌트**: 폼 요소의 값은 state에 의해 제어되며, 이벤트 핸들러를 통해 state를 업데이트합니다.
- **이벤트 처리**: 폼 제출 시 `onSubmit` 이벤트를 사용하여 기본 동작(페이지 새로고침)을 막고 데이터를 처리합니다.

## 5. 상태 관리의 모범 사례

- **상태 최소화**: 컴포넌트에 필요한 최소한의 상태만을 저장하여 불필요한 업데이트를 줄입니다.
- **단일 진리의 원천**: 컴포넌트에서 상태는 항상 단 하나의 진리의 원천(Single Source of Truth)이어야 하며, 모든 UI는 이 상태에 따라 동적으로 렌더링되어야 합니다.

이와 같이 React에서 이벤트를 처리하고 상태를 관리함으로써 동적인 UI를 구현할 수 있습니다.
