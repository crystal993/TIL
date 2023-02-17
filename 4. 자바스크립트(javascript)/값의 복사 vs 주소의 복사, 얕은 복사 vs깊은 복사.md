### 🐬 값의 복사 (call by value) vs 주소의 복사 (call by reference)

#### 1. 값의 복사(Call By Value)

```javascript
let origin = 'crystal';
let copy = origin;
origin = '수정';

console.log(copy); // crystal
```

<br>

- 원본 orgin의 값을 '수정'으로 변경해도, copy의 값 'cryatal'은 변하지 않는다.

- `call by value` 란 값이 그대로 복사되는 것을 의미한다.

- 원시데이터의 경우 값의 복사 (`Call By Value`) 가 일어난다.

<br><br>

#### 2. 주소의 복사 (Call by Reference)

```javascript
let origin = [1, 2, 3];
let copy = origin;
origin.pop();

console.log(origin); // [1, 2]
console.log(copy); // [1, 2]
```

origin => 201 => 560 => [1,2,3]
copy => 201 => 560 => [1,2,3]

<br><br>

- 참조 타입은 가변성을 가진다.

- orgin 배열을 pop() 해서 마지막 요소 3을 제거했음에도 불구하고, origin, copy 둘 다 [1,2]만
  반환되는 것을 볼 수 있다.

- copy는 origin을 복사할 때 201을 복사함.
  => ⭐ 같은 주소값을 복사해서 같은 값을 공유하고 있다.

- `Call by reference`는 데이터가 있는 공간(주소:메모리의 위치)이 `참조` 되는 것을 의미한다.

- 객체는 `Call by reference`가 일어난다.

<br>

https://lamarr.dev/javascript/2020/04/08/04.html

<br>
<br>
<br>

### 🐬 깊은 복사와 얕은 복사의 차이에 대해서 설명하세요. 자바스크립트에서 깊은 복사를 하는 방법은 무엇인가요?

#### 1. 깊은 복사 (deep copy)

깊은 복사는 객체가 중첩되어 있는 상황일 때 내부 객체까지 모두 새로 생성된 것을 의미합니다. 이 때 복사된 A객체와 B객체 중 어느 하나를 수정해도 다른 객체에 영향을 미치지 않습니다.

<br>

#### 2. 얕은 복사 (shallow copy)

- 얕은 복사는 상위 객체만 새로 생성되고 내부 객체들은 참조 관계인 경우를 의미합니다. 같은 주소값을 가리키기 때문에 복사된 A객체와 B객체 중 어느 하나를 수정하면 다른 객체에 영향을 미칩니다. 자바스크립트에서 깊은 복사를 하는 방법은 재귀함수를 이용하여 복사하거나 lodash()라이브러리를 사용하는 방법이 있습니다.

<br>
	<br>
