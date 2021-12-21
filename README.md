# React-Native Set-Up과 Navigation 구현 보고서

### 201720808<br>소프트웨어학과<br>김기창

### MAC OS - IOS

---

1. React Native의 Set-UP
2. React Native Navigation에 대한 이해

---

### React Native의 Set-UP

#### React Native란? <br>

React native는 RN이라고도 불린다. 이는 JAVASCRIPT 라이브러리 중 하나인 React를 이용해서 크로스 플랫폼 앱을 만들 수 있는
오픈 소스 모바일 애플리케이션 프레임워크

#### React Native의 동작 원리 <br>

React native가 가상 DOM을 통해 DOM을 직접적으로 조작하지 않는다는 부분에서 REACT와 동일하다.
React의 선언형 UI 패러다임과 JavaScript를 통해 기존의 네이티브 코드 ( IOS의 Object-c 혹은 swift, Android의 Kotlin 혹은 JAVA) 를 감싸고 네이티브 API와 통신하여 모바일 앱을 개발할 수 있도록 한다.

#### React Native Set-Up에 필요한 요소

1. [HomeBrew](https://brew.sh/index_ko)
   Mac을 사용하는 유저라면 반드시 필요한 패키지 매니저
   맥에서 대부분의 패키지들은 이 홈브류를 이용해서 설치한다.
2. [watchman](https://facebook.github.io/watchman/docs/install.html)
   페이스북에서 제작한 파일 시스템 변경 감지 도구.
   RN에서 왓치맨은 소스코드의 변화를 감지하고 자동으로 빌드하여 화면에 업로드하는 역할을 담당.

   ```
   rew install watchman
   ```

3. [Node JS](https://nodejs.org/ko/)
   Chrome V8 JavaScript 엔진으로 빌드된 JavaScript 런타임
   노드 패키지 매니저인 npm 을 사용할 수 있게 됨.

   ```
   brew install node
   ```

4. Xcode
   os 를 개발하는데 반드시 필요한 개발 도구.
   IOS 시뮬레이터 및 IOS 앱을 빌드하는데 사용됨.
   - Xcode command Line Tool  
     버전 관리 도구, 소스코드 빌드 도구, 프로그래밍 언어 인터프리터 등에 사용되는 도구들.
     최신버전으로 설정
   - 시뮬레이터
     가상 기기에서 테스트를 진행하기 위한 IOS 시뮬레이터
     아이폰이 없어도 IOS 개발을 눈으로 확인할 수 있도록 도와줌.
5. CocoaPods
   Mac이나 IOS 개발에 사용되는 라이브러리를 관리해주는 도구
   이는 반드시 Ruby 환경에서 설치해주어야 한다.
   <img src="../src/rosetta.png"></img>

#### React Native 프로젝트 생성 방법

1. [EXPO](https://expo.dev/)
   RN을 편하게 사용할 수 있도록 미리 여러 설정이 되어 있는 툴.
   **단점**
   EXPO에서 제공하는 API만 사용할 수 있으며 필요한 기능이 제공되지 않을 때 네이티브 모듈을 추가로 생성하는 것이 불가능.

2. React native CLI
   필요한 기능이 있을 경우 모듈을 직접 만들어 사용할 수 있다.
   _이 프로젝트의 개발에 사용될 것_
   **단점**
   EXPO에 비해 불편하고 RN을 처음 다루는 이용자에게 좀 더 여럽게 느껴짐.
