
# 10장: 프로젝트 실습

React의 기본 개념과 고급 기술들을 실습하며 배워본 후, 이제 실제 프로젝트를 통해 이러한 기술들을 적용해보겠습니다. 이 장에서는 간단한 Todo 리스트 애플리케이션과 사용자 인증 폼, 그리고 전역 상태 관리를 이용한 데이터 Fetch를 구현해 봅니다.

## 1. Todo 리스트 애플리케이션 만들기

이 실습에서는 상태 관리, 이벤트 처리, 그리고 리스트 렌더링을 사용하여 간단한 Todo 리스트를 만듭니다.

### Todo 리스트 구성 요소

- **입력 필드**: 사용자가 할 일을 입력할 수 있는 텍스트 필드
- **추가 버튼**: 입력된 할 일을 추가하는 버튼
- **리스트**: 추가된 할 일들을 렌더링하는 리스트
- **삭제 버튼**: 각 항목을 삭제할 수 있는 버튼

### Todo 리스트 코드 예시

```jsx
import React, { Component } from 'react';

class TodoApp extends Component {
    state = {
        todos: [],
        newTodo: '',
    };

    handleChange = (e) => {
        this.setState({ newTodo: e.target.value });
    };

    addTodo = () => {
        if (this.state.newTodo.trim() !== '') {
            this.setState(prevState => ({
                todos: [...prevState.todos, prevState.newTodo],
                newTodo: '',
            }));
        }
    };

    removeTodo = (index) => {
        this.setState(prevState => ({
            todos: prevState.todos.filter((_, i) => i !== index),
        }));
    };

    render() {
        return (
            <div>
                <h1>Todo List</h1>
                <input
                    type="text"
                    value={this.state.newTodo}
                    onChange={this.handleChange}
                />
                <button onClick={this.addTodo}>Add</button>
                <ul>
                    {this.state.todos.map((todo, index) => (
                        <li key={index}>
                            {todo}
                            <button onClick={() => this.removeTodo(index)}>Delete</button>
                        </li>
                    ))}
                </ul>
            </div>
        );
    }
}

export default TodoApp;
```

- **상태 관리**: `state`를 사용하여 할 일 목록과 입력 값을 관리합니다.
- **이벤트 처리**: 입력 값 변경, 추가, 삭제 등의 이벤트를 처리하여 UI를 업데이트합니다.

## 2. 사용자 인증 폼 구현

사용자 로그인 폼을 만들어, 입력 필드와 제출 버튼을 구현하고 폼 제출 시 API 호출을 통해 인증을 처리합니다.

### 사용자 인증 폼 코드 예시

```jsx
class LoginForm extends Component {
    state = {
        username: '',
        password: '',
    };

    handleChange = (e) => {
        this.setState({ [e.target.name]: e.target.value });
    };

    handleSubmit = (e) => {
        e.preventDefault();
        // 실제 인증 로직은 여기에서 처리됩니다.
        alert(`Username: ${this.state.username}, Password: ${this.state.password}`);
    };

    render() {
        return (
            <form onSubmit={this.handleSubmit}>
                <input
                    type="text"
                    name="username"
                    placeholder="Username"
                    value={this.state.username}
                    onChange={this.handleChange}
                />
                <input
                    type="password"
                    name="password"
                    placeholder="Password"
                    value={this.state.password}
                    onChange={this.handleChange}
                />
                <button type="submit">Login</button>
            </form>
        );
    }
}
```

- **폼 처리**: 입력 필드와 제출 버튼을 포함한 폼을 구성하고, 제출 시 기본 동작을 방지하며 사용자 입력 데이터를 처리합니다.
- **이벤트 바인딩**: 입력 필드에서 변경된 값을 상태에 반영하고, 폼 제출 시 상태 값을 활용합니다.

## 3. 전역 상태 관리와 데이터 Fetch

전역 상태 관리와 Context API를 이용하여 외부 API로부터 데이터를 Fetch하고, 전역 상태를 업데이트하여 애플리케이션의 여러 컴포넌트에서 이를 사용할 수 있도록 합니다.

### 데이터 Fetch 및 전역 상태 관리 예시

```jsx
const DataContext = React.createContext();

class DataProvider extends Component {
    state = {
        data: null,
        loading: true,
        error: null,
    };

    componentDidMount() {
        fetch('https://api.example.com/data')
            .then(response => response.json())
            .then(data => this.setState({ data, loading: false }))
            .catch(error => this.setState({ error, loading: false }));
    }

    render() {
        return (
            <DataContext.Provider value={this.state}>
                {this.props.children}
            </DataContext.Provider>
        );
    }
}

function DataDisplay() {
    return (
        <DataContext.Consumer>
            {({ data, loading, error }) => {
                if (loading) return <p>Loading...</p>;
                if (error) return <p>Error occurred: {error.message}</p>;
                return <pre>{JSON.stringify(data, null, 2)}</pre>;
            }}
        </DataContext.Consumer>
    );
}

function App() {
    return (
        <DataProvider>
            <h1>Data Fetch Example</h1>
            <DataDisplay />
        </DataProvider>
    );
}
```

- **Context API**: 데이터를 전역으로 관리하고, `Provider`를 통해 모든 하위 컴포넌트에서 접근할 수 있도록 합니다.
- **데이터 Fetch**: 외부 API로부터 데이터를 가져와 상태를 업데이트하고, 이를 Context를 통해 공유합니다.

## 4. 프로젝트 실습의 모범 사례

- **컴포넌트 분리**: 각 기능별로 컴포넌트를 분리하여 코드의 재사용성을 높이고 유지보수를 용이하게 합니다.
- **상태 관리와 전역 상태의 활용**: 상태가 필요한 곳에만 적절히 사용하고, 전역적으로 관리가 필요한 경우 Context API나 Redux와 같은 도구를 사용합니다.
- **비동기 처리와 에러 핸들링**: 외부 API 호출 시 로딩 상태와 에러 처리를 명확하게 하여 사용자 경험을 향상시킵니다.

이 실습을 통해 React 애플리케이션의 기본적인 구조와 외부 통합, 그리고 상태 관리 방법을 익힐 수 있습니다.
