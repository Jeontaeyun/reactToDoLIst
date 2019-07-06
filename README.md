# 리액트 To-Do-List MVC 설계

## 01. 프로젝트 개요

### (01) 프로젝트 스택

- Language : HTML5, CSS3, Javascript
- Framework: React
- CSS in JS : SASS

### (02) 리액트 개발 환경 설정

- ``` npm install react react-dom ``` 리액트 환경을 설치하는 npm 명령어
- ``` npm install create-react-app ``` Create-React-App을 설치하는 npm 명령어

### (03) 프로젝트 설정

- ``` create-react-app $projectName``` 으로 프로젝트 생성

- ``` yarn eject ``` 를 통해서 리액트 프로젝트의 환경 설정 파일들을 프로젝트 루트 경로로 이동시킵니다.

- yarn eject로 만들어진 config 폴더의 환경 설정 파일들에 SASS-Loader 설정을 변경

- ``` yarn add sass-loader node-sass classnames ``` 로 프로젝트에 필요한 패키지 설치

- ``` yarn add open-color ``` open-color 라이브러리의 색상들을 참조하면서 컴포넌트를 디자인

#### 01) SASS-Loader 설정

- webpack.config.js 부분의 sassRegex 부분을 다음과 같이 바꿔준다.
```javascript
test: sassRegex

use: getStyleLoaders({ importLoaders: 2 }).concat({
      loader: require.resolve('sass-loader'),
      options: {
        includePaths: [paths.appSrc + '/styles']
      }
    })
```
- 위의 코드는 sass-loader을 사용할 때 공통된 Sass 파일의 경로를 미리 잡아주는 것이다.

- 또한, config/paths.js에서 경로를 다음과 같이 추가해주어야 한다.

```javascript
module.exports = {
    (...),
    styles: resolveApp('src/styles');
}
```

## 02. 프로젝트 학습

### (01) 프로젝트 진행 방식 | To Do List Project

01. 프로젝트 생성 및 환경 설정

    - create-react-app 을 통한 프로젝트 생성

    - yarn eject 를 통한 환경 설정

    - 필요한 패키지 설치

02. UI 디자인 및 구성 계획

    - 와이어 프레임을 통한 기본 구성 디자인

    - 컴포넌트 계획 수립

03. 상태 관리 계획

    - 상태 관리 라이브러리 선택

    - 각 컴포넌트의 상태 정의

04. Dev Tool을 통한 테스트 및 최적화

    - Dev Tool을 통한 기능 테스트

    - 컴포넌트 분리를 통한 성능 최적화


### (02) 컴포넌트 설계 방식

01. 디렉토리 만들기

02. 자바스크립트 파일 만들기

03. SASS 파일 만들기

04. index.js 파일 만들기

    - index.js 파일은 나중에 해당 컴포넌트를 호출할 때 ./components/PageTemplate/PageTemplate와 같이 중복되는 주소가 아닌 ./components/PageTemplate로 입력하기 위해 만든다.

### (03) 리액트 컴포넌트 상태 관리

- 개발 시 리액트의 컴포넌트는 기능별로 상태가 필요한 컴포넌트의 최상위 컴포넌트에서 상태 관리를 하는 것이 효율적입니다.

#### 01) 리액트 스마트 컴포넌트와 덤프 컴포넌트

01. Smart Component 

- 어플리케이션의 State를 관리하는 컴포넌트

- State가 있는 컴포넌트를 말하며 주로 Class Componenet가 그 역할을 하나 React Hooks를 사용할 경우 Functional Component로 Smart Component를 구현할 수 있다.

02. Dump Component

- State가 없는 컴포넌트로 주로 Functional Component를 사용한다. 

- 주로 상위 컴포넌트로부터 Props를 받아 화면에 보여주는 View로서의 기능만 한다.

#### 02) e.stopPropagation()

- 어떤 컴포넌트의 상위 컴포넌트에 onClick 이벤트가 설정되어 있고, 자식 요소에서도 onClick 이벤트가 설정되어 있으면 자식 -> 부모 순으로 메서드를 실행하게 되는데 이를 **propagation**이라고 합니다.

- 이럴 경우 자식 요소의 onClick 이벤트의 메소드가 실행되지 않을 수 있기에 **e.stopPropagation()** 메소드를 넣어주어야한다.

```javascript
<div ... onClick={(e) => { 
        onRemove();
        e.stopPropagation();
        }}></div>
 ```
 
## 03. 프로젝트 고찰

