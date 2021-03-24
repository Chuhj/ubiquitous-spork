## CORS 정책
*Cross-origin Resources sharing*  
한 출처에서 실행 중인 웹 애플리케이션이 다른 출처의 선택한 자원에 접근할 수 있는 권한을 부여하도록 브라우저에 알려주는 체제
최신 브라우저는 XMLHttpRequest 또는 Fetch와 같은 API에서 CORS를 사용하여 교차 출처 HTTP 요청의 위험을 완화  
프론트에서 백으로 요청을 할때 origin이 설정되고 응답으로는 Access-Control-Allow-Origin: <origin> | * 를 설정해줘야함  
요청헤더에 cookie가 있을때는 응답에서 Access-Control-Allow-Origin 을 *로 설정하면 안됨
## Server Side Rendering
  서버에서 필요한 데이터들을 불러와 html을 만들어 클라이언트에게 보냄  
  첫 페이지 로딩이 빠름  
  SEO 효율적  
  blinking issue  
  서버에 과부하가 걸리기 쉬움  
  동적으로 데이터를 처리하는 자바스크립트 파일을 들고와야 interact할 수 있음 interact와 보는것의 공백기가 존재
  
