# YeenNote

### 예인이가 한다. 정리를 공부한 것들을


************
## 2020-09-17
webRTC: web Real Time Communication 을 공부하기 시작했다.

**배울것**
1. 웹캠에서 비디오 가져 오기
2. RTCPeerConnection으로 비디오 스트리밍
3. RTCDataChannel을 사용하여 데이터 스트리밍
4. 메시지 교환을위한 신호 서비스 설정
5. 피어 연결 및 신호 결합
6. 사진을 찍고 데이터 채널을 통해 공유


구글 앱에서 Web Server For Chorm을 설치하면 크롬으로 로컬 서버를 만들 수 있다
getUserMedia()를 호출하면 브라우저는 사용자에게 카메라에 액세스 할수 있는 권한을 요청한다. 성공하면 MediaStream이 반환되면서 srcObject속성을 통해 미디어 요소를 사용할 수 있다. 

      const hdConstraints = {
      video: {
        width: {
          min: 1280
        },
        height: {
          min: 720
        }
      }
    }

이런 식으로 비디오의 추가 요구사항에 대한 제약 조건을 사용할 수 있다.

Link: [참조사이트][webRTClink]

[webRTClink]: https://codelabs.developers.google.com/codelabs/webrtc-web/#0 "Go google"
