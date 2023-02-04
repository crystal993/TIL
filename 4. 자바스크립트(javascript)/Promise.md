# 1. Promise

<br>

## 1.1 왜 Promise를 쓰게 되었을까?

- 연속되는 비동기함수와 콜백함수를 사용하여 비동기 처리를 하면서 콜백지옥이 생김.

- 다음과 같이 콜백 함수의 콜백 함수의 콜백 함수를 넣어서 비동기 처리의 결과를 또 다른 비동기 처리의 매개변수로 전달 할 수 있다.

- 콜백 함수는 주로 이벤트 처리나 서버 통신과 같은 비동기 작업을 제어 하기 위해 사용되지만 콜백 함수를 반복 해서 사용하게 되면, 들여 쓰기 수준이 감당할 수 없을 정도록 깊어지게 된다.

<br>

## 1.2 Promise

- ⭐ 자바스크립트의 비동기를 돕는 객체 ⇒ 비동기 처리의 결과값을 핸들링 가능 ⇒ 비동기 처리 함수에 콜백을 줄지어 전달할 필요가 없다.

- 프라미스란 비동기 연산이 종료된 이후에 결과를 알기 위해 사용하는 객체입니다.

- 프라미스를 사용하면, 비동기 메서드를 마치 동기 메서드처럼 값을 반환할 수 있습니다.

- then()과 catch()문의 체이닝을 통해 값을 반환 받아올 수 있습니다.

- .then으로 함수실행순서를 정할 수 있다.

- 위 그림의 callback 처럼 함수들이 많아질수록 작성하기가 어렵고 가독성이 떨어집니다.

<br>

promise는 언젠가 완료가 되는 작업의 결과값을 담는 상자와 같은 역할 을 합니다.콜백지옥을 해결하기 위한 Promise는 다음 중 하나의 상태를 가집니다. 세가지 상태 중 하나를 가짐

<br>

#### ✔ 대기 ( pending ) : 이행하지도 거부하지도 않은 초기 상태

#### ✔ 이행 ( fulfill ) : 연산 성공, 비동기 작업이 우리가 의도한대로 정상적으로 작동함.

#### ✔ 거부 ( reject ) : 연산 실패, 비동기 작업이 모종의 이유로 실패, (서버 에러, 시간 초과 등)

<br>

```javascript
function taskA(a, b) {
const executor = (resolve, reject) => {
setTimeout(() => {
const res = a + b;
resolve(res);
}, 3000);
};
return new Promise(executor);
}

function taskB(a) {
const executor = (resolve, reject) => {
setTimeout(() => {
const res = a \* 2;
resolve(res);
}, 1000);
};
return new Promise(executor);
}

function taskC(a) {
const executor = (resolve, reject) => {
setTimeout(() => {
const res = a \* -1;
resolve(res);
}, 2000);
};
return new Promise(executor);
}

// Promise도 뭔가 콜백지옥 같은 느낌
taskA(5, 1).then((a_res) => {
console.log("A RESULT : ", a_res);
taskB(a_res).then((b_res) => {
console.log("B RESULT : ", b_res);
taskC(b_res).then((c_res) => {
console.log("C RESULT : ", c_res);
});
});
});
```

⇒ Promise 쓰는 방식을 callback처럼 사용해서 이러한 결과가 나옴.
바뀐 결과 : then chaining이라고 한다.

<br>
<br>

```javascript
taskA(5, 1)
  .then((a_res) => {
    console.log('A RESULT : ', a_res);
    return taskB(a_res);
  })
  .then((b_res) => {
    console.log('B RESULT : ', b_res);
    return taskC(b_res);
  })
  .then((c_res) => {
    console.log('C RESULT : ', c_res);
  });
```

<br>
<br>

## 1.3 Promise의 장점

<br>

```javascript
const bPromiseResult = taskA(5, 1).then((a_res) => {
  console.log('A RESULT : ', a_res);
  return taskB(a_res);
});

console.log('dsadadaddasdsad');
console.log('dsadadaddasdsad');
console.log('dsadadaddasdsad');
console.log('dsadadaddasdsad');
console.log('dsadadaddasdsad');

bPromiseResult
  .then((b_res) => {
    console.log('B RESULT : ', b_res);
    return taskC(b_res);
  })
  .then((c_res) => {
    console.log('C RESULT : ', c_res);
  });
```

<br>
<br>

⇒ 중간에 then chaining 대신 console.log로 다른 코드를 넣어놔도
비동기 코드들이 동기적으로 실행되는 것을 볼 수 있다.

- ⭐ Promise를 쓰면 비동기를 처리하는 코드와 결과가 나오는 코드를 분리하는 것이 가능하다.

- ⭐ 콜백지옥을 피하고, 조금 더 가독성이 좋고 깔끔한 코드를 작성하는 데 도움을 준다.

<br>
<br>

# 2. Async/Await

<br>
<br>

# 🐬 Async/Await과 Promise의 차이

Promise를 활용할 시에는 .catch()문을 통해 에러 핸들링이 가능하지만, async/await은 에러 핸들링을 할 수 있는 기능이 없어 try-catch()문을 활용해야 합니다. 그리고 Promise는 .then 지옥의 가능성이 있는 반면에 async/await을 활용한 코드는 가독성이 좋습니다. async/await은 비동기 코드가 동기코드 처럼 읽히게 해주며 코드 흐름을 이해하기 쉽게 해줍니다.

- 에러 핸들링
  - Promise를 활용할 시에는 .catch()문을 통해 에러핸들링이 가능하지만, async/await은 에러 핸들링을 할 수 있는 기능이 없어 try-catch() 문을 활용
- 코드 가독성
  - Promise의 .then() 지옥의 가능성
  - 코드가 길어지면 길어질수록, async/await를 활용한 코드가 가독성이 좋다.
  - async/await은 비동기코드가 동기 코드처럼 읽히게 해준다. 코드 흐름을 이해하기 쉽다.
