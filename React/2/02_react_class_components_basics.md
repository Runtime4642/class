
# React 클래스 컴포넌트 기초

React에서 클래스 컴포넌트는 상태(state)와 생명주기 메서드(lifecycle methods)를 사용할 수 있어, 함수형 컴포넌트보다 복잡한 기능을 구현할 수 있습니다. 이 장에서는 클래스 컴포넌트의 기본 구조와 props, state 사용법을 다룹니다.

## 1. 클래스 컴포넌트의 정의

React에서 클래스 컴포넌트는 `React.Component`를 상속받아 정의됩니다. 클래스 컴포넌트는 `render()` 메서드를 통해 UI를 반환하며, 이 메서드는 React에 의해 자동으로 호출됩니다.

```jsx
import React, { Component } from 'react';

class MyComponent extends Component {
    render() {
        return <h1>Hello, React!</h1>;
    }
}

export default MyComponent;
```

- **클래스 선언**: 클래스는 `class` 키워드를 사용하여 선언하며, `Component`를 상속받아야 합니다.
- **render() 메서드**: UI를 반환하는 메서드로, JSX를 반환하여 화면에 표시될 내용을 정의합니다.

## 2. props 사용하기

props는 부모 컴포넌트에서 자식 컴포넌트로 데이터를 전달하는 방법입니다. 클래스 컴포넌트에서는 `this.props`를 통해 props에 접근할 수 있습니다.

```jsx
class Welcome extends Component {
    render() {
        return <h1>Hello, {this.props.name}!</h1>;
    }
}

// 사용 예시
<Welcome name="John" />
```

- **this.props**: 클래스 컴포넌트에서는 `this.props`를 통해 props에 접근하여 사용할 수 있습니다.
- **불변성**: props는 읽기 전용이며, 자식 컴포넌트에서 직접 수정할 수 없습니다.

## 3. state와 setState()

클래스 컴포넌트는 `state`를 사용하여 컴포넌트의 상태를 관리할 수 있습니다. state는 컴포넌트 내에서 변경 가능한 데이터이며, `setState()` 메서드를 통해 상태를 업데이트합니다.

```jsx
class Counter extends Component {
    constructor(props) {
        super(props);
        this.state = { count: 0 };
    }

    increment = () => {
        this.setState({ count: this.state.count + 1 });
    }

    render() {
        return (
            <div>
                <p>Count: {this.state.count}</p>
                <button onClick={this.increment}>Increment</button>
            </div>
        );
    }
}
```

- **state 초기화**: `constructor`에서 `this.state` 객체로 초기화합니다. `super(props)`를 호출하여 부모 클래스의 생성자를 초기화해야 합니다.
- **setState()**: 상태를 업데이트하기 위해 `setState()` 메서드를 사용합니다. 이 메서드는 상태를 비동기적으로 업데이트하므로, 상태가 변경된 후의 값을 바로 참조하면 이전 값이 반환될 수 있습니다.
- **이벤트 핸들러 바인딩**: 클래스 메서드를 이벤트 핸들러로 사용할 때, 메서드를 화살표 함수로 정의하거나 `bind`를 통해 `this`를 바인딩해야 합니다.

## 4. 클래스 컴포넌트의 장점과 단점

- **장점**:
  - 생명주기 메서드를 사용할 수 있어, 컴포넌트의 생성 및 업데이트, 제거 시점에서 특정 작업을 수행할 수 있습니다.
  - `state`를 사용하여 컴포넌트 내부에서 동적인 데이터를 관리할 수 있습니다.

- **단점**:
  - 함수형 컴포넌트에 비해 상대적으로 코드가 길고, `this` 바인딩 문제를 해결해야 하는 불편함이 있습니다.
  - React Hooks가 도입된 이후, 함수형 컴포넌트에서도 상태와 생명주기 메서드를 사용할 수 있게 되면서, 클래스 컴포넌트의 사용 빈도가 줄어들고 있습니다.

이와 같이, React 클래스 컴포넌트는 state와 props를 사용하여 동적인 UI를 관리하며, 생명주기 메서드를 통해 컴포넌트의 특정 시점에서 작업을 수행할 수 있습니다.
