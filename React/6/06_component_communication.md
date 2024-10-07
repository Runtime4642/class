
# 6장: 컴포넌트 간의 데이터 통신

React에서는 컴포넌트 간의 데이터 통신을 위해 props와 state를 활용합니다. 부모-자식 관계에서 데이터를 전달하거나, 상태를 끌어올리는 방식으로 컴포넌트 간의 데이터를 공유할 수 있습니다.

## 1. 부모에서 자식으로 데이터 전달 (Props)

React에서 가장 기본적인 데이터 전달 방식은 부모 컴포넌트가 자식 컴포넌트에 props를 통해 데이터를 전달하는 것입니다. props는 읽기 전용이며, 자식 컴포넌트에서 수정할 수 없습니다.

```jsx
class Parent extends Component {
    render() {
        return <Child message="Hello from parent!" />;
    }
}

class Child extends Component {
    render() {
        return <p>{this.props.message}</p>;
    }
}
```

- **읽기 전용**: 자식 컴포넌트는 props를 읽기만 할 수 있으며, 수정할 수 없습니다.
- **props 구조 분해**: 자식 컴포넌트에서 props를 구조 분해 할당하여 사용할 수 있습니다.

## 2. 자식에서 부모로 데이터 전달 (콜백 함수 사용)

자식 컴포넌트가 부모 컴포넌트로 데이터를 전달하려면, 부모에서 콜백 함수를 props로 전달하고, 자식 컴포넌트에서 해당 콜백을 호출하여 데이터를 전달합니다.

```jsx
class Parent extends Component {
    handleData = (data) => {
        console.log('Received from child:', data);
    };

    render() {
        return <Child onData={this.handleData} />;
    }
}

class Child extends Component {
    sendData = () => {
        this.props.onData('Data from child');
    };

    render() {
        return <button onClick={this.sendData}>Send Data</button>;
    }
}
```

- **콜백 함수**: 부모 컴포넌트에서 정의된 함수를 자식 컴포넌트로 전달하여 자식이 해당 함수를 호출할 수 있게 합니다.
- **데이터 전달**: 자식 컴포넌트는 부모 컴포넌트의 콜백 함수를 호출할 때 데이터를 인자로 전달합니다.

## 3. 상태 끌어올리기 (Lifting State Up)

두 개 이상의 컴포넌트가 동일한 데이터를 필요로 할 때, 가장 가까운 공통 부모 컴포넌트로 상태를 끌어올려서 관리할 수 있습니다. 이를 통해 공통 부모 컴포넌트가 상태를 관리하고, 자식 컴포넌트들이 props로 데이터를 공유할 수 있게 합니다.

```jsx
class Parent extends Component {
    state = { value: '' };

    handleChange = (e) => {
        this.setState({ value: e.target.value });
    };

    render() {
        return (
            <div>
                <Input value={this.state.value} onChange={this.handleChange} />
                <Display value={this.state.value} />
            </div>
        );
    }
}

class Input extends Component {
    render() {
        return (
            <input
                type="text"
                value={this.props.value}
                onChange={this.props.onChange}
            />
        );
    }
}

class Display extends Component {
    render() {
        return <p>{this.props.value}</p>;
    }
}
```

- **상태 끌어올리기**: 공통 부모 컴포넌트에서 상태를 관리하고, 자식 컴포넌트들이 props를 통해 동일한 데이터를 공유합니다.
- **중앙 집중식 관리**: 상태를 중앙에서 관리함으로써 데이터의 일관성을 유지하고, 컴포넌트 간의 데이터 흐름을 명확히 할 수 있습니다.

## 4. Context API를 통한 전역 데이터 관리

props를 통해 데이터를 전달하는 방식은 트리 구조가 깊어질수록 비효율적일 수 있습니다. React에서는 이러한 문제를 해결하기 위해 Context API를 제공합니다. Context는 전역적으로 데이터를 관리하고, 필요한 컴포넌트들에만 데이터를 전달할 수 있습니다.

### Context 생성 및 사용 예시

```jsx
const MyContext = React.createContext();

class Parent extends Component {
    state = { value: 'Hello Context' };

    render() {
        return (
            <MyContext.Provider value={this.state.value}>
                <Child />
            </MyContext.Provider>
        );
    }
}

class Child extends Component {
    static contextType = MyContext;

    render() {
        return <p>{this.context}</p>;
    }
}
```

- **Context 생성**: `React.createContext()`를 사용하여 Context를 생성합니다.
- **Provider 사용**: Context의 `Provider`를 사용하여 자식 컴포넌트들에게 데이터를 제공합니다.
- **Consumer 사용**: Context의 데이터를 사용하고자 하는 컴포넌트에서는 `Consumer`나 `contextType`을 사용하여 접근할 수 있습니다.

## 5. 컴포넌트 간의 데이터 통신 모범 사례

- **상태 최소화**: 컴포넌트의 상태는 가능한 최소화하여 필요한 데이터만 관리합니다.
- **상태 끌어올리기**: 공통 부모 컴포넌트를 사용하여 데이터의 일관성을 유지하고 컴포넌트 간의 통신을 간소화합니다.
- **Context 사용**: 복잡한 컴포넌트 트리에서 전역 상태가 필요한 경우 Context를 사용하여 데이터를 관리합니다.

이와 같이 React에서는 다양한 방법을 통해 컴포넌트 간의 데이터를 전달하고 상태를 관리할 수 있습니다.
