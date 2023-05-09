### GET

주로 데이터를 읽거나 검색할 때 사용하는 메소드이다. GET 요청이 성공적으로 이루어진다면 XML이나 JSON과 함께 200(ok) HTTP Status Code를 반환한다. 
만약, 에러가 발생하면 주로 404(Not found) 에러나 400(Bad Request) 에러가 발생한다.

HTTP 명세에 의하면 GET 요청은 오로지 데이터를 읽을 때만 사용되고 수정할 때는 사용하지 않는다. 따라서 이런 이유로 사용하면 안전하다고 간주된다. 즉, 데이터 변형의 위험 없이 사용할 수 있다는 뜻이다. 게다가 GET 요청은 **멱등성**을 가지고 있다. 즉, 같은 요청을 여러번 하더라도 변함없이 항상 같은 응답을 받을 수 있다.

그러므로 GET을 데이터를 변경하는 등의 안전하지 않은 연산에 사용하면 안된다.

### POST

주로 새로운 리소스를 생성(Create)할 때 사용된다. 구체적으로 POST는 하위 리소스들(부모 리소스의 하위 리소스)을 생성하는데 사용된다. 성공적으로 Creation을 완료하면 201(Created) HTTP Status Code를 반환한다. 

POST 요청은 안전하지도 않고 멱등성이 있지도 않다. 다시 말해서 같은 POST 요청을 반복해서 했을 때 항상 같은 결과물이 나오는 것을 보장하지 않는다는 것이다. 그러므로 두 개의 같은 POST 요청을 보내면 같은 정보를 담은 두 개의 다른 resource를 반환할 가능성이 높다.

### GET vs POST

- GET : 모든 필요한 데이터를 URL에 포함하여 요청한다.
- POST : 추가적인 데이터를 body에 포함할 수 있다.

|제목| GET | POST |
|------|---|---|
|History|파라미터들은 URL의 일부분이기 때문에 브라우저 히스토리에 남는다.|파라미터들이 브라우저 히스토리에 저장되지 않는다.|
|Bookmarked|요청 파라미터들이 URL로 인코딩되므로 즐겨찾기가 가능하다.|요청 파라미터들이 request body에 포함되고 request URL에 나타나지 않으므로 즐겨찾기가 불가능하다.|
|button/re-sumit behavior|GET 요청이 다시 실행되더라도 브라우저 캐시에 HTML이 저장되어 있다면 서버에 다시 submit되지 않는다.|브라우저가 보통 사용자에게 데이터가 다시 submit 되어야 한다고 alert을 준다.|
|Encoding type|application/x-www-form-urlencoded|multipart/form-data or application/x-www-form-urlencoded Use multipart encoding for binary data|
|Parameters|전송 가능하지만 URL에 넣을 수 있는 파라미터 데이터가 제한된다. 2K 이하로 사용하는 것이 안전하며 몇몇 서버들은 64K까지 다룬다.|서버에 파일 업로드하는 것을 포함하여 파라미터를 전송할 수 있다.|
|Hacked|script kiddies에 의해 해킹되기 쉽다.|GET에 비해 해킹이 좀 더 어렵다.|
|Restrictions on form data type|오직 ASCII characters만 허용된다.|제한이 없으며, binary data도 허용된다.|
|Security|GET은 POST에 비해 보안에 약하다. 그 이유는 데이터가 URL의 일부로 전송되고 그 때문에 브라우저 히스토리에 저장되며 서버가 plain text로 로그를 남기기 때문이다.|POST는 GET에 비해 보안이 조금 더 안전하다. 그 이유는 파라미터들이 브라우저 히스토리나 서버 로그에 저장되지 않기 때문이다.|
|Restrictions on form data length|form data가 URL에 포함되고 URL 길이가 제한되기 때문에 form data의 길이도 제한된다. 안전한 URL 길이는 2047 characters이나 브라우저나 웹 서버에 따라 달라진다.|제한이 없다.|
|Usability|GET 메소드는 비밀번호와 같은 민감한 정보들을 전송하는데 사용해서는 안된다.|POST 메소드는 비밀번호와 같은 민감한 정보를 전송하는데 사용된다.|
|Visibility|GET 메소드는 모두에게 보여진다. (브라우저 주소창에 그대로 보여지고 그에 따라 전송가능한 정보의 양도 제한된다.)|POST 메소드는 URL에 보여지지 않는다.|
|Cached|GET 은 idempotent하기 때문에 캐시가 된다.(멱등성 : 같은 요청을 여러 번 보내도 항상 같은 응답이 나온다.)|POST는 idempotent하지 않기 때문에 캐시가 되지 않는다. (같은 요청을 여러 번 보내도 다른 응답이 올 수 있다.)|

### Ref
- https://im-developer.tistory.com/166
