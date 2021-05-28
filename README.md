## [ 5월 25일 ]
# 9장 express 모듈
## 1. 요청과 응답
* 요청하는 대상 : 클라이언트(사용자)<br>
-> 요청 메세지 : 클라이언트가 서버로 보내는 편지
* 응답하는 대상 : 서버(제공자)<br>
-> 응답 메시지 : 서버가 클라이언트로 보내는 편지
## 2. express 모듈을 사용한 서버 생성과 실행
* express 모듈의 기본 메소드
>* express() : 서버 애플리케이션 객체를 생성합니다.
>* app.use() : 요청이 왔을 때 실행할 함수를 지정합니다.
>* app.listen() : 서버를 실행합니다.
## 3. 페이지 라우팅
* 페이지 라우팅 : 클라이언트 요청에 적절한 페이지를 제공하는 기술
* express 모듈의 페이지 라우팅 메소드
>* get(path. callback) : GET 요청이 발생했을 때 이벤트 리스너를 지정합니다.
>* post(path. callback) : POST 요청이 발생했을 때 이벤트 리스너를 지정합니다.
>* put(path. callback) : PUT 요청이 발생했을 때 이벤트 리스너를 지정합니다.
>* delete(path. callback) DELETE 요청이 발생했을 때 이벤트 리스너를 지정합니다.
>* all(path. callback) : 모든 요청이 발생했을 때 이벤트 리스너를 지정합니다.
* 페이지 라우팅을 할 때 토큰을 활용함
>* ':<토큰이름>' 형태로 설정
>* 토큰은 다른 문자열로 변환 입력가능, request 객체의 params 속성으로 전달됨
## 4. 요청과 응답
* response 객체
>* send() : 데이터 본물을 제공합니다.
>* status() : 상태 코드를 제공합니다.
>* set() : 헤더를 설정합니다.
* 데이터 제공
>* send()메소드 : 사용자에게 데이터 본문을 제공
>* send()메소드는 가장 마지막에 실행해야 하며, 두 번 실행할 수 없음
* Content-Type<br>
-> 서버가 Content-Type을 제공 : 웹 브라우저는 헤더를 확인, 제공된 데이터의 형태
를 확인(MIME라는 문자열로 제공)
* MINE 형식
>* text/plain : 기본적인 텍스트를 의미합니다.
>* text/html : html 데이터를 의미합니다.
>* image/png: png 데이터를 의미합니다.
>* audio/mpe : MP3 음악 파일을 의미합니다.
>* video/mpeg : MPEG 비디오 파일을 의미합니다.
>* application/json : json 데이터를 의미합니다.
>* multipart/form-data : 입력 양식 데이터를 의미합니다.
* Content-Type 지정 메소드
>* type() : Content-Type을 MIME 형식으로 지정합니다.
* HTTP 상태 코드 : 404 Not Found<br>
상태 코드 : 서버가 클라이언트에 '해당 경로는 이러한 상태'라고 알려 주는 용도
* HTTP 상태 코드의 예
>* 1XX : 처리중 ex) 100 Countinue
>* 2XX : 성공 ex) 200 OK
>* 3XX : 리다이렉트 ex) 300Multiple Choices
>* 4XX : 클라이언트 오류 ex) 400
>* 5XX : 서버 오류 ex) Internal Server Error
* status()메소드
>* status() : 상태 코드를 지정합니다.
* 리다이렉트 : 3XX, 특수한 상태 코드<br>
-> 웹 브라우저가 리다이렉트를 확이하면 화면을 출력하지 않고, 응답 헤더에 있는 Location 속성을 확인해서 해당 위치로 이동<br>
-> 특정 경로로 웹 브라우저를 인도 할 때 사용
>* redirect() : 리다이렉트합니다.
* request 객체
>* 요청 매개 변수 -> 네이버에서 '초콜릿'문자를 검색<br>
https://search.naver.com/search.naver?where=nexearch&query=초콜릿&sm=top_hty&fbm=0&ie=utf8
>* 프로토콜 : HTTPS -> 통신에 사용되는 규칙을 의미합니다.
>* 호스트 : (search.)naver.com -> 애플리케이션 서버(또는 분신 장치 등)의 위치를 의미합니다.
>* URL : search.naver -> 애플리케이션 서버 내부에서 라우트 위치를 나타냅니다.
>* 요청 매개 변수 : ?where=nexearch -> 추가적인 정보를 의미합니다.
>* &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &query=초콜릿
>* &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &sm=top_hty
>* &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &fbm=0
>* &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &ie-utf8
## 5. 미들웨어
* 미들웨서 설정 메소드
>* use() : 미들웨어를 설정합니다.
* 정적 파일 제공<br>
-> 웹 페이지에서 변경되지 않는 요소(이미지, 음악, 자바스크립트 파일, 스타일시트 파일 등)를 쉽게 제공<br>
-> public 폴더에는 이미지, 음악 등 원하는 파일을 넣음<br>
-> 현재 폴더에는 audio.mp3 파일과 image.png 파일을 넣음
* morgan 미들웨어<br>
-> express 모듈의 미들웨어로 사용할 수 있는 외부 모듈을 확인
>* express middleware<br>
https ://expressjs.com/en/resources/middleware.html
>* morgan 미들웨어 : 로그 출력 미들웨어
>* 로그 : 관련된 정보를 가진 글자
>* 로그 출력 미들웨어 : 웹 요청과 관련된 내용을 출력하는 미들웨어
* body-parser 미들웨어<br>
-> 요청 본문을 분석함
>* 클라이언트에서 서버로 데이터 전송
>>* URL을 사용한 요청<br>
-> 'http://localhost:52273/books/:id' 형태로 라우트하면 :id 부분을 변경 해서 데이터를 전달<br>
-> URL에 요청 매개 변수를 입력하면, 추가적인 정보를 객체 형태로 전달<br>
-> URL을 사용한 요청은 주소에 정보가 남는다는 단점이 있음, 쉽게 추적당해 문제가 발생함<br>
-> 요청 본문 사용 : 주소에 기록을 남기지 않고 데이터를 전달 가능함
>* 요청 본문
>>* 클라이언트가 서버로 본문을 전달할 때 요청 본문의 종류를 함께 전달
>>* MIME 형식
>>* 클라이언트가 어떤 Encoding-Type으로 요청했는지 확인, 변환해서 읽음(복잡) -> body-parser 미들웨어 : 쉽게 처리
>* body-parser 미들웨어
>>* https://github.com/expressjs/body-parser <설치>
>* 속성 정리 : 클라이언트가 서버로 데이터를 전송하는 세 가지 방법
>>* params 객체 : URL의 토큰. 보기가 간편
>>* query 객체 : URL의 요청 매개 변수. 토큰보다 많은 데이터를 전달할 수 있으며, 주소로 어떤 데이터가 오고 가는지 확인 가능
>>* body 객체 : 대용량 문자열 등을 전송할 때 사용. 주소에 데이터를 기록하지 못하므로 새로고침이나 즐겨찾기 기능 등을 활용 불가
# 11장 미니 프로젝트 - RESTful 웹 서비스
## 1. RESTful 웹 서비스 개요
* REST 규정에 맞게 만든 ROA를 따르는 웹 서비스 디자인 표준
>* GET : 컬렉션을 조회합니다. -> 컬렉션의 특정 요소를 조회합니다.
>* POST : 컬렉션에 새로운 데이터를 추가합니다. -> 요소를 사용하지 않습니다.
>* PUT : 컬렉션 전체를 한꺼번에 변경합니다. -> 컬렉션에 특정 요소를 수정합니다.
>* DELETE : 컬렉션 전체를 삭제합니다. -> 컬렉션의 특정 요소를 삭제합니다.
* RESTful 웹 서비스
>* GET : /user -> 모든 사용자 정보를 조회합니다.
>* POST : /user -> 사용자를 추가합니다
>* GET : /user/:id -> 특정 사용자 정보를 조회합니다.
>* PUT : /user/:id -> 특정 사용자 정보를 수정합니다.
>* DELETE : /user/:id -> 특정 사용자 정보를 제거합니다.
## 2. 코드 구성
## 3. Postman 크롬 애플리케이션
* 크롬 웹 브라우저에서 다음 주소에 접속한 후 애플리케이션을 다운로드<br>
-> https ://www.getpostman.com/




