## XHR
= XHR(XML HTTP Request)기술은 자바스크립트의 XMLHttpRequest 객체를 통해 구현할 수 있다.
= 흔히 AJAX(Asynchronous Javascript And XML)라고 부르기도 한다.
- 페이지의 새로고침 없이, 비동기적으로 외부 서버에 요청을 보내고 응답을 받아오기 위해 사용한다. 사용자 경험(UX, User Experience)에 긍정적인 영향을 주므로 많이 사용하는 편이다.
- 일반적으로 아래 구조와 같이 구현할 수 있다.

> ```javascript
> const xhr = new XMLHttpRequest();
> xhr.onreadystatechange = () => {
>   if (xhr.readyState !== XMLHttpRequest.DONE) {
>       return;
>   }
>   if (xhr.status < 200 || xhr.status >= 300) {
>       // 요청 실패 로직 구현
>    return;
>   }
>   // 요청 실패 로직 구현
> };
> xhr.open([요청 방식], [요청 주소]);
> xhr.send([요청 데이터]?);
> ```
- 여기서 요청 방식은 아래와 같은 값을 사용할 수 있다
  - GET: 웹 브라우저를 통해 주소를 적고 요청을 보낼 때 사용하는 방식이다. xhr.send 함수를 호출할 때 요청 데이터를 함께 보낼 수 없고 서버로 전송하는 데이터가 모두 주소에 포함된다. 주로 해당 요청으로 서버에서 SELECT가 발생하는 경우많이 사용한다. 
  - POST : 주로 해당 요청으로 서버에서 INSERT가 발생하는 경우 많이 사용한다.
  - PATCH : 주로 해당 요청으로 서버에서 UPDATE가 발생하는 경우 많이 사용한다. 어떠한 엔티티(Entity)의 필드 중 일부가 수정될 때 사용한다. 실질적으로 PATCH와 PUT은 그 용처를 심하게 가리지 않는다.
  - PUT : 주로 해당 요청으로 서버에서 UPDATE가 발생하는 경우 많이 사용한다. 어떠한 엔티티(Entity)의 필드 전체가 수정될 때 사용한다. 실질적으로 PATCH와 PUT은 그 용처를 심하게 가리지 않는다.
  - DELETE : 주로 해당 요청으로 서버에서 DELETE가 발생하는 경우 많이 사용한다.

# 정적 속성
- UNSENT : XHR 객체의 readyState 속성 값으로 0과 같고. XHR 객체가 객체화된 후 아무런 동적을 하지 않은 초기 상태이다.
- OPENED : XHR 객체의 readyState 속성 값으로 1과 같고, open 메서드가 호출된 후의 상태이다.
- HEADERS_RECEIVED : XHR 객체의 readyState 속성 값으로 2와 같고, send 메서드 호출 후 서버와의 연결을 수립하였으며 요청에 대한 응답 상태 및 헤더가 수신된 상태이다.
- LOADING : XHR 객체의 readyState 속성 값으로 3과 같고, 서버의 응답(Response Body)이 수신되기 시작한 상태이다.(완료된 것은 아님)
- DONE : XHR 객체의 readyState 속성 값으로 4와 같고, XHR 통신이 성공 여부와 관계 없이 종료되었음을 의미한다. (통신 성공 여부는 status 속성 값으로 판단해야 한다.)

# 객체 속성
- readyState : XHR 객체의 대기 상태인 숫자값이다.
- responseText : 서버가 응답으로 전송한 문자열 데이터이다.
- status : XHR 객체의 HTTP 상태 코드인 숫자값이다.
 - 200 : OK. 정상상태. (주로 200이상 300미만의 값을 정상으로 판단한다. 단, 특별한 이유가 없다면 200을 사용.)
 - 400 : Bad Request. 서버가 요청하고 있는 데이터를 클라이언트가 부락하였거나 그 데이터의 형태가 잘못되었음을 의미한다.
 - 404 : Not Found. 해당 경로에 대한 맵핑이나 리소스가 서버에 존재하지 않는다는 의미이다.
 - 405 : Method Not Allowed. 맵핑이나 리소스가 존재하지만 해당 요청 방식(Method)으로는 접근할 수 없다는 의미이다.
 - 500 : Internal Server Error. 요청을 처리하는 도중 서버 내부에서 오류가 발생하였다는 의미이다. (HTML, CSS, Javascript 오류가 아닌 Java-Spring 오류가 여기에 해당.)