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

   <img width="200" alt="스크린샷 2021-12-21 오후 8 30 14" src="https://user-images.githubusercontent.com/71534899/146923061-6332f92f-c7d6-443f-ade5-5829fdccb618.png">
   <br>
   위의 사진과 같이 <em>Rosetta를 사용하여 열기<em>를 클릭한 후에 터미널을 열고 다음과 같은 커맨드를 입력해주어야 한다. **반드시 이 설정을 해주어야 한다.**

   ```
   sudo gem install cocoapods
   ```

#### React Native 프로젝트 생성 방법

1. [EXPO](https://expo.dev/)
   RN을 편하게 사용할 수 있도록 미리 여러 설정이 되어 있는 툴.<br>
   **단점**<br>
   EXPO에서 제공하는 API만 사용할 수 있으며 필요한 기능이 제공되지 않을 때 네이티브 모듈을 추가로 생성하는 것이 불가능.

2. React native CLI
   필요한 기능이 있을 경우 모듈을 직접 만들어 사용할 수 있다.<br>_이 프로젝트의 개발에 사용될 것_ <br>
   **단점**<br>
   EXPO에 비해 불편하고 RN을 처음 다루는 이용자에게 좀 더 여럽게 느껴짐.

   만들고자 하는 디렉토리 위치에 다음 커멘드를 작성

```
npx react-native init 프로젝트이름
<!-- 생각보다 로딩이 오래 걸릴 수 있다.-->
```

Rosetta 설정된 iterm에서 다음을 실행

```
npx react-native start
```

이는 Javascript bundler를 해석해줄 Metro라는 것을 열어주는 과정이다. 이는 반드시 리액티 네이티브 프로젝트 폴더 내에서 실행해주어야만 한다.

다른 터미널을 하나 열고 프로젝트 실행해줄 커맨드를 입력한다.

```
npx react-native run-ios
```

반드시 React Native 프로젝트 폴더 내에서 실행해주어야만 한다.

이 폴더 안에 IOS 라는 폴더가 있는데 이것을 빌드하여 IOS용 모바일 앱을 실행시키는 과정이다.

#### Navigation view

Navigation을 Stack 형태로 구현 => Stack Navigation

현재 화면 위에 다른 화면을 쌓으면서 화면을 이동하는 방식

새로운 화면을 스택 구조로 push하여 쌓이기 때문에
가장 위에 있는 화면을 pop하면 이전 화면으로 돌아갈 수 있음.

##### 개발 순서

1. 프로젝트 폴더 내의 App.js의 코드를 전부 삭제하고 다음 코드를 입력.

   ```
   import App from './src/App';

   export default App;
   ```

2. src 폴더를 새로 만들고 그 곳에 App.js 파일 생성.

3. Stack Navigation 구현을 위한 Dependency 추가

   ```
   npm install @react-navigation/native @react-navigation/native-stack
   ```

   ```
   npm install react-native-screens react-native-safe-area-context
   ```

4. Cocoapods를 최신으로 업데이트 해주기 위해 다음 코드 입력

   ```
   cd ios
   pod install
   cd ..
   ```

   React Native 개발을 할 때 이 부분을 생략해서 오류가 발생하는 경우가 다수 있다.

   반드시 Cocoapods를 dependency가 추가되고 나서 업데이트 하는 습관을 기르는 것이 중요하다.

   IOS 개발에 사용되는 라이브러리를 관리해주는 도구이기 때문에 이를 최신화 해주지 않으면 해당 Dependency를
   인지할 수 없다는 _error_ 가 뜨는 것을확인할 수 있다.

5. Navigation 구현에 필요한 Component들을 import하고 코드 작성

   ```js
   import * as React from "react";
   import { NavigationContainer } from "@react-navigation/native";
   import { createNativeStackNavigator } from "@react-navigation/native-stack";
   import { Button, Text } from "react-native";

   const Stack = createNativeStackNavigator();

   const HomeScreen = ({ navigation }) => {
     return (
       <Button
         title="Go to kichang's profile"
         onPress={() => navigation.navigate("Profile", { name: "kichang" })}
       />
     );
   };
   const ProfileScreen = ({ navigation, route }) => {
     return <Text>This is {route.params.name}'s profile</Text>;
   };

   const App = () => {
     return (
       <NavigationContainer>
         <Stack.Navigator>
           <Stack.Screen
             name="Home"
             component={HomeScreen}
             options={{ title: "Welcome" }}
           />
           <Stack.Screen name="Profile" component={ProfileScreen} />
         </Stack.Navigator>
       </NavigationContainer>
     );
   };
   export default App;
   ```

   - NavigationContainer안에 Stack.Navigator로 Stack Navigation에 대한 컨테이너를 만듬.
     Stack.screen의 순서대로 screen에 대한 Stack이 쌓이는 것이다.

   - name Props를 반드시 해당 컴포넌트에 대한 navaigate처리 시의 name과 동일하게 mapping해주어야만한다.
   - Stack.screen의 component Props를 통해서 해당 Stack이 나타내는 screen을 정의할 수 있다.

   - HomeScreen에서 버튼에 핸들러를 작성한다.

     이는 "Profile"이라는 이름을 가진 screen으로 이동할 것임을 뜻하고 Route라는 Props의 name이라는 내부 Props로 *kichang*이라는 데이터를 넘겨주는 의미이다.

     Profile screen에서는 이를 route.params.name을 통해 전달받은 data를 화면에 출력할 수 있게 된다.

---

### React Native에 대한 모든 정보는 공식홈페이지가 기반이 된다. 하지만 셋업을 진행하는 과정에서 공식 홈페이지가 구체적으로 다루지 않는 부분이 존재하고 Navigation에 대해서도 원리적인 것에는 다소 설명이 부족하다. 이 git project를 통해 독자가 보다 쉽고 빠르게 이해하며 React native에 한 발 다가갈 수 있으면 좋겠다.