## [ 5월 18일 ]
# 9장 Node.js 기본
## 1. 전역 변수
* 전역변수, 전역함수, 전역 객체 : 모든 곳에서 사용할 수 있는 것들
>* __filename : 현재 실행 중인 코드의 파일 경로를 나타냅니다.
>* dirname : 현재 실행 중인 코드의 폴더 경로를 나타냅니다.

## 2. process 객체의 속성과 이벤트
* Node.js는 process전역 객체를 제공
* process 객체는 프로세스 정보를 제공하며, 제어할 수 있게 하는 객체<br>
### -> process 객체의 속성
>* env : 컴퓨터 환경 정보를 나타냅니다.
>* version : Node.js 버전을 나타냅니다.
>* versions : Node.js와 종속된 프로그램 버전을 나타냅니다.
>* arch : 프로세서의 아키텍처를 나타냅니다.
>* platform : 플랫폼을 나타냅니다.
### -> process 객체의 메소드
>* exit([exitCode] = 0 ]) : 프로그램을 종료합니다.
>* memoryUsage() : 메모리 사용 정보 객체를 리턴합니다.
>* uptime() : 현재 프로그램이 실행된 시간을 리턴합니다.
## process 객체와 이벤트 개요
* Node.js의 이벤트 연결 메소드
>* on(<이벤트 이름>, <이벤트 핸들러>) : 이벤트를 연결합니다.
* process 객체의 이벤트
>* exit : 프로세스가 종료될 때 발생합니다.
>* uncaughtException : 예외가 일어날 때 발생합니다.
>* 1. process 객체에 exit 이벤트와 uncaughtException 이벤틀슬 연결
>* 2. 이후에 예외를 강제로 발생시켜 이벤트가 발생하는지 확인
>* Node.js가 제공하는 객체의 이벤트 : https://nodejs.org/en/docs/
>* process 객체 : https://nodejs.org/dist/latest-v6.x/docs/api/process.html
* 이벤트 매개 변수 : 이벤트 핸들러의 매개 변수로 전달되는 매개 변수
>* exit  이벤트와 uncaughtException 이벤트의 이벤트 매개 변수를 출력
## 4. os 모듈
-> os 모듈의 메소드
>* hostname() : 운영체제의 호스트 이름을 리턴합니다.
>* type() : 운영체제의 이름을 리턴합니다.
>* platform() : 운영체제의 플랫폼을 리턴합니다.
>* arch() : 운영체제의 아키텍처을 리턴합니다.
>* release() : 운영체제의 버전을 리턴합니다.
>* uptime() : 운영체제가 실행된 시간을 리턴합니다.
>* loadavg() : 로드 에버리지 정보를 담은 배열을 리턴합니다.
>* totalmem() : 시스템의 총 메모리를 리턴합니다.
>* freemem() : 시스템의 사용 가능한 메모리를 리턴합니다.
>* cpus() : CPU의 정보를 담은 객체를 리턴합니다.
>* getNetworkInterfaces() : 네트워크 인터페이스의 정보를 담은 배열을 리턴합니다.
## 5. URL 모듈
-> url 모듈의 메소드
>* parse(urlStr[.parseQueryString = false.slashesDenoteHost = false]) : URL 문자열을 URL 객체로 변환해 리턴합니다.
>* format(urlObj) : URL 객체를 URL 문자열로 변환해 리턴합니다.
>* resolve(from. to) : 매개 변수를 조합하여 완전한 URL 문자열을 생성해 리턴합니다.
* url 모듈 -> url 모듈을 추출하고, parse()메소드를 사용
## 6. File System 모듈
* fs 모듈 추출 방법
> const fs = require('fs');
* 파일 읽기 메소드
>* fs.readFileSync(<파일 이름>) : 동기적으로 파일을 읽어 들입니다.
>* fs.readFile(<파일 이름>, <콜백 함수>) : 비동기적으로 파일을 읽어 드립니다.
* fs.readFileSync() 메소드를 사용해 동기적으로 파일을 읽음
* 동기와 비동기의 실행 결과는 같지만 내부 실행 구조는 다름
* 동기적으로 파일을 읽어 들일 때 코드 순서
## 비동기 처리의 장점
* 웹 서버를 C++ 프로그래밍 언어로 만들면 무척 빠르지만, 개발과 유지 보수는 어려움
* 전 세계 웹 서비스 기업(페이스북, 트위터 등)도 C++로 웹 서버를 개발하지 않고 PHP, 자바, 루비, 파이썬, Node.js 등 프로그래밍 언어로 개발
* 프로그래밍 언어 자체는 느리지만 큰 의미가 없다고 판단해 개발 속도와 유지 보수성이 좋은 프로그래밍 언어를 사용
* 자바 스크립트 프로그래밍 언어는 C++, 자바보다 느리지만 Node.js를 사용하면 손쉽게 비동기 처리를 구현하여 빠른 처리가 가능
* 파일 쓰기 메소드
>* fs.writeFileSync(<파일 이름>, <문자열>) : 동기적으로 파일을 씁니다.
>* fs.writeFile(<파일 이름>, <문자열>, <콜백 함수>) : 비동기적으로 파일을 씁니다.
* 파일 처리와 예외 처리<br>
-> 동기 코드 예외처리 : try catch 구문<br>
-> 비동기 코드 예외처리 : 콜백함수의 첫 번째 매개 변수 error를 활용
## 7. 노드 패키지 매니저
* 과거의 프로그래밍 언어들은 외부 모듈 설치가 어려웠음
* 현재는 '패키지 매니저' 모듈 관리 프로그램을 사용해 모듈을 쉽게 설치하고 활용 가능함
* node.js는 npm(Node.js Package Manager)패키지 매니저를 사용
## 8. request 모듈
* 웹 요청을 쉽게 만들어 주는 모듈로 외부 모듈임
* 코드 실행 전에 npm install request 명령어를 실행해서 request 모듈을 설치
## 9. cheerio 모듈
* request 모듈로 가져온 웹 페이지는 단순한 HTML 문자열임<br>
여기에서 원하는 정보를 추출해야 단순한 '데이터'가 '정보'가 됨 -> 파싱
* cheerio 모듈 : 가져온 웹 페이지의 특정 위치에서 손쉽게 데이터 추출
* cheerio 모듈 설치






