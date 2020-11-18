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

#### 동작 방식
![Spring](https://user-images.githubusercontent.com/57241500/93783140-5750d380-fc66-11ea-91dc-4944c0b75db8.JPG)

#### web.xml 설정파일   
 WAS가 최초 구동될 때 WEB-INF 디렉토리에 존재하는 web.xml을 읽고, 그에 해당하는 웹 애플리케이션 설정을 구한다. 각종 설정을 위한 파일이다. (mybatis, servlet, ...)
#### servlet-context.xml
서블릿 관련 설정이다. 

             <!-- Resolves views selected for rendering by @Controllers to .jsp resources in the/WEB-INF/views directory -->
       <beans:bean class="org.springframework.web.servlet.view.InternalResourceViewResolver">
       <beans:property name="prefix" value="/WEB-INF/views/" />
       <beans:property name="suffix" value=".jsp" />
       </beans:bean>

       <context:component-scan base-package="com.company.devpad" />
 <beans:bean class> : Controller가 Model를 리턴하고 DispatcherServlet이 jsp 파일을 찾을 때 쓰이는 정보를 기술하는 태그. "home"이라는 문자열을 반환하면 /WEB-INF/views/ 경로에서 접미사가 .jsp인 해당 파일을 찾는다. /WEB-INF/views/home.jsp    
 <context:component-scan> : Java 파일의 @Controller로 등록된 bean 객체를 찾도록 해주는 태그
 
 #### Mybatis
 기존에 JDBC를 이용하여 프로그래밍을 하는 방식에 비해서 MyBatis는 개발자의 부담을 굉장히 많이 덜어주고, 생산성 향상에도 도움이 된다.
 
 
 ## 2020-09-23
 mybatis에서 #{} 와 ${}의 차이   
 #: PreparedStatemnet      
ex)SELECT ID FROM TEST WHERE ID=#{id}      
   SELECT ID FROM TEST WHERE ID=?   (오라클로 넘어온 쿼리)      
   SELECT ID FROM TEST WHERE ID='amdin'   (실제수행)     
   ?에 파라미터가 바인딩되어 수행된다. 파싱된 쿼리문은 재활용(캐싱)이 되기 떄문에 효율적    
$: Statement       
ex)SELECT ID FROM TEST WHERE NUM = ${num}      
   SELECT ID FROM TEST WHERE NUM = 77    
   작은따옴표가 붙지 않기때문에 테이블이름이나 컬럼 이름을 동적으로 결정할 때 사용할 수 있다.    
   단, 파라미터 값이 바뀔 때마다 항상 쿼리문 파싱을 진행해야해서 성능상 단점이 존재     
      
## 2020-09-25
webrtc API해보는데 어렵다..서버는 넘 어렵다... 접속도 어렵다..
ERR_SSL_VERSION_OR_CIPHER_MISMATCH오류는 인증서 버전에 대문 문제 또는 SSL통신 시 사용하는 암호화 방식이 맞지 않거나 둘 중 하나이다.    

## 2020-09-29
 파이널 프로젝트 로그인 구현
 #### @RequestBody와 @ModelAttribute
 GET방식은 URL에 데이터를 담아 전송하며 1차원 데이터 밖에 담지 못한다. 따라서 검색조건 수준의 데이터를 담는게 옳바르다. GET방식 프로토콜은 Request 패킷에 Body가 존재하지 않는다. 그리고 POST방식은 Request의 Body에 데이터를 담는데 이 경우, JSON, 다차원 데이터를 담을 수 있다. 
 결론은 GET방식일 떄는 @RequestBody를 명시하지 않아야하고, POST방식일 때는 반드시 명시해야한다.     
 
 @ModelAttribute는 Parameter에 쓸 경우 방아오자 하는 데이터의 이름을 지정하여 해당 데이터만 가져온다. 받아오는 데이터를 '지정한다'   
 #### ModelAndView 객체
      
      @RequeestMapping("/border")
      public ModelAndView board(){
            ModelAndView mv = new ModelAndView();
            mv.setViewName("board");      //뷰 이름
            mv.addObject("data", "11234");      //뷰로 보낼 데이터 값
            
            return mv;
        }
      
 addObject는 key와 value를 동시에 전송한다.
 그러면 jsp에서는 ${data}로 받아주면 된다.   
 
 ## 2020-09-30   
 
      session.setAttribute("login", res); 
      
이렇게 저장한 세션 값은 .jsp에서 

      <h2>${sessionScope.login.u_id }님 환영합니다.</h2>
      
이렇게 값을 가져오면 된다... 이렇게 간단한 것일 줄이야...
              
## 2020-10-05
파이널 프로젝트 회원가입 구현 중
#### @RequestParam   
단일 HTTP요청 파라미터를 메소드 파라미터에 넣어주는 애노테이션    
    
    
가져올 요청 파라미터의 이름을 @RequestParam 애노테이션의 기본값으로 지정해 주면 된다.   
요청 파라미터의 값은 메소드 파라미터의 타입에 따라 적절하게 변환된다.

      @RequestMapping(value="/check_id.do", method = RequestMethod.POST)
            public void check_id(@RequestParam("u_id")String u_id, HttpServletResponse response) throws Exception {
            
파라미터 값이 꼭 존재해야하 한다.
      
      $.ajax({
			url : "check_id.do",
			type : "post",
			data : {
				u_id : $("#id").val()
			},
파라미터가 존재하지 않으면 400에러 발생

## 2020-10-22
.getMapper...

## 2020-10-23
PrintWriter out = resoponse.getWriter(); 형식으로 응답으로 내보낼 출력 스트림을 얻어낸 후, 
out.println("<script>");이런 식으로 스트림에 텍스트를 기록하게 된다.


## 2020-11-04
Ajax를 사용하는데 결과값이 controller에서 넘어오지 않았다.
원인은 값은 안넘겨주니 넘어갈리가...


	PrintWriter out = response.getWriter();
		out.println(dao.check_id(u_id));
		
요래하니 넘어간다.

-@ResponsBody
뷰 페이지를 응답하지 않고 return 값을 그대로 반환한다는 것이다.

## 2020-11-06
String은 새로운 값을 할당 할 때마다 새로생성.
StringBuffer는 메모리에 append해주는 방식이다.thread-safe라는 말에서처럼 변경가능하지만 multiple thread환경에서 안전한 클래스라고 한다.
 StringBuilder는 변경가능한 문자열이지만 synchronization이 적용되지 않았다. 
 
 
## 2020-11-19
### Priority Queue
큐는 FIFO이다 우선순위큐는 인터페이스 구현체 중 하나로, 저장한 순서에 구애받지 않고 우선순위에따라 정렬되며 가장 높은 우선순위부터 꺼낼 수 있다.
저장공간을 배열을 사용하며 각 요소를 '힙'이라는 자료구조 형태로 저장한다. 그래서 시간 복잡도는 O(NLogN)이다.
 
