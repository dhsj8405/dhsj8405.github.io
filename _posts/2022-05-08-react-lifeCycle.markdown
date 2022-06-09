---

layout: post
title: '리액트 생명주기(LifeCycle)'
subtitle: '리액트 생명주기(LifeCycle)'
categories: devlog
tags: react
comments: true

---
# 리액트
- 컴포넌트 기반의 View를 중심으로 한  자바스크립트 라이브러리

# 리액트 라이프 사이클
- 모든 컴포넌트들은 수명 주기가 존재한다.   
=> 라이프사이클은 컴포넌트의 수명주기

![image](https://user-images.githubusercontent.com/60701130/170182331-530c8143-5986-4009-893b-a8f8f7cb4843.png)


## Mount(생성)  
DOM이 생성되고 웹 브라우저상에 나타나는 것
- 메소드(실행순)
    1. constructor()  
        - 컴포넌트의 생성자 메서드  
            : 컴포넌트가 만들어지면 가장 먼저 실행
        - 용도  
            : 초기 state를 정할 때  
        - super(props)를 가장 먼저 호출해야함  
            - 부모의 constructor 메소드 초기화
            - 상속받은 메소드를 사용할 수 있게함
        - 예시
            ```
            class Header extends React.Component {
                constructor(props) {
                    super(props)
                    this.state = { favoritecolor: 'red' }
                }
                render() {
                    return <h1>My Favorite Color is {this.state.favoritecolor}</h1>
                }
            }
            ```
        - hook에서 대체
            ```
            const[state, setState] =  useState();
            ```
    2. getDerivedStateFromProps()  
    = props로부터 유래된 상태값을 얻다  
    => props가 변경되면 상태가 props 값과 동기화된다.
        - DOM에서 요소들이 랜더링 되기 직전에 호출
        - 용도  
        : props 변경시 state 값을 props값과 동기화  
        - mount,update 에서 사용가능한 메소드
        - 예시
            ```
            class Header extends React.Component {
                constructor(props) {
                    super(props)
                    this.state = { favoritecolor: 'red' }
                }
                static getDerivedStateFromProps(props, state) {
                    return { favoritecolor: props.favcol }
                }
                render() {
                    return <h1>My Favorite Color is {this.state.favoritecolor}</h1>
                }
            }
            ```
        - hook에서 대체
            ```
            function ScrollView({row}) {
            const [isScrollingDown, setIsScrollingDown] = useState(false);
            const [prevRow, setPrevRow] = useState(null);

            if (row !== prevRow) {
                // 마지막 렌더링 이후 행이 변경되었습니다. isScrollingDown을 업데이트합니다.
                setIsScrollingDown(prevRow !== null && row > prevRow);
                setPrevRow(row);
            }

            return `Scrolling down: ${isScrollingDown}`;
            }
            ```
    3. render()  
        - 필수 값
        - DOM에 HTML을 표현해준다.
        - 예시
            ```
            class Header extends React.Component {
                render() {
                    return <h1>This is the content of the Header component</h1>
                }
            }
            ```
    4. componentDidMount()  
    = 컴포넌트는 (이미)마운트를 했다.  
    => 컴포넌트가 랜더링된 직후에 호출
        - 용도  
            : DOM에 이미 위치한 상태 값 변경할 때
        - 예시
            ```
            class Header extends React.Component {
                constructor(props) {
                    super(props)
                    this.state = { favoritecolor: 'red' }
                }
                componentDidMount() {
                    setTimeout(() => {
                    this.setState({ favoritecolor: 'yellow' })
                    }, 1000)
                }
                render() {
                    return <h1>My Favorite Color is {this.state.favoritecolor}</h1>
                }
            }
            ```
        - hook에서 대체
            - 상태 값이 변경될 때 마다 실행
                ```
                const[state, setState] =  useState();
                useEffect(() => {
                    //state 변경시 실행
                }, [state]) 
                ```
            - 한번만 실행(두번째 인자에 빈배열 넣기)
                ```
                const Example = () => {
                    useEffect(() => {
                        ...
                    }, []);
                }  
                ```  

## Update(업데이트)  
= 컴포넌트의 업데이트  
=> 상태나 props가 변경될 때 마다 업데이트 된다.
- 메소드(실행순)
    1. getDerivedStateFromProps()
        = 컴포넌트 업데이트 시 제일 먼저 호출
        - 초기 props에 기반한 state가 저장  
            => 어떤 이벤트로 상태값을 변경해주어도 getDerivedStateFromProps()가 가장 먼저 호출되어 변경된 상태가 아닌 이전 상태값으로 남는다.  
        - 예시  
            ```
            class Header extends React.Component {
                constructor(props) {
                    super(props)
                    this.state = { favoritecolor: 'red' }
                }
                static getDerivedStateFromProps(props, state) {
                    return { favoritecolor: props.favcol }
                }
                changeColor = () => {
                    this.setState({ favoritecolor: 'blue' })
                }
                render() {
                    return (
                    <div>
                        <h1>My Favorite Color is {this.state.favoritecolor}</h1>
                        <button type="button" onClick={this.changeColor}>
                        Change color
                        </button>
                    </div>
                    )
                }
            }
            ```  
        => onClick 이벤트로 blue로 변경해주어도 getDerivedStateFromProps()가 가장 먼저 호출되기때문에 DOM에 출력되는 색깔은 yellow
    2. shouldComponentUpdate()  
        = React가 랜더링을 계속해야하는지 마는지에 대한 Boolean 값을 반환 ( 기본값은 true)  
        - 용도  
            : 컴포넌트 최적화
        - 예시
            ```
            shouldComponentUpdate(prevProps, prevState) {
                return this.props.data !== prevProps.data;
            }
            ```
        - hook에서 대체  
            ```
            const Example = React.memo(() => {
                ...
            }, (prevProps, nextProps) => {
                return nextProps.value === prevProps.value;
            })
            ```
    3. render()  
    4. getSnapshotBeforeUpdate()  
        업데이트 되기 전의 props와 state에 접근 할 수 있다.(업데이트 이후에도 확인가능)
        - `주의점`  
            : 사전에 업데이트 돼야하는 전제조건이 있기 때문에 componentDidUpdate() 메소드도 작성해야한다.  
        - 예시
            ```
            class Header extends React.Component {
                constructor(props) {
                    super(props)
                    this.state = { favoritecolor: 'red' }
                }
                componentDidMount() {
                    setTimeout(() => {
                    this.setState({ favoritecolor: 'yellow' })
                    }, 1000)
                }
                getSnapshotBeforeUpdate(prevProps, prevState) {
                    document.getElementById('div1').innerHTML =
                    'Before the update, the favorite was ' + prevState.favoritecolor
                }
                componentDidUpdate() {
                    document.getElementById('div2').innerHTML =
                    'The updated favorite is ' + this.state.favoritecolor
                }
                render() {
                    return (
                    <div>
                        <h1>My Favorite Color is {this.state.favoritecolor}</h1>
                        <div id="div1"></div>
                        <div id="div2"></div>
                    </div>
                    )
                }
            }
            ```        
        초깃값이 ‘red로 랜더링 되면, componentDidMount() 메소드에 의해 1초 후 값이 ‘yellow’로 업데이트 되고, 그 다음에 getSnapshotBeforeUpdate()메소드가 실행되며 div1에 해당 텍스트가 출력된다.
        업데이트 이전 내역을 표시해 주었으므로 업데이트 이후도 실행되야 하기 때문에 componentDidUpdate() 가 포함되야 한다.
    5. componentDidUpdate()  
        컴포넌트가 DOM에서 update된 후에 호출
        - 예시
            ```
            class Header extends React.Component {
                constructor(props) {
                    super(props)
                    this.state = { favoritecolor: 'red' }
                }
                componentDidMount() {
                    setTimeout(() => {
                    this.setState({ favoritecolor: 'yellow' })
                    }, 1000)
                }
                componentDidUpdate() {
                    document.getElementById('mydiv').innerHTML =
                    'The updated favorite is ' + this.state.favoritecolor
                }
                render() {
                    return (
                    <div>
                        <h1>My Favorite Color is {this.state.favoritecolor}</h1>
                        <div id="mydiv"></div>
                    </div>
                    )
                }
            }
            ```
        red에서 yellow로 값이 업데이트 되고 그 내용이 mydiv 돔에 출력된다.
        - hook에서 대체
            ```
            const Example = () => {
                useEffect(() => {
                    ...
                });
            }
            ```  

## Unmount(제거)  
 = 컴포넌트가 DOM을 제거하거나 unmounting 할 때를 의미
 - 메소드
    1. componentWillUnmount  
    = 컴포넌트가 DOM에서 제거될 때 호출되는 메소드
        - 예시  
            ```
            class Example extends React.Component {
                componentWillUnmount() {
                    ...
                }
            }
            ```
        - hook에서 대체
            ```
            const Example = () => {
                useEffect(() => {
                    return () => {
                        ...
                    };
                }, []);
            }
            ```
