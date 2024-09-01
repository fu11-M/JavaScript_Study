### Extensible(확장이 가능한지 여부를 설정)

```jsx
const jiMin = {
    name: '지민',
    year: 1995,

    get age(){
        return new Date().getFullYear() - this.year;
    },

    set age(age){
        this.year = new Date().getFullYear - age;
    }
}

console.log(jiMin);
console.log();

//Extensible -> 확장이 가능한지 여부를 설정
console.log(Object.isExtensible(jiMin));
jiMin['position'] = 'dance';
console.log(jiMin);

console.log();
Object.preventExtensions(jiMin);
console.log(Object.isExtensible(jiMin));

jiMin['groupName'] = 'BTS';
console.log(jiMin);
```

```jsx
{ name: '지민', year: 1995, age: [Getter/Setter] }

true
{ name: '지민', year: 1995, age: [Getter/Setter], position: 'dance' }

false
{ name: '지민', year: 1995, age: [Getter/Setter], position: 'dance' }
```

isExtensible로 설정하여 확장이 가능한 상태로 jiMin을 출력 하였을 때  position이 확장된 상태로 출력
되지만 preventExtensions로 설정하여 확장이 불가능한 상태로 출력 하였을 때는 groupName이 출력
되지 않는 것을 볼 수 있다.

### Seal(봉인)

```jsx
const jiMin = {
    name: '지민',
    year: 1995,

    get age(){
        return new Date().getFullYear() - this.year;
    },

    set age(age){
        this.year = new Date().getFullYear - age;
    }
}

//Seal -> 객체 봉인
console.log(jiMin);

console.log(Object.isSealed(jiMin)); //봉인이 되어 있냐 안되어 있냐에 따라 기본값은 false이다.
```

```jsx
{ name: '지민', year: 1995, age: [Getter/Setter] }
false
```

```jsx
const jiMin = {
    name: '지민',
    year: 1995,

    get age(){
        return new Date().getFullYear() - this.year;
    },

    set age(age){
        this.year = new Date().getFullYear - age;
    }
}

//Seal -> 객체 봉인
console.log(jiMin);

console.log(Object.isSealed(jiMin)); //봉인이 되어 있냐 안되어 있냐에 따라 기본값은 false이다.

Object.seal(jiMin);

console.log(Object.isSealed(jiMin));
```

```jsx
{ name: '지민', year: 1995, age: [Getter/Setter] }
false
true
```

```jsx
const jiMin = {
    name: '지민',
    year: 1995,

    get age(){
        return new Date().getFullYear() - this.year;
    },

    set age(age){
        this.year = new Date().getFullYear - age;
    }
}

//Seal -> 객체 봉인
console.log(jiMin);

console.log(Object.isSealed(jiMin)); //봉인이 되어 있냐 안되어 있냐에 따라 기본값은 false이다.

Object.seal(jiMin);

console.log(Object.isSealed(jiMin));

jiMin['groupNmae'] = 'BTS';
console.log(jiMin);

delete jiMin['name'];
console.log(jiMin);
```

```jsx
{ name: '지민', year: 1995, age: [Getter/Setter] }
false
true
{ name: '지민', year: 1995, age: [Getter/Setter] }
{ name: '지민', year: 1995, age: [Getter/Setter] }
```

봉인을 한 다음 groupName을 출력해보면 groupName이 추가되지 않고 name이 삭제되지 않은 채로 출력 된 것을 볼 수 있다.

```jsx
const jiMin = {
    name: '지민',
    year: 1995,

    get age(){
        return new Date().getFullYear() - this.year;
    },

    set age(age){
        this.year = new Date().getFullYear - age;
    }
}

//Seal -> 객체 봉인
console.log(jiMin);

console.log(Object.isSealed(jiMin)); //봉인이 되어 있냐 안되어 있냐에 따라 기본값은 false이다.

Object.seal(jiMin);

console.log(Object.isSealed(jiMin));

jiMin['groupNmae'] = 'BTS';
console.log(jiMin);

delete jiMin['name'];
console.log(jiMin);

Object.defineProperty(jiMin, 'name', {
    value: '정국'
});
console.log(Object.getOwnPropertyDescriptor(jiMin, 'name'));
```

