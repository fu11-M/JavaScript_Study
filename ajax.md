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
AJAX는 동적인 웹 페이지를 구축하는 데 필수적인 기술로, 현대의 많은 웹 애플리케이션에서 사용됩니다. 예를 들어, 구글 지도, 페이스북, 트위터와 같은 웹 애플리케이션에서 AJAX를 활용하여 페이지 전체를 새로 고치지 않고도 데이터를 실시간으로 업데이트합니다.