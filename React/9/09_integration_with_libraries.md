
# 9장: 리액트와 외부 라이브러리 통합

React는 다양한 외부 라이브러리와의 통합이 용이하며, 이를 통해 애플리케이션의 기능을 확장할 수 있습니다. 이 장에서는 API 통신, 상태 관리 라이브러리인 Redux, 그리고 React Router를 사용한 페이지 네비게이션 구현을 다룹니다.

## 1. 외부 API 통신 (Axios 활용)

외부 API와 통신하기 위해 Axios와 같은 라이브러리를 사용할 수 있습니다. Axios는 Promise 기반의 HTTP 클라이언트로, React에서 API 요청을 간단히 처리할 수 있습니다.

### Axios 사용 예시

```bash
npm install axios
```

```jsx
import React, { Component } from 'react';
import axios from 'axios';

class DataFetcher extends Component {
    state = {
        data: null,
        loading: true,
        error: null,
    };

    componentDidMount() {
        axios.get('https://api.example.com/data')
            .then(response => {
                this.setState({ data: response.data, loading: false });
            })
            .catch(error => {
                this.setState({ error, loading: false });
            });
    }

    render() {
        const { data, loading, error } = this.state;
        if (loading) return <p>Loading...</p>;
        if (error) return <p>Error occurred: {error.message}</p>;
        return <div>{JSON.stringify(data)}</div>;
    }
}
```

- **Axios 설치**: npm을 통해 Axios를 설치합니다.
- **API 요청**: `componentDidMount`에서 API 요청을 수행하여 데이터를 가져오고 상태를 업데이트합니다.

## 2. Redux 도입과 상태 관리

Redux는 전역 상태 관리를 위해 자주 사용되는 라이브러리입니다. 컴포넌트 간에 상태를 쉽게 공유하고 관리할 수 있습니다. Redux를 React와 함께 사용하려면 `react-redux` 라이브러리를 추가로 설치해야 합니다.

### Redux 설치

```bash
npm install redux react-redux
```

### Redux 사용 예시

```jsx
import { createStore } from 'redux';
import { Provider, connect } from 'react-redux';

// 초기 상태와 리듀서 정의
const initialState = { count: 0 };

function counterReducer(state = initialState, action) {
    switch (action.type) {
        case 'INCREMENT':
            return { count: state.count + 1 };
        case 'DECREMENT':
            return { count: state.count - 1 };
        default:
            return state;
    }
}

// 스토어 생성
const store = createStore(counterReducer);

class Counter extends Component {
    render() {
        const { count, increment, decrement } = this.props;
        return (
            <div>
                <p>Count: {count}</p>
                <button onClick={increment}>Increment</button>
                <button onClick={decrement}>Decrement</button>
            </div>
        );
    }
}

// Redux state와 action을 컴포넌트의 props로 매핑
const mapStateToProps = state => ({ count: state.count });
const mapDispatchToProps = dispatch => ({
    increment: () => dispatch({ type: 'INCREMENT' }),
    decrement: () => dispatch({ type: 'DECREMENT' }),
});

const ConnectedCounter = connect(mapStateToProps, mapDispatchToProps)(Counter);

// App 컴포넌트에 Provider 추가
function App() {
    return (
        <Provider store={store}>
            <ConnectedCounter />
        </Provider>
    );
}
```

- **스토어 생성**: `createStore`를 사용하여 Redux 스토어를 생성합니다.
- **Provider**: `Provider`로 컴포넌트를 감싸서 Redux 스토어를 모든 하위 컴포넌트에서 접근할 수 있게 합니다.
- **connect**: 컴포넌트를 Redux 스토어에 연결하여 상태와 액션을 props로 전달합니다.

## 3. React Router를 사용한 페이지 네비게이션

React Router는 SPA(Single Page Application)에서 페이지 전환을 구현할 수 있도록 도와주는 라이브러리입니다. `react-router-dom`을 사용하여 라우팅을 설정할 수 있습니다.

### React Router 설치

```bash
npm install react-router-dom
```

### React Router 사용 예시

```jsx
import { BrowserRouter as Router, Route, Switch, Link } from 'react-router-dom';

function Home() {
    return <h2>Home Page</h2>;
}

function About() {
    return <h2>About Page</h2>;
}

function App() {
    return (
        <Router>
            <nav>
                <Link to="/">Home</Link> | <Link to="/about">About</Link>
            </nav>
            <Switch>
                <Route exact path="/" component={Home} />
                <Route path="/about" component={About} />
            </Switch>
        </Router>
    );
}
```

- **Router 설정**: `BrowserRouter`로 애플리케이션을 감싸고, `Route`를 사용하여 각 경로에 해당하는 컴포넌트를 렌더링합니다.
- **Link 사용**: `Link` 컴포넌트를 사용하여 네비게이션 링크를 설정할 수 있습니다.

## 4. 외부 라이브러리와의 통합 모범 사례

- **외부 API 호출은 컴포넌트의 생명주기와 맞추기**: `componentDidMount`에서 API 요청을 수행하여 컴포넌트가 마운트될 때 데이터를 가져옵니다.
- **전역 상태 관리는 Redux와 Context API 활용**: 복잡한 상태를 관리할 때는 전역 상태 관리 라이브러리를 사용하여 코드를 깔끔하게 유지합니다.
- **라우터 설정은 SPA의 핵심**: React Router를 사용하여 SPA에서의 사용자 경험을 개선하고, 페이지 전환을 부드럽게 구현합니다.

이와 같이 React에서 외부 라이브러리와 통합하여 애플리케이션의 기능을 확장하고, 복잡한 상태를 관리할 수 있습니다.