```jsx
{ name: '지민', year: 1995, age: [Getter/Setter] }
false
true
{ name: '지민', year: 1995, age: [Getter/Setter] }
{ name: '지민', year: 1995, age: [Getter/Setter] }
{ value: '정국', writable: true, enumerable: true, configurable: false }
```

Seal을 하였을 경우 값이 바뀌지 않아야 하지만 value값을 변경하면 변경되어 진다.

```jsx
const jiMin = {
    name: '지민',
    year: 1995,

    get age(){
        return new Date().getFullYear() - this.year;
    },

    set age(age){
        this.year = new Date().getFullYear - age;
    }
}

//Seal -> 객체 봉인
console.log(jiMin);

console.log(Object.isSealed(jiMin)); //봉인이 되어 있냐 안되어 있냐에 따라 기본값은 false이다.

Object.seal(jiMin);

console.log(Object.isSealed(jiMin));

jiMin['groupNmae'] = 'BTS';
console.log(jiMin);

delete jiMin['name'];
console.log(jiMin);

Object.defineProperty(jiMin, 'name', {
    writable: false,
});
console.log(Object.getOwnPropertyDescriptor(jiMin, 'name'));
```

```jsx
{ name: '지민', year: 1995, age: [Getter/Setter] }
false
true
{ name: '지민', year: 1995, age: [Getter/Setter] }
{ name: '지민', year: 1995, age: [Getter/Setter] }
{ value: '지민', writable: false, enumerable: true, configurable: false }
```

writable도 값이 변경되는 것을 볼 수 있다. 여기서 알 수 있듯이 이전에 property attribute에서 configurable이 false여도 value와 writable의 값은 바꿀 수 있다고 하였다. 즉, Seal을 하는 과정은
configurable이 false가 되는 과정이다.

## Freezed(읽기 외에 모든 기능을 불가능 하게 만든다.)

```jsx
const jiMin = {
    name: '지민',
    year: 1995,

    get age(){
        return new Date().getFullYear() - this.year;
    },

    set age(age){
        this.year = new Date().getFullYear - age;
    }
}

//Freezed(읽기 외에 모든 기능을 불가능하게 만듬)
console.log(Object.isFrozen(jiMin)); // 동결이 되어 있는가? -> 기본값 : false
Object.freeze(jiMin); //동결 설정  
console.log(Object.isFrozen(jiMin)); // 동결이 되어 있어 있는가  -> 동결 후 : true
```

```jsx
false
true
```

```jsx
const jiMin = {
    name: '지민',
    year: 1995,

    get age(){
        return new Date().getFullYear() - this.year;
    },

    set age(age){
        this.year = new Date().getFullYear - age;
    }
}

//Freezed(읽기 외에 모든 기능을 불가능하게 만듬)
console.log(Object.isFrozen(jiMin)); // 동결이 되어 있는가?
Object.freeze(jiMin);
console.log(Object.isFrozen(jiMin));

jiMin['groupNmae'] = 'BTS';
console.log(jiMin);

Object.defineProperty(jiMin, 'name', {
    value: '정국',
})
```

```jsx
false
true
{ name: '지민', year: 1995, age: [Getter/Setter] }
c:\JavaScript\Immutable_object.js:22
Object.defineProperty(jiMin, 'name', {
       ^

TypeError: Cannot redefine property: name
    at Function.defineProperty (<anonymous>)
    at Object.<anonymous> (c:\JavaScript\Immutable_object.js:22:8)
    at Module._compile (node:internal/modules/cjs/loader:1368:14)
    at Module._extensions..js (node:internal/modules/cjs/loader:1426:10)
    at Module.load (node:internal/modules/cjs/loader:1205:32)
    at Module._load (node:internal/modules/cjs/loader:1021:12)
    at Function.executeUserEntryPoint [as runMain] (node:internal/modules/run_main:142:12)
    at node:internal/main/run_main_module:28:49
```

Object.freaaze로 설정하면 값을 변경할 경우 에러가 발생한다.