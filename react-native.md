# React Native

- cache clear
    ```
    $ watchman watch-del-all && rm -rf $TMPDIR/react-* && rm -rf node_modules/ && npm cache verify && npm install && npm start -- --reset-cache
    ```
- 성능을 고려한 정적&동적 이미지 사용
    
    * [참고](https://www.slideshare.net/deview/121react-native?from_m_app=android)
    
    1. 정적 이미지 - slide 52
        * iOS / Android 가 원래 이미지를 불러오는 방식을 이용하면 빨라질 수 있음.
    2. 동적 이미지 - slide 54
        * react-native-fast-Image 라이브러리 사용    

- shouldComponentUpdate 의 올바른 이해
    
    react-native 프로젝트를 진행하다보면 특정 state 의 변화가 일어날때엔, Component 를 re-render 하고 싶지 않을 때가 있을것이다.
    이럴때 shouldComponentUpdate 메서드를 사용하면 된다.

    ```
    shouldComponentUpdate(nextProps, nextState) {

        //  someProp 이 변경되었을때만 Component 를 Update 한다.
        if (this.props.someProp !== nextProps.someProp) {
            return true;    
        }

        return false;
    }
    ```
    
    shouldComponentUpdate 는 의도치 않는 re-render 를 막음으로써 성능을 훨씬 좋게 유지할 수 있으며,
    진정한 의미로 Component 를 관리하는 느낌을 받을 수 있다.

- HOC (Higher Order Component)

    1. HOC (Higher Order Component)는 컴포넌트 로직을 재사용 하기 위해 리액트에서 사용되는 진보된 기술이다. HOC 는 리액트 API 의 부분이 아니다. 리액트의 Compositional 속성으로 부터 야기된 하나의 패턴이다. (Composition 과 Inheritance 를 명확히 구분지어 공부할 것)

    2. HOC 는 컴포넌트를 Parameter 로 받고, 새로운 컴포넌트를 리턴해준다. 이 과정에서 원하는 동작을 사전에 처리할 수 있다.

    3. 언제, 왜 사용해야 할까? 개념은 이해해도, 왜 필요한지 이해하는 것은 또다른 문제인 것 같다.

    4. 리액트에서 컴포넌트는 코드 재사용의 기본 단위이다. 그러나, 가끔은 재사용 하고자 하는 컴포넌트가 필요한 공간에서 완전히 딱 걸맞지 않은 경우가 발생할 수 있다.

    5. CommentList 라는 컴포넌트가 있다고 가정해보자. 이 컴포넌트는 comment list 를 렌더링 하기 위해 외부 데이터 소스를 구독하는 컴포넌트이다.

- Code Push 내용 [react-native-code-push](https://github.com/Microsoft/react-native-code-push)

    1. 일단 앱이 릴리즈되면, 자바스크립트 코트나 이미지 에셋파일들을 업데이트 하는 것은 당신이 리컴파일을 하도록 요구하고, 전체의 바이너리를 재배포 하도록 한다. 그리고 당연히 앱스토어/플레이스토어의 리뷰가 따른다.

    2. 코드 푸쉬 플러그인은 코드푸쉬 서버에 당신이 릴리즈한 업데이트로 동기화된 당신의 자바스크립트와 이미지들을 유지함으로써, 사용자가 즉각적으로 제품 향상을 얻도록 도와준다.

    3. 정상작동하는 버전의 코드를 코드푸쉬가 유지하고 있기때문에, 실수로 크래쉬가 발생하는 코드를 업데이트하더라도, 이전 버전으로 쉽게 롤백 할 수 있다.

    4. 네이티브 코드를 변경시키는 코드의 변화는 코드푸쉬를 통해 업데이트 될 수 없다. 그러므로 스토어를 통해야만 한다.

    5. [code-push 설치](https://docs.microsoft.com/en-us/appcenter/distribution/codepush/index)

    6. [프로젝트에 code-push 셋팅](https://docs.microsoft.com/en-us/appcenter/distribution/codepush/index)

    7. 코드푸쉬 플러그인 사용법
        코드푸쉬가 프로젝트에 다운&링크 되면, 이제 JS 코드라인에 다음만 명시해주면 된다.

        1. 언제 업데이트를 체크할 것 인가?
        2. 언제 업데이트가 이용가능하며, 어떻게 유저에게 노출시킬 것 인가?

        위의 내용을 지원하기 위해 "CodePush-ify" 를 사용하면 되고, 이를 사용하기 위해 2 가지 옵션이 있으나, higher-order-component 를 사용하는 것이 좋아보인다.

        ```
        import codePush from "react-native-code-push";

        class MyApp extends Component {
        }

        export default codePush(MyApp);
        ```

        기본적으로 코드푸쉬는 앱이 시작할때마다 업데이트를 체크한다. 만약 업데이트가 이용가능하면, 조용히 다운로드 될것이고, 다음 앱 실행 시 설치될것이다. (또는 사용자에게 노출시키거나 OS 에 따라 제어되게 할수도 있음)

        만약 앱이 업데이트 여부를 더 빨리 발견하도록 하고 싶으면, 옵션을 주면 된다.

        ```
        let codePushOptions = { checkFrequency: codePUsh.CheckFrequency.ON_...};

        ...

        export codePush(codePushOptions)(MyApp);
        ```

        자세한 것은 공식문서 확인할 것.

    8. 스토어 가이드라인 규약

        Android는 제한이 덜하나, iOS 는 까다롭다. 관련 내용을 잘 인지하고 있어야 할 것이다.

        [Store Guideline Compliance](https://docs.microsoft.com/en-us/appcenter/distribution/codepush/index)

    9. 업데이트 사항들을 릴리즈 하기

        가장 간단한 방법은 CodePush CLI 가 제공하는 `realease-react` 커맨드를 사용하는 것이다. 이것은 JS 파일들과 asset 파일들을 빌드시킬것이고, 코드푸쉬 서버에 업데이트 네용을 릴리즈 할 것이다.

        가장 기본적인 형태로, 앱의 이름과 업데이트를 진행할 플랫폼(iOS or Android) 를 파라미터로 가진다.

        ```
        $ code-push release-react <appName> <platform>
        ```

        다음과 같은 선택적인 업데이트 배포도 가능하다.

        ```
        # Release a mandatory update with a changelog
        code-push release-react MyApp-iOS ios -m --description "Modified the header color"

        # Release an update for an app that uses a non-standard entry file name, and also capture
        # the sourcemap file generated by react-native bundle
        code-push release-react MyApp-iOS ios --entryFile MyApp.js --sourcemapOutput ../maps/MyApp.map

        # Release a dev Android build to just 1/4 of your end users
        code-push release-react MyApp-Android android --rollout 25% --dev true

        # Release an update that targets users running any 1.1.* binary, as opposed to
        # limiting the update to exact version name in the build.gradle file
        code-push release-react MyApp-Android android --targetBinaryVersion "~1.1.0"
        ```

        코드푸쉬에 모든 업데이트 내역에 대한 JS bundle 과 assets 이 릴리즈되었을지라도, 사용자는 그들이 실제로 필요한 파일들만 다운받을 것 이다. 

    

