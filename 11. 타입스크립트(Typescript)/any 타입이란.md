# any 타입이란?

<br>

`any`를 사용하면 모든 유형의 값을 `any` 변수에 할당할 수 있다.

<br><br>

# any 타입은 언제 사용하나요?

1. 변수에 값을 저장하고 싶지만, 그 변수의 type을 미리 알지 못하는 경우가 있다.

```typescript
// third-party API로부터 받은 json
const employeeData: string = `{"name": "John Doe", "salary": 60000}`;

// employee객체를 build하기 위해 json parse
const employee: any = JSON.parse(employeeData);

console.log(employee.name);
console.log(employee.salary);
```

2. 명시적으로 type을 제공하지 않고 컴파일러가 주변 컨텍스트에서 type을 유추할 수 없을 경우 any를 사용한다.
