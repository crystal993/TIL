# unknown은 무엇이고 TypeScript에서 언제 사용해야 할까요?

<br>
<br>

- unknown 은 any의 type-safe한 버전이다.
- unknown으로 선언한 변수에는 모든 type의 값을 할당할 수 있다.

<br>

- ⭐⭐ 하지만 unknown 변수는 unknown, any를 제외한 다른 type의 변수에 할당할 수 없다.
- 먼저 Type Assertion 혹은 Type narrowing으로 범위를 좁히지 않고는 unknown 변수에 대해 작업을 수행할 수 없다. => Type Assertion, Type narrowing은 추후에 다룰 예정

<br>

```typescript
let foo: unknown = 'Akshay';
let bar: string = foo; // Type 'unknown' is not assignable to type 'string'.(2322)
```

<br>

- `typeof` 검사 또는 비교 검사를 수행하거나
- `type guards`를 사용하여 `unknown`의 변수를 특정한 것으로 narrow 할 수 있다.

```typescript
let foo: unknown = 'Akshay';
let bar: string = foo as string;
```
