# void란 무엇이며 언제 void를 사용하나요?

<br><br>

- `void`는 변수에 유형이 없음을 나타낸다.
- `any`와 반대되는 유형으로 작용한다.
- ⭐⭐ 값을 반환하지 않는 함수에서 특히 유용하다.
- 변수 유형이 `void`인 경우 해당변수에 `null` 또는 `undefined`만 할당할 수 있다.

<br>

```typescript
function notify(): void {
  alert('The user has been notifed.');
}
```
