# React Native

- cache clear
    ```
    $ watchman watch-del-all && rm -rf $TMPDIR/react-* && rm -rf node_modules/ && npm cache verify && npm install && npm start -- --reset-cache
    ```
- 성능을 고려한 정적&동적 이미지 사용
    
    *[참고](https://www.slideshare.net/deview/121react-native?from_m_app=android)
    
    1. 정적 이미지 - slide 52
        * iOS / Android 가 원래 이미지를 불러오는 방식을 이용하면 빨라질 수 있음.
    2. 동적 이미지 - slide 54
        * react-native-fast-Image 라이브러리 사용    




