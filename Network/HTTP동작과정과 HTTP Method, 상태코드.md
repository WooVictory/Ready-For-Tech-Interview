# HTTP란?
> HyperText Transfer Protocal의 약자로써 **인터넷 통신을 위해 사용되는 프로토콜**이다.

# HTTP 동작

Client가 브라우저를 통해 URI을 통해 특정 요청(Request)을 보내면, Server는 해당 요청(Request)을 받아 처리를 하여 Client에게 응답(Response)을 하는 형태

![hppt동작 과정](https://user-images.githubusercontent.com/37958836/119261737-ab57f180-bc13-11eb-85d4-cae4e392c5a3.png)

# HTTP 특징
- TCP/IP을 이용한 응용 프로토콜이다.
- 연결 상태를 유지하지 않는 비연결성 프로토콜이다.
- 요청과 응답 방식으로 동작한다.
- 서버와 클라이언트에 의해 HTTP 메세지가 해석된다.

# HTTP Method
| Method  | 설명                                                                                                    |
| ------- | ------------------------------------------------------------------------------------------------------- |
| GET     | URI가 가진 정보를 검색하기 위해 요청하는 메소드                                                         |
| HEAD    | GET메소드와 방식은 동일하지만, `응답에 BODY가 없고 응답 코드와 HEAD만 응답하는데 사용`되는 메소드       |
| POST    | 요청된 자원을 생성하기 위한 메소드                                                                      |
| PUT     | 요청된 자원을 수정할때 사용하고, `PATHCH와는 다르게 자원 전체를 갱신하는데 사용`되는 메소드             |
| PATCH   | PUT메소드와 유사하게 요청된 자원을 수정할때 사용되지만, `자원의 일부를 수정`하는 의미로 사용되는 메소드 |
| DELETE  | 요청된 자원을 삭제하기 위한 메소드                                                                      |
| CONNECT | 동적으로 터널 모드를 교환하고 프락시 기능을 요청할때 사용하는 메소드                                    |
| TRACE   | 원격 서버에 루프백 메세지를 호출하기 위해 테스트용도로 사용하는 메소드                                  |
| OPTIONS | 웹 서버에서 지원하는 메소드의 종류들을 확인할 경우 사용하는 메소드                                      |

# HTTP Status Code

### 정보전송 임시응답 (1xx)
- 서버가 요청을 클라이언트에서 성공적으로 수신을 했고 서버에서 처리중인 정보를 보낸디.

    | Status Code | 설명               |
    | ----------- | ------------------ |
    | 100         | Continue           |
    | 101         | Swiching protocols |

### 성공 (2xx)
- 서버가 요청을 `성공`적으로 받았음을 알려준다.

    | Status Code | 설명                          |
    | ----------- | ----------------------------- |
    | 200         | Ok!                           |
    | 201         | Created                       |
    | 202         | Accepted                      |
    | 203         | Non-authoritative Information |
    | 204         | No Cotent                     |

### 리다이렉션 (3xx)
- 캐싱된 파일을 새로고침 하여 확인하면 3xx대 코드을 받을 수 있다.

    | Status Code | 설명              |
    | ----------- | ----------------- |
    | 301         | Moved permanently |
    | 302         | Not temporarily   |
    | 303         | Not modified      |

### 클라이언트 요청 오류 (4xx)
- 클라이언에서 서버에 잘못된 요청을 보내 서버가 요청을 해결 할 수 없을때 발생하는 코드이며, `클라이언트측에서 발생하는 코드`이다.

    | Status Code | 설명                          |
    | ----------- | ----------------------------- |
    | 400         | Bad Request                   |
    | 401         | Unauthorized                  |
    | 402         | Payment required              |
    | 403         | Forbidden                     |
    | 404         | Not found                     |
    | 405         | Method not allowed            |
    | 407         | Proxy authentication required |
    | 408         | Request timeout               |
    | 410         | Gone                          |
    | 412         | Precondition failed           |
    | 414         | Request-URI too long          |

### 서버에러 (5xx)
- 클라이언트의 요청을 받고 서버에서 처리하지 못할때 발생하는 코드이며, `서버측에서 발생하는 코드`이다.

    | Status Code | 설명                       |
    | ----------- | -------------------------- |
    | 500         | Internal server error      |
    | 501         | Not implemented            |
    | 503         | Service unnailable         |
    | 504         | Gateway timeout            |
    | 505         | HTTP version not supported |