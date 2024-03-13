# LIVE-RARY
![](https://github.com/RiYaZe123/live-rary/assets/130757327/aa818ae1-258c-4b31-9935-43bb13d11538)
## 1. 프로그램 소개
- - -
 &nbsp; 이 프로젝트는 도서관 대출 관리 웹 서비스를 개발했다. 도서관에 가면 내가 찾는 책이 없거나 빌리려던 책이 이미 대출되어있는 경우가 종종 있다. 
 만약 인터넷에서 미리 검색해서 책이 있는지, 대출 가능한지 확인할 수 있다면 헛걸음하는 일이 없을 것이다. 
 따라서 인터넷에서 해당 도서관의 소장 도서 목록을 확인할 수 있고, 도서 대출이 가능한지 확인할 수 있는 프로그램을 만들었다. 
 또 내가 찾는 책이 누군가가 이미 대출을 해서 대출할 수 없다면 대출예약을 할 수 있고, 대출이 가능해졌을 때 알림을 표시해 주는 프로그램을 만들어 사용자가 어디서나 도서 대출 가능 여부를 편리하게 확인할 수 있다.

**<로그인 화면>**<br>
![login](https://github.com/RiYaZe123/live-rary/assets/130757327/0eaaa8ce-8d1b-4af9-ba9d-a3878793b723)
<br><br>**<유저로 로그인 시>**<br>
![User](https://github.com/RiYaZe123/live-rary/assets/130757327/128c9684-ce72-4a21-9d50-42dd320cf7de)
<br><br>**<사서로 로그인 시>**<br>
![librarian](https://github.com/RiYaZe123/live-rary/assets/130757327/aefac91c-f023-4c78-90c5-c00c66d245df)

**[기능]**
- 공통 : 로그인, 회원가입, 마이페이지(수정, 탈퇴), 도서 검색
- 사서 : 대출, 반납, 신규 도서 등록, 책 삭제
- 대출자 : 알람(연체, 대출 가능 목록), 대출(확인 및 연장), 예약(예약 및 취소)

**[개발 주요사항]**
- AJAX를 이용하여 새로 고침 없이 웹페이지 화면을 동적으로 변경
- 세션 방식으로 로그인 구현

## 2. 기술 스택
- - -
- **Language** : HTML, CSS, Java(JSP), Javascript
- **DB** : MYSQL
- **Engine** : Apache Tomcat Server
- **Tool** : Eclipse
<br><br>
![](https://github.com/RiYaZe123/live-rary/assets/130757327/d66f6f42-2378-499d-b9bc-6f49f8fc0f5d)

## 3. 팀원
- - -
홍상혁 (팀장-사서 기능 구현)

김규빈 (팀원-로그인 기능 구현 및 CSS 구성)

진민주 (팀원-유저 기능 구현)
<br><br>

## 4. 개발 기간
- - -
2022.11.26 ~ 2022.12.24 (개발)
<br><br>

## 5. 어려웠던 점과 배운 것
- - -
**5-1. AJAX**

단순하게 WEB 화면에서 페이지를 새로고침하지 않기 위해 사용

기본적으로 HTTP 프로토콜은 클라이언트쪽에서 Request를 보내고 서버쪽에서 Response를 받으면 이어졌던 연결이 끊기게 되어있다.

그래서 화면의 내용을 갱신하기 위해서는 다시 request를 하고 response를 하며 페이지 전체를 갱신하게 된다.

하지만 이렇게 할 경우, 엄청난 자원낭비와 시간낭비를 초래하고 말 것이다.

AJAX는 HTML 페이지 전체가 아닌 일부분만 갱신할 수 있도록 XMLHttpRequest객체를 통해 서버에 request한다.

이 경우, JSON이나 XML형태로 필요한 데이터만 받아 갱신하기 때문에 그만큼의 자원과 시간을 아낄 수 있다.

장점으로는 다음과 같다.
- 웹페이지 속도 향상
- 서버의 처리가 완료할 때까지 기다리지 않고 처리가 가능하다.
- 서버에 데이터만 전송하면 되므로 전체적인 코딩의 양이 줄어든다.
<br>

AJAX가 적용된 예시로 'librarianMain.jsp'를 가져와봤다.

<br>**단계 1 : 서버에 요청할 객체 만들기: 요청 객체** <br>
➢ XMLHttpRequest 객체 사용

```
function createRequest() {
	try {
		value = new XMLHttpRequest();
	} catch(failed) {
		value = null;
	}
	
	if(value == null) 
		alert("리퀘스트 오브젝트 생성 중 에러");
}
```

<br>**단계 2 : 서버 연결 자바스크립트 작성** <br>
비동기 앱의 서버 요청

➢ 폼 전송이 아닌 자바스크립트 객체 XMLHttpRequest 이용

```
function searchCheckUser() {
	var userid = document.getElementById("searchuserID").value;
	var url = "searchkUser.jsp";
	createRequest();
	value.open('POST', url, true);
	value.onreadystatechange = updateUser;
	value.setRequestHeader("Content-Type", "application/x-www-form-urlencoded");
	value.send("userid=" + userid);
}
```

<br>**단계3 : 응답 시 업데이트할 자바스크립트 작성**
```
function updateUser() {
	if(value.readyState == 4 && value.status == 200) {
		var data = value.responseText;
		var searchResult = document.getElementById("userResult");
		searchResult.innerHTML = data;
		document.getElementById("userResult").style.visibility="visible";
	}
}
```

**AJAX 기능을 이용하여 웹 페이지를 리로드 할 필요 없이 일부 요소만 업데이트 할 수 있게 되었다.**

<br>

**5-2. 팀장으로서의 역할**

 &nbsp; 먼저 팀원들과 해야할 역할을 분담을 할 때 최대한 비슷하게 할려고 했다. 개발 진행도를 만들어 한 사람이 한 파트가 끝나면 다음에 무엇을 만들어야 하는지 바로 파악할 수 있게 미리 만들었고 팀원들이 헤매지 않게 하기 위해 최대한 노력했다.
 처음에는 톱니바퀴가 제대로 물릴 수 있을까하는 걱정이 앞서기도 했지만 팀원들이 내 의견을 잘 따라줘서 순탄히 진행되었다. 그리고 내가 개발해야할 부분을 진행하면서 동시에 다른 사람들의 코드 확인나 테스트 등등
 여러 가지를 동시에 해야했기 때문에 어지러운 상황이 있었는데 팀원들이 도와주면서 팀워크의 중요성을 느꼈다.

**<개발 당시 진행도 초기 버전>**
![진행도1](https://github.com/RiYaZe123/live-rary/assets/130757327/73561662-fadc-4c0d-ba8d-3db4a6278f0a)

**<개발 진행도 최종 버전>**
![진행도2](https://github.com/RiYaZe123/live-rary/assets/130757327/53325614-dee6-4f45-9f94-2ad79a133cea)