## [ 5월 11일 ]
# 7장 4. Date 객체
>* new Date() : 현재 시간으로 Date 객체를 생성합니다.
>* new Date(<유닉스 타임>) : 유닉스 타임(1970년 1월 1일 >* 00시 00분 00초부터 경과한 밀리초)으로 Date 객체를 생성합니다.
>* new Date(<시간 문자열>) : 문자열로 Date 객체를 생성합니다.
>* new Date(<년>, <월 -1>, <일>, <시간>, <분>, <밀리초>) : >* 시간요소(년, 월-1, 일, 시간, 분, 초, 밀리초)를 기반으로 Date 객체를 생성합니다.
★ Month를 나타내는 '월'은 0부터 시작..... 0 -> 1월, 11 -> 12월
#
* 메소드 활용
>* Date 객체
> -> getOO()형태 메소드, setOO() 형태 메소드 : FullYear, Month, Day, Hours, Minutes, Seconds 등 사용.
>* getTime() 메소드 : 유닉스 타임
>* 2개의 시간을 빼고, 일 단위(1000밀리초 * 60초 * 60분 * 24시간)로 나누어 시간간격을 구함.
### Array 객체
* Array 객체의 기본 메소드
* -> 대부분 파괴적 메소드로 자기 자신을 변경
>* concat() : 매개 변수로 입력한 배열의 요소를 모두 합쳐 배열을 만들어 리턴합니다.
>* join() : 배열 안의 모든 요소를 문자열로 만들어 리턴합니다.
>* pop()* : 배열의 마지막 요소를 제거하고 리턴합니다.
>* pust()* : 배열의 마지막 부분에 새로운 요소를 추가합니다.
>* reverse()* : 배열의 요소 순서를 뒤집습니다.
>* slice() : 배열 요소의 지정한 부분을 리턴합니다.
>* sort()* 배열의 요소를정렬합니다.
>* splice()* : 배열 요소의 지정한 부분을 삭제하고 삭제한 요소를 리턴합니다.
* ECMAScript5에서 추가된 메소드
>* forEach() : 배열의 요소를 하나씩 뽑아 반복을 돌립니다.
>* map() : 콜백 함수에서 리턴하는 것을 기반으로 새로운 배열을 만듭니다.
>* filter() : 콜백 함수에서 true를 리턴하는 것으로만 새로운 배열을 만들어 리턴합니다.

