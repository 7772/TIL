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



