
# 5장: 조건부 렌더링과 리스트 렌더링

React에서는 조건에 따라 렌더링을 다르게 하거나, 데이터를 기반으로 리스트를 동적으로 생성할 수 있습니다. 이 장에서는 조건부 렌더링과 리스트 렌더링을 구현하는 방법에 대해 다룹니다.

## 1. 조건부 렌더링 (Conditional Rendering)

조건부 렌더링은 특정 조건에 따라 컴포넌트의 일부를 렌더링하거나 숨기는 방법입니다. JavaScript의 조건문(`if`, 삼항 연산자 등)을 사용하여 구현할 수 있습니다.

### `if` 문을 사용한 조건부 렌더링

```jsx
class Greeting extends Component {
    render() {
        const isLoggedIn = this.props.isLoggedIn;
        if (isLoggedIn) {
            return <h1>Welcome back!</h1>;
        } else {
            return <h1>Please sign in.</h1>;
        }
    }
}
```

### 삼항 연산자를 사용한 조건부 렌더링

```jsx
class Greeting extends Component {
    render() {
        return this.props.isLoggedIn ? <h1>Welcome back!</h1> : <h1>Please sign in.</h1>;
    }
}
```

### 논리 연산자 `&&`를 사용한 렌더링

```jsx
class Notification extends Component {
    render() {
        const hasUnreadMessages = this.props.unreadMessages.length > 0;
        return (
            <div>
                <h1>Hello!</h1>
                {hasUnreadMessages && <p>You have {this.props.unreadMessages.length} unread messages.</p>}
            </div>
        );
    }
}
```

- **삼항 연산자**: 간결하게 조건에 따른 렌더링을 표현할 수 있습니다.
- **논리 연산자 `&&`**: 조건이 참일 때만 특정 요소를 렌더링합니다.

## 2. 리스트 렌더링 (List Rendering)

리스트 렌더링은 배열 데이터를 기반으로 여러 개의 컴포넌트를 동적으로 생성하는 방식입니다. `map()` 함수를 사용하여 배열의 각 요소를 컴포넌트로 변환합니다.

```jsx
class NameList extends Component {
    render() {
        const names = ['Alice', 'Bob', 'Charlie'];
        return (
            <ul>
                {names.map((name, index) => (
                    <li key={index}>{name}</li>
                ))}
            </ul>
        );
    }
}
```

- **`map()` 함수**: 배열의 각 요소를 순회하며 컴포넌트를 반환합니다.
- **Key 속성**: 리스트 렌더링 시 각 컴포넌트에 고유한 `key` 값을 설정해야 합니다. 이는 React가 각 요소를 식별하고 효율적으로 업데이트할 수 있도록 돕습니다.

### Key의 중요성

React에서 Key는 컴포넌트를 식별하는 데 사용되며, 리스트가 업데이트될 때 성능 최적화에 중요한 역할을 합니다. Key가 없거나 중복될 경우, 예상치 못한 렌더링 이슈가 발생할 수 있습니다.

```jsx
class TodoList extends Component {
    render() {
        const todos = this.props.todos;
        return (
            <ul>
                {todos.map(todo => (
                    <li key={todo.id}>{todo.text}</li>
                ))}
            </ul>
        );
    }
}
```

- **고유한 ID 사용**: Key는 보통 데이터의 고유한 ID를 사용하여 설정하는 것이 좋습니다.

## 3. 리스트와 조건부 렌더링 결합

조건부 렌더링과 리스트 렌더링을 함께 사용할 수도 있습니다. 예를 들어, 특정 조건을 만족하는 리스트 요소만 렌더링하거나, 빈 리스트일 때 대체 요소를 렌더링할 수 있습니다.

```jsx
class Mailbox extends Component {
    render() {
        const unreadMessages = this.props.unreadMessages;
        return (
            <div>
                <h1>Mailbox</h1>
                {unreadMessages.length > 0 ? (
                    <ul>
                        {unreadMessages.map((message, index) => (
                            <li key={index}>{message}</li>
                        ))}
                    </ul>
                ) : (
                    <p>No new messages</p>
                )}
            </div>
        );
    }
}
```

- **리스트 조건부 렌더링**: 리스트가 비어 있을 때는 대체 요소를, 데이터가 있을 때는 해당 데이터를 렌더링합니다.

## 4. 리스트 렌더링의 모범 사례

- **Key는 고유하고 불변이어야 함**: Key로 배열의 인덱스를 사용하는 것은 추천되지 않습니다. 데이터가 변경될 때 인덱스가 바뀌면 예상치 못한 결과를 초래할 수 있습니다.
- **데이터를 기준으로 렌더링 최적화**: 필요한 경우, `shouldComponentUpdate()` 메서드와 같은 생명주기 메서드를 활용하여 렌더링을 최적화할 수 있습니다.

이와 같이 React에서 조건부 렌더링과 리스트 렌더링을 효과적으로 사용하여 동적인 UI를 구현할 수 있습니다.
