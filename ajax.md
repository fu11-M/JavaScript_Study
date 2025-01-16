## AJAX(Asynchronous JavaScript and XML)는 
웹 페이지가 전체 페이지를 새로 고침하지 않고도 서버와 데이터를 비동기적으로 주고받을 수 있게 해주는 기술이다.

### AJAX의 주요 특징
비동기성: AJAX는 비동기적으로 서버와 통신합니다. 즉, 웹 페이지가 서버로 요청을 보내고 서버로부터 응답을 받는 동안 페이지의 다른 부분을 계속해서 사용할 수 있다.

### AJAX의 작동 방식
- 사용자 요청: 사용자가 버튼 클릭, 양식 제출, 스크롤 등으로 트리거를    발생시키면 JavaScript가 서버로 요청을 보냅니다.

- 서버 요청: JavaScript는 XMLHttpRequest 객체 또는 fetch API를 사용해 서버로 데이터를 요청합니다.

- 서버 처리: 서버는 요청을 처리하고 필요한 데이터를 반환합니다.
- 응답 처리: 클라이언트는 서버의 응답을 받아 적절한 방식으로 화면을
업데이트합니다.

### AJAX의 예시
```javascript

fetch('https://api.example.com/data')
  .then(response => response.json())
  .then(data => {
    console.log(data); // 데이터를 받아서 처리
    document.getElementById('content').innerHTML = data.content; // HTML 업데이트
  })
  .catch(error => console.error('Error:', error));
```


### fetch 역할
HTTP 요청 보내기 : 
 - fetch는 서버에 GET, POST, PUT, DELETE 등의 HTTP 요청을 보낼 수 있다. 이 요청을 통해 데이터를 서버와 교환할 수 있다.

응답 받기 : 
- 서버가 응답을 보내면, fetch는 이를 처리하여 클라이언트가 필요한 데이터를 사용할 수 있게 한다. 응답은 주로 JSON, 텍스트, 이미지 등의 형태로 올 수 있다.

비동기 처리 : 
- fetch는 비동기 방식으로 동작하기 때문에, 요청을 보내고 서버의 응답을 기다리는 동안 웹 애플리케이션의 다른 작업을 차단하지 않는다.