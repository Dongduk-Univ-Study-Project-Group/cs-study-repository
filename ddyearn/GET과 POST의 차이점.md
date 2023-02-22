## GET과 POST의 차이점

### GET
GET 메서드란 브라우저에서 웹 서버로 값을 전달할 때 URL 뒤에 값을 더하여 보내는 방식이다.
URL 뒤에 오는 정보를 '쿼리 스트링(query string)' 또는 '쿼리 문자열'이라고 한다.
+ URL 끝에 '?'가 붙어 쿼리 스트링의 시작을 나타낸다. (예: domain.com/?)
+ 형식은 '이름=값' 이다. (예: domain.com/?name=value)
+ 여러 값을 전달하려면 '&'로 연결한다. (예: domain.com/?name=value&tel=010)

### POST
POST 메서드란 브라우저로부터 웹 서버에 값을 보낼 때 '요청 본문(request body)'라는 URL에는 보이지 않는 장소에 값을 넣어서 보내는 방법이다.
많은 양의 값을 보내는 데 적합하다.  
POST 메서드로 요청을 보내려면 HTML의 \<form>태그 속성에서 method=POST를 지정해야 한다.

### 차이점
GET 메서드와 POST 메서드의 차이는 '브라우저의 즐겨찾기에 등록할 수 있는가?' 라는 예로 자주 설명된다.
GET 메서드에서는 URL에 연결해 데이터를 송신하기 때문에 '즐겨찾기'에 등록하는 URL 자체에 쿼리 스트링으로 검색 데이터를 포함할 수 있지만,
POST 메서드에서는 검색 데이터를 요청 본문에 저장하기 때문에 '즐겨찾기'에 등록할 수 없다.  
브라우저의 주소 표시줄에 URL을 직접 입력하는 것과 브라우저의 즐겨찾기에서 URL에 액세스하는 것은 GET 메서드로 요청을 보낸다.

#### 참고
https://github.com/Dongduk-Univ-Study-Project-Group/spring-study-repository/blob/ddyearn/ddyearn/2%EC%A3%BC%EC%B0%A8/README.md

