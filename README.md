# YeenNote

### 예인이가 한다. 정리를 공부한 것들을


************
## 2020-09-17
webRTC: web Real Time Communication 을 공부하기 시작했다.   

> 배울것
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

**1. 웹캠에서 비디오 가져 오기 마침**

Link: [참조사이트][webRTClink]

[webRTClink]: https://codelabs.developers.google.com/codelabs/webrtc-web/#0 "Go google"   

## 2020-09-18
WebRT의 자바스크립트 API
*getUserMedia(): capture audio, video
*MediaRecorder: record audio, video
*RTCPeerConnection: user들 간에 audio, video 스트리밍
*RTCDataCh:user달 간에 data 스트리밍    

> STRN, TURN이란?
WebRTCsms peer-to-peer로 작동하게 디자인되어있기 떄문에 사용자들은 direct route로 연결이 가능하다. 하지만 WebRTC는 실제 networking에 대처할 수 있게 만들어져 있다.   
클라이언트 애플리케이션은 NAT 게이트웨이와 방화벽을 통과해야하며, P2P 네트워킹은 직접 연결이 실패 할 경우 폴 백이 필요하다. 이 프로세스의 일부로 WebRTC API는 STUN 서버를 사용하여 컴퓨터의 IP 주소를 가져오고 TURN 서버는 피어-투-피어 통신이 실패 할 경우 릴레이 서버로 작동한다.   
암호화는 WebRTC의 필수요소 이다.

**RTCPeerConnection**
예인과 준열이 RTCPeerConnection을 사용하여 영상채팅을 설정하려고 한다고 가정하면 예인과 준열은 네트워크 정보를 교환한다. 'finding candidates'표현은 ICE 프레임워크를 사용하여 서로의 인터페이스 및 포트를 찾는다.

1. 예인은 RTCPeerConnection 객체를 생성한다.
2. 예인은 getUserMedia()를 호출하고 여기에 전달 된 스트림을 추가한다.
3. 예인은 직렬화 된 cadidate data를 밥에게 보낸다. 
4. 준열은 예인에게 cadidate 메세지를 받으면, 준열은 addIceCandidate()를 호출한다. 그리고 cadidate를 원격 피어 설명에 추가한다.   

WebRTC 피어는 또한 해상도 및 코덱 기능과 같은 로컬 및 원격 오디오 및 비디오 미디어 정보를 찾고 교환해야한다.

1. 예인은 RTCPeerConnection createOffer()를 실행한다. 
2. 성공하면, 예인은 setLocalDescription()을 사용하여 로컬을 설정하고 세선 설명을 신호채널을 통해 준열에게 보낸다.
3. 준열은 setRemoteDescription()을 사용하여 Alice가 자신에게 보낸 정보를 원격 정로로 설정한다.
4. 준열은 RTCPeerConnection createAnswer()메서드를 실행하여 예인에게 받은 원격 설명을 전달하므로 예인과 호환되는 로컬세션을 생성 할 수 있다.
5. 그러면 예인은 준열의 세션 정보를 받고, 예인은 setRemoteDescription()을 사용하여 이를 원격 정보로 설정한다.
6. 성공!

**RTCPeerConnection으로 비디오 스트리밍**

Link: [참조사이트][webRTClink]

[webRTClink]: https://codelabs.developers.google.com/codelabs/webrtc-web/#4 "Go google"      

## 2020-09-21
**Spring Framework**

동작 방식
![Spring](\Spring.jsp)




