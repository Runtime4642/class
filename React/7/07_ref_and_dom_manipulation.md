
# 7장: Ref와 DOM 조작

React에서는 직접적으로 DOM에 접근하거나 조작할 필요가 있을 때 `ref`를 사용합니다. `ref`는 DOM 요소나 클래스 컴포넌트에 직접 접근할 수 있는 방법을 제공합니다. 이 장에서는 `ref`를 생성하고 활용하는 방법에 대해 다룹니다.

## 1. Ref의 개념과 사용법

`ref`는 React에서 DOM 요소나 컴포넌트 인스턴스에 접근할 수 있는 속성입니다. 보통 다음과 같은 경우에 사용합니다.

- 포커스, 텍스트 선택, 혹은 미디어의 재생 제어 등과 같은 직접적인 DOM 조작이 필요할 때
- 외부 라이브러리와 통합할 때
- 애니메이션을 구현할 때

### Ref 생성과 사용

React에서는 `React.createRef()`를 사용하여 `ref`를 생성합니다.

```jsx
class InputFocus extends Component {
    constructor(props) {
        super(props);
        this.inputRef = React.createRef();
    }

    focusInput = () => {
        this.inputRef.current.focus();
    };

    render() {
        return (
            <div>
                <input type="text" ref={this.inputRef} />
                <button onClick={this.focusInput}>Focus Input</button>
            </div>
        );
    }
}
```

- **`React.createRef()`**: `ref` 객체를 생성합니다.
- **`ref` 속성**: JSX 요소에 `ref` 속성을 설정하여 해당 요소에 접근할 수 있습니다.
- **`current` 속성**: `ref` 객체의 `current` 속성을 통해 실제 DOM 요소나 컴포넌트 인스턴스에 접근합니다.

## 2. 클래스 컴포넌트에 Ref 적용

`ref`는 DOM 요소뿐만 아니라 클래스 컴포넌트에도 적용할 수 있습니다. 이를 통해 자식 컴포넌트의 메서드나 상태에 접근할 수 있습니다.

```jsx
class Child extends Component {
    alertMessage = () => {
        alert('Hello from child component!');
    };

    render() {
        return <p>Child Component</p>;
    }
}

class Parent extends Component {
    constructor(props) {
        super(props);
        this.childRef = React.createRef();
    }

    callChildMethod = () => {
        this.childRef.current.alertMessage();
    };

    render() {
        return (
            <div>
                <Child ref={this.childRef} />
                <button onClick={this.callChildMethod}>Call Child Method</button>
            </div>
        );
    }
}
```

- **자식 컴포넌트에 `ref` 전달**: 부모 컴포넌트에서 자식 컴포넌트에 `ref`를 전달하여 자식의 메서드나 속성에 접근할 수 있습니다.

## 3. 콜백 Ref

React에서는 콜백 함수를 사용하여 `ref`를 설정할 수도 있습니다. 콜백 `ref`는 컴포넌트가 마운트되거나 언마운트될 때 호출됩니다.

```jsx
class CallbackRefExample extends Component {
    setRef = (element) => {
        this.inputElement = element;
    };

    focusInput = () => {
        if (this.inputElement) this.inputElement.focus();
    };

    render() {
        return (
            <div>
                <input type="text" ref={this.setRef} />
                <button onClick={this.focusInput}>Focus Input</button>
            </div>
        );
    }
}
```

- **콜백 함수**: `ref`에 콜백 함수를 전달하여, 해당 함수가 DOM 요소를 인자로 받습니다.
- **변수에 직접 저장**: 콜백 함수 내에서 DOM 요소를 클래스 속성으로 저장하여 사용할 수 있습니다.

## 4. Ref와 함수형 컴포넌트 (useRef)

함수형 컴포넌트에서는 React Hooks를 통해 `ref`를 사용할 수 있습니다. `useRef` 훅을 사용하여 DOM 요소에 접근하거나 값을 저장할 수 있습니다.

```jsx
import React, { useRef } from 'react';

function FunctionComponent() {
    const inputRef = useRef(null);

    const focusInput = () => {
        if (inputRef.current) inputRef.current.focus();
    };

    return (
        <div>
            <input type="text" ref={inputRef} />
            <button onClick={focusInput}>Focus Input</button>
        </div>
    );
}
```

- **`useRef`**: 함수형 컴포넌트에서 `ref`를 생성하고 사용할 수 있습니다.
- **값 저장**: `useRef`는 컴포넌트가 다시 렌더링되더라도 값을 유지합니다.

## 5. Ref 사용 시 주의사항

- **과도한 사용 자제**: React는 선언형 방식으로 UI를 제어하므로, 직접적으로 DOM을 조작하는 `ref`의 사용은 최소화하는 것이 좋습니다.
- **단방향 데이터 흐름 준수**: `ref`는 컴포넌트 간의 데이터를 전달하는 용도로 사용되지 않아야 하며, props와 state를 통해 데이터가 흐르도록 유지하는 것이 중요합니다.

이와 같이 `ref`를 사용하여 React에서 DOM 요소나 컴포넌트 인스턴스에 접근하고 조작할 수 있습니다. 적절하게 사용하면 복잡한 UI를 효율적으로 관리할 수 있습니다.
