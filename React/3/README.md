
# React 생명주기 (Lifecycle Methods)

클래스 컴포넌트에서는 컴포넌트의 생명주기를 관리할 수 있는 다양한 메서드를 제공합니다. 이 장에서는 React 클래스 컴포넌트의 생명주기 메서드와 그 사용법에 대해 다룹니다.

## 1. 생명주기 개요

React 컴포넌트는 생성, 업데이트, 그리고 제거의 세 가지 주요 단계로 구성된 생명주기를 가지고 있습니다.

- **마운트(Mounting)**: 컴포넌트가 DOM에 삽입될 때 호출되는 메서드들입니다.
- **업데이트(Updating)**: 컴포넌트의 props나 state가 변경될 때 호출되는 메서드들입니다.
- **언마운트(Unmounting)**: 컴포넌트가 DOM에서 제거될 때 호출되는 메서드입니다.

## 2. 마운트 단계

마운트 단계에서는 컴포넌트가 생성되어 DOM에 삽입됩니다. 주요 메서드는 다음과 같습니다.

- **constructor()**: 컴포넌트가 처음 생성될 때 호출되며, state를 초기화하거나 메서드를 바인딩할 때 사용됩니다.
- **static getDerivedStateFromProps()**: props로부터 state를 업데이트할 수 있는 정적 메서드입니다. 컴포넌트가 렌더링되기 직전에 호출됩니다.
- **render()**: 컴포넌트의 UI를 정의하는 메서드입니다. 반드시 JSX를 반환해야 하며, DOM이 구성됩니다.
- **componentDidMount()**: 컴포넌트가 마운트된 후 호출되며, 주로 외부 API 호출이나 DOM 조작을 수행할 때 사용됩니다.

```jsx
class MyComponent extends Component {
    constructor(props) {
        super(props);
        this.state = { data: null };
    }

    componentDidMount() {
        // 외부 API 호출 예시
        fetch('https://api.example.com/data')
            .then(response => response.json())
            .then(data => this.setState({ data }));
    }

    render() {
        return <div>{this.state.data ? this.state.data : 'Loading...'}</div>;
    }
}
```

## 3. 업데이트 단계

업데이트 단계에서는 컴포넌트의 props 또는 state가 변경될 때 호출됩니다. 주요 메서드는 다음과 같습니다.

- **static getDerivedStateFromProps()**: 마운트와 업데이트 단계 모두에서 호출되며, props 변화에 따라 state를 업데이트할 수 있습니다.
- **shouldComponentUpdate()**: 컴포넌트가 업데이트될지 여부를 결정하는 메서드입니다. 성능 최적화를 위해 조건부로 렌더링을 방지할 수 있습니다.
- **render()**: 변경된 상태나 props에 따라 UI를 다시 렌더링합니다.
- **getSnapshotBeforeUpdate()**: 실제 DOM이 업데이트되기 직전에 호출되며, 이전 DOM 상태를 캡처하여 저장할 수 있습니다.
- **componentDidUpdate()**: 업데이트가 완료된 후 호출되며, 이전 props나 state와 비교하여 추가 작업을 수행할 수 있습니다.

```jsx
componentDidUpdate(prevProps, prevState) {
    if (this.state.count !== prevState.count) {
        console.log('Count가 업데이트되었습니다:', this.state.count);
    }
}
```

## 4. 언마운트 단계

언마운트 단계에서는 컴포넌트가 DOM에서 제거될 때 호출됩니다.

- **componentWillUnmount()**: 컴포넌트가 제거되기 직전에 호출되며, 타이머 해제, 구독 해제, 또는 메모리 정리와 같은 작업을 수행할 수 있습니다.

```jsx
componentWillUnmount() {
    clearInterval(this.timerID);
}
```

## 5. 생명주기 메서드의 사용 예시

```jsx
class Clock extends Component {
    constructor(props) {
        super(props);
        this.state = { time: new Date() };
    }

    componentDidMount() {
        this.timerID = setInterval(() => this.tick(), 1000);
    }

    componentDidUpdate() {
        console.log('컴포넌트가 업데이트되었습니다.');
    }

    componentWillUnmount() {
        clearInterval(this.timerID);
    }

    tick() {
        this.setState({ time: new Date() });
    }

    render() {
        return <h1>{this.state.time.toLocaleTimeString()}</h1>;
    }
}
```

이와 같이 생명주기 메서드를 사용하여 컴포넌트의 상태를 관리하고, 특정 시점에 작업을 수행할 수 있습니다.
