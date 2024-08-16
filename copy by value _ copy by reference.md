```jsx
// copy by value 값에 의한 전달
// copy by reference 참조에 의한 전달
// 기본적으로 모든 primitive 값은 copy by value다.
// 객체는 copy by reference이다.
```

```jsx
let original = '안녕하세요';
let clone = original;

console.log(original);
console.log(clone);

clone += ' 안유진 입니다.';
console.log('-------------');
console.log(original);
console.log(clone);
```

```jsx
안녕하세요
안녕하세요
-------------
안녕하세요
안녕하세요 안유진 입니다.
```

위의 코드에서는 clone만 수정하였기 때문에 clone만 변경하여 출력된다.

```jsx
let originalObj = {
    name: '안유진',
    group: '아이브',
};

let cloneObj = originalObj;
console.log(originalObj);
console.log(cloneObj);

console.log('---------------------------');
originalObj['group'] = '코드팩토리';
console.log(originalObj);
console.log(cloneObj);
```

```jsx
{ name: '안유진', group: '아이브' }
{ name: '안유진', group: '아이브' }
-------------------------------------
{ name: '안유진', group: '코드팩토리' }
{ name: '안유진', group: '코드팩토리' }
```

하지만 Object는 cloneObj만 변경하였지만 originalObj값 까지 변경되었다. 그 이유는 Object는 값을 저장할 때 메모리 주소를 저장하며 originalObj를 cloneObj에 저장하였기 때문에 originalObj의 메모리 주소를 cloneObj와 공유하기 때문이다. 

```jsx
let original = '안녕하세요';
let clone = original;

console.log(original);
console.log(clone);

clone += ' 안유진 입니다.';
console.log('---------------------------');
console.log(original);
console.log(clone);
let originalObj = {
    name: '안유진',
    group: '아이브',
};

console.log('---------------------------');
let cloneObj = originalObj;
console.log(originalObj);
console.log(cloneObj);

console.log('---------------------------');
originalObj['group'] = '코드팩토리';
console.log(originalObj);
console.log(cloneObj);

console.log('---------------------------');
console.log(original === clone); // copy by value
console.log(originalObj === cloneObj); // copy by reference
```

```jsx
안녕하세요
안녕하세요
---------------------------
안녕하세요
안녕하세요 안유진 입니다.
---------------------------
{ name: '안유진', group: '아이브' }
{ name: '안유진', group: '아이브' }
---------------------------
{ name: '안유진', group: '코드팩토리' }
{ name: '안유진', group: '코드팩토리' }
---------------------------
false
true
```

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/ea204791-94b0-4594-95e9-37705edf8245/c68ffc62-d7ca-4c43-9e70-a6b19db43e26/image.png)

### Object Spread Operator

```jsx
const yuJin1 = {
    name : '안유진',
    group : '아이브'
}

const yuJin2 = {
    ...yuJin1
}

console.log(yuJin1);
console.log(yuJin2);
console.log(yuJin1 === yuJin2);
```

```jsx
{ name: '안유진', group: '아이브' }
{ name: '안유진', group: '아이브' }
false
```

Spread Operator는 copy by value에 해당한다.

```jsx
const yuJin1 = {
    name : '안유진',
    group : '아이브'
}

const yuJin2 = {
    year : 2024,
    ...yuJin1
}

console.log(yuJin1);
console.log(yuJin2);
console.log(yuJin1 === yuJin2);
```

```jsx
{ name: '안유진', group: '아이브' }
{ year: 2024, name: '안유진', group: '아이브' }
false
```

key, values도 추가가 가능하지만 Spread Operator를 사용할 때는 순서가 중요하다.

```jsx
const yuJin1 = {
    name : '안유진',
    group : '아이브'
}

const yuJin2 = {
    name : '장원영',
    ...yuJin1
}

console.log(yuJin1);
console.log(yuJin2);
console.log(yuJin1 === yuJin2);
```

```jsx
{ name: '안유진', group: '아이브' }
{ name: '안유진', group: '아이브' }
false
```

Spread Operator를 사용하기 전엔 선언을 하면 name이 ‘장원영’으로 바뀌었다가 다시 Spread Operator로 인해서 yujin1이 저장되기 때문에 name이 다시 ‘안유진’으로 변경된다. 

```jsx
const yuJin1 = {
    name : '안유진',
    group : '아이브'
}

const yuJin2 = {
    ...yuJin1,
    name : '장원영',
}

console.log(yuJin1);
console.log(yuJin2);
console.log(yuJin1 === yuJin2);
```

```jsx
{ name: '안유진', group: '아이브' }
{ name: '장원영', group: '아이브' }
false
```

하여 변경을 원한다면 Spread Opertor로 값을 가져온 뒤에 key, values를 설정하여야 한다.