# 8. 예외처리
### 1. 예외와 기본 예외 처리
- 예외 : 실행에 문제가 발생하면 자동 중단 됨. 이렇게 발생한 오류<br>
- 예외 처리 : 오류에 대처할 수 있게 하는 것

### 2. 고급 예외 처리
* 1. 예외 상황 확인 : 배열을 생성할 때 길이를 음수로 지정하면 RangeError가 발생.
* 2. 고급 예외 처리 : try catch finally 구문

### 3. 예외 객체
* 예외가 발생하면 어떤 예외가 발생했는지 정보를 전달함.
* catch 구문의 괄호 안의 변수.
* name 속성과 message 속성이 있음.

### 4. 예외 강제 발생
* throw 키워드 사용
 -> throw 키워드 뒤에는 문자열 또는 Error 객체를 입력.
* 자세한 예외 출력은 Error 객체를 사용
 -> 어떤 파일의 몇 번째에 줄에서 예외가 발생했는지도 확인 가능.
 * 문자열을 사용할 때에는 catch 구문의 예외 객체에 간단한 문자열만 전달됨.
 * Error 객체를 사용한 예외 강제 발생 때의 예외 객체








## [05월 4일]
# 6장 4. 생성자 함수와 프로토타입
* 객체 지향 프로그래밍 : 현실의 객체를 모방해서 프로그래밍
* 배열과 객체를 사용하면 여러 개의 데이터를 쉽게 다룰 수 있음<br>
### 생성자 함수
* 객체를 만드는 함수, 대문자로 시작하는 이름 사용<br>
### 프로토 타입
* 생성자 함수로 만든 객체는 프로토 타입 공간에 메소드를 지정해서 모든 객체가 공유 하도록 함, 해당 함수를 생성자 함수로 사용했을 때만 의미가 있음
# 7장 표준 내장 객체
### 기본 자료형과 객체 자료형의 차이
* 자바 스크립트는 다양한 객체를 제공
* 기본 자료형 숫자, 문자열, 불
>* 기본 자료형의 속성 또는 메소드를 사용할 때 기본 자료형이 자동적으로 객체로 변환이 됨. 즉, 기본 자료형과 객체 자료형 모두 속성과 메소드를 사용함
>* 차이점 : 기본 자료형은 객체가 아니므로 속성과 메소드를 추가할 수 없음
### Number 객체
* 자바 스크립트에서 숫자를 표현할 때 사용
* Number 객체 생성
>* toExponential() : 숫자를 지수 표시로 나타낸 문자열을 리턴합니다.
>* toFixed() : 숫자를 고정소수점 표시로 나타낸 문자열을 리턴합니다.
>* toPrecision() : 숫자를 길이에 따라 지수 표시 또는 고정소수점 표시로 나타낸 문자열을 리턴합니다.
####
* 생성자 함수의 속성과 메소드
>* MAX_VALUE : 자바 스크립트의 숫자가 나타낼 수 있는 최대 숫자
>* MIN_VALUE : 자바 스크립트의 숫자가 나타낼 수 있는 최소 숫자
>* NaN : 자바 스크립트의 숫자로 나타낼 수 없는 숫자
>* POSITIVE_INFINITY : 양의 무한대 숫자
>* NEGATIVE_INFINITY : 음의 무한대 숫자
### String 객체
* 속성과 메소드
> length : 문자열의 길이를 나타냅니다.
#### 
* String 객체의 메소드는 변경된 값을 리턴함.
> charAt(position) -> position에 위치하는 문자를 리턴합니다.<br>
charCodeAt(position) -> position에 위치하는 문자의 유니코드 번호를 리턴합니다.<br>
concat(args) -> 매개 변수로 입력한 문자열을 이어 리턴합니다.<br>
indexOf(searchString, position) -> 앞에서부터 일치하는 문자열의 위치를 리턴합니다.<br>
lastIndexOf(searchString, position) -> 뒤에서부터 일치하는 문자열의 위치를 리턴합니다.<br>
match(regExp) -> 문자열 안에 regExp가 있는지 확인합니다.<br>
replace(regExp, replacement) regExp를 replacement로 바꾼 후 리턴합니다.<br>
search(regExp) -> regExp와 일치하는 문자열의 위치를 리턴합니다.<br>
slice(start, end) -> 특정 위치의 문자열의 추출해 리턴합니다.<br>
split(separator, limit) -> separator로 문자열을 잘라 배열을 리턴합니다.<br>
substr(start, count) -> start부터 count만큼 문자열을 잘라서 리턴합니다.<br>
substring(start, end) -> start부터 end까지 문자열을 잘라서 리턴합니다.<br>
toLowerCase() -> 문자열을 소문자로 바꾸어 리턴합니다.<br>
toUpperCase() -> 문자열을 대문자로 바꾸어 리턴합니다.<br>
####
* 메소드 활용
>* indexOf() 메소드 : 특정 문자열이 있는지 확인, 위치를 리턴함. 문자열이 포함되어 있지 않을 때는 -1을 리턴




