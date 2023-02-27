## 1. for in 문

- 주로 객체에서 사용
- 객체의 `key`를 반복문으로 출력 가능하다.

<br>

```javascript
for (let key in documentObj) {
  console.log(key);
}
```

<br><br>

## 2. for of 문

- 배열, 객체, 유사 배열(String 등)에서 사용
- 객체에서 사용할 때 `value`를 반복문으로 출력 가능하다.

<br>

```javascript
for (let value of documentObj) {
  console.log(value);
}
```
