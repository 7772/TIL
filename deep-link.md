# Deep Link

Deep Link 는 특정 url 을 이용해 사용자를 원하는 특정 도메인으로 이동시키는 기술을 말함.

그러한 기술들 중에서 최근에 Web URL 을 그대로 이용하는 방식이 적용된 것이 다음과 같음.

Android : Android App Links

iOS     : Universial Links

## 기존 URL Schema 의 기술과의 차이점

기존의 URL Schema 는 `exampleApp://go/to/screen` 과 같은 방식으로 원하는 스크린으로 이동시켰음.

그러나, 앱의 host 로 사용된 `exampleApp` 이 사용자의 스마트폰에서 Unique 한지 보장할 수 있는 방법이 없음.

만약 사용자의 스마트폰에서 `exampleApp` 이라는 host name 을 가진 앱이 2개 존재한다면, 사용자가 링크를 클릭했을때, 랜덤하게 (혹은 버그를 유발하며) 두개 중 아무 앱이나 켜지게 되는 한계점이 있음.
Android App Links 와 Universial Links 는 사용자에게 전달되는 URL 의 소유권이 나에게 있음을 증명하는 과정을 통해, 기존 URL Schema 의 한계점을 보완하였음.

## Android

1. 앱의 manifest file 에 App Links 의 URL을 등록한다.
2. 앱과 웹사이트에 소유권(assetLinks)을 등록한다.
  - Web - [link](https://developer.android.com/training/app-links/verify-site-associations#publish-json)
  - App - [link](https://developer.android.com/training/app-links/verify-site-associations#request-verify)
  - `assetLinks.json`
    ```
    [{
      "relation": ["delegate_permission/common.handle_all_urls"],
      "target": {
        "namespace": "android_app",
        "package_name": "com.example.app",
        "sha256_cert_fingerprints":["DB:...............................:E1"]
      }
    }]
    ```

## iOS

1. 앱의 delegate file 에 Universial Links 의 URL을 등록한다.
2. 앱과 웹사이트에 소유권(Apple App Site Association file)을 등록한다.
3. `apple-app-site-association`

```
{
    "applinks": {
        "apps": [],
        "details": [
          {
            "appID": "{Prefix}.com.example.app",
            "paths": ["/invitations/run", "NOT /invitations/intro"]
          }
        ]
    }
}
```

## Web

1. `.well-known/assetLinks.json`, `.well-known/apple-app-site-association` 등록