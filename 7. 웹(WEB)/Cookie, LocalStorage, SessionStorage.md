# 🍪 Cookie

쿠키는 클라이언트에 대한 정보를 이용자의 PC의 하드디스크에 보관하기 위해서 웹사이트에서 클라이언트의 웹 브라우저에 전송하는 정보이다.

## Cookie의 특징

- 웹 사이트에서 쿠키를 설정하면 모든 웹 요청은 쿠키 정보를 포함하여 서버로 전송된다.
- 쿠키는 개수와 용량에 있어 제한을 걸어두고 있다.

  - 하나의 사이트에서 사용할 수 있는 최대 쿠키 수는 20개이다.
  - 하나의 사이트에서 저장할 수 있는 최대 쿠키 크기는 **4KB**로 제한되어 있다.

- 쿠키는 만료 일자를 지정하게 되어 있어 언젠가 제거된다.
  - 만료 일자로 지정된 날짜에 쿠키는 제거된다.
  - 만료 일자를 지정하지 않으면 세션 쿠키가 된다.

## Cookie의 장/단점

- 장점 : 대부분의 브라우저에 지원이 다 된다.
- 단점 : API가 한번 더 호출되므로 서버에 부담이 증가된다.

<br><br>

# 웹 스토리지

HTML5에는 웹사이트의 데이터를 클라이언트에 저장할 수 있는 새로운 자료구조인 WebStorage 스펙이 포함되어 있다.

WebStorage의 개념은 키/값 쌍으로 데이터를 저장하고
키를 기반으로 데이터를 조회하는 패턴이다.

그리고 영구저장소(LocalStorage)와 임시저장소(SessionStorage)를 따로 두어 데이터의 지속성을 구분할 수 있어 응용 환경에 맞는 선택이 가능하다.

쿠키와 거의 차이가 없어 보일지라도 몇가지 쿠키의 단점을 극복하는 개선점이 도입됬다.

<br><br>

# 웹 스토리지의 특징

- 저장된 데이터가 클라이언트에 존재할 뿐 **서버로 전송은 이루어지지 않는다.** 이것은 네트워크 트래픽 비용을 줄여준다는 주요한 장점이 된다.

- WebStorage는 용량의 제한이 없다.
- 만료기간의 설정이 없다. 즉, 한번 저장한 데이터는 영구적으로 존재하는 것이다.

- 프로토콜, 호스트, 포트가 같으면 같은 스토리지를 공유한다.

- LocalStorage, SessionStorage 존재
- 둘의 차이점은 **데이터의 영구성**이다.
- 두 스토리지는 모두 window 객체 안에 들어 있다.
- 두 스토리지는 Storage 객체를 상속받기 때문에 메소드가 공통적으로 존재한다.

- 도메인 별 용량 제한도 존재한다.
- 브라우저별 기기별로 다르긴 하지만 모바일은 2.5mb, 데스크탑은 5mb~10mb의 용량을 갖는다.

## 1. 로컬 스토리지 (LocalStorage)

- 로컬 스토리지는 저장한 데이터를 지우지 않는 이상 영구적으로 보관이 가능하다.
- 도메인마다 별도로 로컬 스토리지가 생성이 된다.

- window.localStorage에 위치한다.
- Windows 전역 객체의 LocalStorage라는 컬렉션을 통해 저장/조회가 이루어진다.
- key / value 저장소이기 때문에 key와 value를 순서대로 저장하면 된다.
- 값으로는 문자열, boolean, 숫자, null, undefined 등을 저장할 수 있지만, 모두 문자열로 변환된다.
- 키도 문자열로 변환된다.

<br>

### (1) 로컬 스토리지 (LocalStorage) 특징

- ⭐⭐⭐ 브라우저를 종료해도 데이터는 보관되어 다음번 접속해도 그 데이터를 사용할 수 있다.
- 지속적으로 필요한 데이터 (자동 로그인 등)을 저장
- 하지만 비밀번호 같은 중요한 정보는 절대 저장하면 안된다.

<br>

### (2) 로컬 스토리지 (LocalStorage) 저장/조회/삭제하는 법

#### 2-1. 사용방법

```javascript
localStorage.setItem(키, 값); // 저장
localStorage.getItem(키, 값); // 조회
localStorage.removeItem(키); // 삭제
localStorage.clear(); // 스토리지 전체 비우기
```

<br>

#### 2-2. 예시

```javascript
localStorage.setItem('name', 'crystal993');
localStorage.getItem('name'); //crystal993
localStorage.removeItem('name');
localStorage.getItem('name'); //null
localStorage.clear(); // 전체 삭제
```

<br>

#### 2-3. 객체

객체를 저장할 때는 `JSON.stringfy`
객체를 가져올 때는 `JSON.parse`

```javascript
localStorage.setItem('object', JSON.stringfy({a: 'b'}));
JSON.parse(localStorage.getItem('object')); //[object Object]
```

<br><br>

## 2. 세션 스토리지 (Session Storage)

- 세션 스토리지는 window.sessionStorage에 위치한다.
- ⭐⭐ 세션 스토리지는 세션 종료 시(브라우저를 닫을 경우) 클라이언트에 대한 정보가 삭제된다.
- 세션 스토리지는 Windows 전역 객체의 SesssionStorage 라는 컬렉션을 통해 저장/조회가 이루어진다.

<br>

### SessionStorage의 특징

- 데이터가 지속으로 보관되지 않는다.
- 이는 마치 브라우저 기반의 세션 쿠키와 그 성질이 비슷한데, 현재 페이지가 브라우징 되고 있는 브라우저 컨텍스트 내에서만 데이터가 유지된다.
- 주로 일회성 정보들을 저장한다.

<br>

### SessionStorage의 장/단점

```javascript
sessionStorage.setItem(키, 값); // 저장
sessionStorage.getItem(키, 값); // 조회
sessionStorage.removeItem(키); // 삭제
sessionStorage.clear(); // 스토리지 전체 비우기
```

<br>

## Cookie vs LocalStorage vs SessionStorage 어떤 상황에서 사용하는 게 좋을까?

- 팝업창 : Cookie
- 자동 로그인 : LocalStorage
- 입력 폼 정보 : SessionStorage
- 비로그인 장바구니 : SessionStorage

<br><br>

[참고링크1](https://jindev-t.tistory.com/107)
[참고링크2](https://www.zerocho.com/category/HTML/post/5918515b1ed39f00182d3048)
