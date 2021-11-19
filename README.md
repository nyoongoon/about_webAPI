# about_webAPI
webAPI에 대해 알게 된 것을 기록하는 저장소입니다.

# Blob(Binary Large Object)
- 파일류의 미가공 불변 데이터를 나타냄. 텍스트와 바이너리 형태로 읽을 수도 있으며, ReadableStream으로 변환한 후 그 메서드를 사용해 데이터를 처리할 수도 있음. 
- File인터페이스는 사용자 시스템의 파일을 지원하기 위해 Blob인터페이스를 상속함.


# File API
```javascript
<input type = "file" id ="input">
```
- File API는 사용자에 의해 선택된 파일을 나타내는 객체인 File을 포함하는 FileList에 접근할 수 있게 해줌.
- input요소에 change 이벤트리스너를 붙여 파일의 변경사항을 다룰 수 있음
## File
## FileList
<br/><br/>

# FormData 
- form필드와 그 값을 나타내는 키/값쌍을 쉽게 생성하는 방법을 제공. ajax를 이용하여 쉽게 데이터 전송가능. 
```javascript
var formData = new FormData($form);
$.ajax({
	url:url,
	type:'post',
	data: formData,
	cache:false,
	contentType:false,
	processData; false,
	success:function(){

	}
}); 
```
<br/><br/>
# Multipart form data 

- multipart/form-data is **one of the value of enctype attribute**, which is used in form element that have a file upload. multi-part means form data divides into multiple parts and send to server.

### enctype attribute ?
- 이 속성은 \<form\>요소의 method 속성값이 post인 경우에만 사용.
- enctype(인코드 타입) 속성은 서버로 데이터가 보내지기 전에 어떻게 인코딩이 되어야하는지 명시해주는 속성이다.
- 기본값은  "application/x-www-form-urlencoded". 공백은 "+" 로, 특수 문자는 아스키코드로 변환되어 인코딩된다.  
<br/> --> (key=value&key=value 형태로 전송되며, 영숫자가 아닌 문자는 퍼센트 기호 및 문자의 ASCII 코드를 나타내는 두 개의 16 진수로 변환됨. 우리가 전송하려는 데이터가 영숫자가 아닌 경우 3바이트로 표현하기 때문에 바이너리 파일을 전송할 경우 페이로드를 3배로 만들기에 무척 비효율적)
- "multipart/form-data". 모든 문자를 인코딩하지 않음. 파일이나 이미지를 서버에 전송할 때 주로 사용.
<br/> --> (바이너리 데이터를 효율적으로 전송할 수 있으나 웹에서 많이 사용되는 텍스트로만 이루어진 POST 전송은 오히려 MIME 헤더가 추가되기 때문에 오버 헤드가 발생됨)
- "text/plain". 공백문자는 "+" 로 변환되지만, 나머지 문자는 모두 인코딩 되지 않음.
<br/><br/>

# ReadableStream
- 바이트 데이터를 읽을 수 있는 스트림을 제공. Fetch API는 Response 객체의 body 속성을 통해서 ReadableStream의 구체적인 인스턴스를 제공. 
<br/><br/>


# REST, REST-ful, REST-API
## REST
- 존재하는 자원(Resource)을 식별하고 제어하는 방법론.

### 자원(Resource)이란?
- 일이 처리되는 비용
- 컴퓨터의 자원이란 cpu가 수행하는 명령, 하드디스크에 저장되는 파일, 메모리에 저장되는 데이터들을 의미한다.
- REST는 컴퓨터 자원을 사용하여 처리하는 한 단위의 작업을 **식별, 제어**할 수 있어야한다. 
- 자원을 식별할 수 있는 식별자가 필요.

### 자원의 제어(Resource Methods)
- CRUD를 자원에 수행하는 것.
- 제어 방법은 일관적 인터페이스로 구성되어야 한다. 

### 자원의 표현(Resource Representation)
- 조회한 순간의 자원 상태를 의미.
- REST의 자원의 표현은 자기서술적인(self-descriptive)메시지와 HATEOAS(hypermedia as the engine of application state)로 구성됨. 이는 데이터를 설명하는 메타데이터, 다음 자원으로의 이동을 안내하는 하이퍼 텍스트 등이 포함. REST은 클라이언트가 자원의 표현만 보더라도 이해 할 수 있는 것을 목표로 함.

## 웹기반(HTTP)의 REST
- 보통 말하는 REST시스템은 HTTP기반의 REST시스템임.

### 자원의 식별 
- HTTP는 REST 시스템이 요구하는 자원의 식별을 **URL**의 정의로 처리합니다. 
- 자원은 명사로 커뮤니케이션 하기 때문에 **URL을 명사로** 표현함으로써 자원을 
나타낸다. 

### 자원의 제어
- HTTP는 자원의 제어를 HTTP Method로 표현함. -> get(조회)/post(등록)/put(수정_/delete(삭제).

### 자원의 표현 
- HTTP는 자원의 표현을 HTTP 응답 메시지로 구현함.
- self-descriptive와 HATEOS를 만족시키기 위해 ContentType 또는 커스텀 HTTP헤더에 메타데이터 명시, 데이터 링크를 포함하는 등의 기법 사용. 

## REST-FUL
### REST 시스템의 구성 요소는 6개.
- 1 Client-Server
- 2 Stateless
- 3 Cacheable
- 4 Unitform-Interface
- 5 Layered-System
- 6 Code on demand(optional)
- -> 4번째 요소는 구현이 어렵기 때문에 생략하기도 한다. 
- 모든 구성요소를 완벽하게 지킨 REST 시스템을 **REST-FUL** 시스템이라고 한다.

## REST-API
- API는 컴퓨터의 자원 제어 방법의 집합.
- REST-API는 REST시스템의 자원 제어 방법의 집합임.
<br/><br/>