## [04월 27일]

# <6장. 객체>
* 배열
>* 배열 선언식<br>
     let array = ['사과', '바나나', '망고, '딸기'];<br><br>
>* 배열 접근<br>
    array[0] -> 사과<br>
    array[1] -> 망고<br>
    <배열은 요소에 접근할 때 인덱스를 사용하고, 객체는 키를 사용함><br><br>
>* 객체 선언식<br>
    let product = {<br>
    제품명 : '7D 건조 망고',<br>
    유형 : '당절임',<br>
    성분 : '망고, 설탕, 메타중아황산나트륨, 치자황색소',<br>
    원산지 : '필리핀'<br>
    };<br><br>
    출력문<br>
    console.log(product);<br><br>
<키> - 제품명, 유형, 성분, 원산지<br>
<속성> - 7D 건조 망고, 당절임, (망고, 설탕, 메타중이황산나트륨, 치자황색소), 필리핀<br>
<객체 접근><br>
product['키1'] -> '속성1'<br>
: product.키1 -> 속성1<br><br>

* 객체와 반복문
>* 객체와 반복문<br>
객체 선언<br>
let object = {<br>
&nbsp;&nbsp;&nbsp;&nbsp;name: '바나나',<br>
&nbsp;&nbsp;&nbsp;&nbsp;price: 1200<br>
};<br><br>
출력<br>
for(let key in object){<br>
&nbsp;&nbsp;&nbsp;&nbsp;console.log('&{object[key]}');<br>
}<br>

* 속성과 메소드
>* 요소 : 배열 내부에 있는 값 하나하나
>* 속성 : 객체 내부에 있는 값 하나하나
>* 객체의 다양한 자료형
>* 메소드 : 객체의 속성 중 자료형이 함수인 속성<br>
객체 선언식<br>
let object = {<br>
&nbsp;&nbsp;&nbsp;&nbsp;name : '바나나',<br>
&nbsp;&nbsp;&nbsp;&nbsp;price : 1200,<br>
&nbsp;&nbsp;&nbsp;&nbsp;print : function (){<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
console.log('${this.name}의 가격은 ${this.price}원입니다.')<br>
&nbsp;&nbsp;&nbsp;&nbsp;}<br>
};<br><br>
호출<br>
object.print();<br><br>
출력 -> 바나나의 가격은 1200원입니다.<br>

* 생성자 함수와 프로토타입
>* 객체 지향 프로그래밍 : 현실의 객체를 모방해서 프로그래밍
>* 생성자함수<br>
객체를 만드는 함수, 대문자로 시작하는 이름을 사용함




## [ 03월 30일 ]

# < IF 문 >
* 기본 형태
> if (<불 표현식>){ }




## [ 03월 23일 ]

* 기본 용어
>* 표현식과 문장 <br>
표현식 : <br> 273 <br>  10+20+30+2 <br> "JavaScript Programming"<br>
문장 : 표현식이 하나 이상 모일 경우, 마지막에 종결 의미로 세미콜론 (;) <br>
프로그램 : 문장이 모이면 프로그램이 됨<br>
>* 기본용어 <br>
키워드 : 자바 스크립트에서 특별한 의미가 부여된 단어 <br>
식별자 : 이름을 붙일 때 사용하는 단어, 변수와 함수 이름 등으로 사용<br>
----------> 키워드 사용 불가 <br>
----------> 특수 문자는 _와 $만 허용<br>
----------> 숫자로 시작하면 안됨<br>
----------> 공백은 입력하면 안됨<br>
식별자 사용 규칙 : <br>
----------> 생성자 함수의 이름은 항상 대문자로 시작<br>
----------> 변수, 함수, 속성, 메소드의 이름은 항상 소문자로 시작<br>
----------> 여러 단어로 된 식별자는 각 단어의 첫 글자를 대문자로 함<br>
주석 : 프로그램의 진행에 영향을 주지 않는 코드<br>

* 출력
>* 출력 메소드<br>
console 객체의 log() 메소드 사용 : console.log()메소드<br>
>* REPL을 사용한 출력<br>
-> 곧바로 문장을 입력해서 출력

*기본 자료형
>* 숫자<br>
-> 가장 기본적인 자료형<br>
-> 연상자 우선순위 : consolo.log(5+3+2)
->나머지 연산자 : %
>* 문자열<br>
->문자의 집합<br>
->문자열 생성시 큰따옴표나 작은따옴표 사용<br>
->이스케이프 문자 : 따옴표를 문자 그대로 사용 가능, 문자열 줄바꿈 할 경우 사용<br>
___\t : 수평 탭 <br>
___\n : 줄바꿈<br>
___\' : 작은따옴표<br>
___\\* : 큰따옴표<br>
___\\\\ : 역슬레시<br> 
-> 문자열 합하기 <br>
___\'+\' : 문자열 연결 연산자<br>
->문자 선택 연산자<br>
___문자열[숫자] : 문자 선택 연산자
 >* 불<br>
 -> 참과 거짓의 표현 : tru와 false<br>
 -> 비교 연산자 : == 같습니다. <br>
 ________________ : ( != ) 다릅니다. <br>
 ________________ : ( > ) 왼쪽 피연산자가 큽니다. <br>
 ________________ : ( < ) 오른쪽 피연산자가 큽니다. <br>
 ________________ :( >= ) 왼쪽 피연산자가 크거나 같습니다. <br>
 ________________ : ( <= ) 오른쪽 피연산자가 크거나 같습니다. <br>
 ->논리연산자 : ( ! ) 논리 부정 연산자<br>
 ________________( || ) 논리합 연산자<br>
 ________________( && ) 논리곱 연산자<br>

 * 변수
 >변수 : 값을 저장할 때 사용하는 식별자, 변수 선언 후 변수에 값을 할당
 
 * 복합 대입 연산자<br>
>* 변수에 사용할 수 있는 몇 개의 특별한 연산자가 존재 <br>
>>* a += 10 는 a = a + 10과 결과가 같음<br>
+= : 숫자 덧셈 후 대입 연산자<br>
 -= : 숫자 뺄셈 후 대입 연산자<br>
 *= : 숫자 곱셈 후 대입 연산자<br>
 /= : 숫자 나눗셈 후 대입 연산자<br>
 >>* 문자열에 적용하는 복합 대입 연산자<br>
 += : 문자열 연결 후 대입 연산자<br>

 * 증감 연산자
 >>* 증감연산자>*변수++ : 기존 변수 값에 1을 더합니다(후위)<br>
 변수++ : 기존 변수 값에 1을 더합니다(후위)<br>
 ++변수 : 기존 변수 값에 1을 더합니다(전위)<br>
 변수-- : 기존 변수 값에서 1을 뺍니다(후위)<br>
 --변수 : 기존 변수 값에서 1을 뺍니다(전위)<br>
 >* 전위는 문장을 실행하기 전에 값을 변경하라는 의미
 >* 즉 console.log(++number)코드는 console.log (number)를 실행하기 전에 변수 number에 1을 더함

 * 자료형 검사
 >* 자료형 확인 연산자 <br>
 >> typeof : 해당 변수의 자료형을 추출한다.<br>
 (보통은 연산자 뒤에 관호를 붙임)<br>
 >>* 자바스크립트의 여섯가지 자료형<br>
 --> 문자열<br>
 \>typeof('String')<br>
 &nbsp; 'string' <br>
  --> 숫자<br>
 \>typeof(273)<br>
 &nbsp; 'number' <br>
  --> 불<br>
 \>typeof(true)<br>
 &nbsp; 'boolean' <br>
  --> 함수<br>
 \>typeof(function () {} )<br>
 &nbsp; 'function' <br>
  --> 객체<br>
 \>typeof({})<br>
 &nbsp; 'object' <br>
  --> undefined<br>
 \>typeof(alpha)<br>
 &nbsp; 'undefined' <br>

 * undefined 자료형
 >* undefined 자료형 : 변수를 선언했으나 초기화 하지 않은 자료형

 * 강제 자료형 변환
 >* Number() : 숫자로 자료형 변환합니다.<br>
 > String() : 문자열로 자료형 변환합니다.<br>
 > Boolean() :  불로 자료형 변환합니다. <br>
 >* Number() 함수와 NaN<br>
 -> '숫자로 변환할 수 없는 문자열'을 Number() 함수로 변환하면 'NaN'을 출력<br>
 -> NaN (Not a Number)은 '숫자 자료형이지만 숫자가 아닌 것'을 의미<br>
 -> NaN의 특징<br>
 >> 1. NaN은 무조건적으로 다름
 >>2. NaN인지 확인할 때는 isNaN() 함수를 사용
>* NaN(Not a Number)의 고찰
>>* 표현 불가능한 수치형 결과를 나타내는 값.
>>* 자기 자신과 일치하지 않는 유일한 값.<br>
>> (자기 자신과도 일치하지 않기 때문에 nan == nan이 false이다.)<br>
>* Boolean() 함수
>>* Boolean() 함수를 사용하면 5개 요소는 false로 변환<br>
>> -> 0, NaN, ""[빈 문자열], null, undefined<br>

* 자동 자료형 변환
>* 숫자와 문자열 자료형 자동 변환
>>* 숫자와 문자열에 '+' 연산자를 적용하면 자동으로 숫자가 문자열로 변환<br>
>>* 불 자료형 자동 변환<br>
-> ! 연산자를 두 번 사용해 Boolean() 함수를 사용하는 것과 같은 효과<br>

* 일치 연산자
>* 자료형까지 검사 <br>
=== : 자료혀오가 값이 같은지 비교합니다.<br>
!== : 자료형과 값이 다른지 비교합니다.<br>

* 상수
>* 상수 : '항상 같은 수'라는 의미, 변수와 반대되는 개념
>* const : 상수(constant)를 만드는 키워드
>* 변하지 않을 대상에 상수를 적용




 
 




#홍시원 [202030434]
## [ 03월 16일 ]

>오늘 배운 내용 요약 <br>
>요약







# 홍시원 [202030434]
## [ 03월 09일 ]

<!-- <h1> ~ <h6> -->
기본 글자 크기
# h1
## h2
...
###### h6
---
* 문장
> 문장
> 문장
> 문장
> 문장
> 문장