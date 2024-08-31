property는 Object를 선언했을 때의 값이 Property이다.

property_attribute는 Object에서 Property를 선언했을 때 기본적으로 가지고 있는 속성이며 기본적으로 2가지를 가지고 있다.

- 데이터 프로퍼티 : 키와 값으로 형성된 실질적 값을 가지고 있는 프로퍼티
- 엑세서 프로퍼티 : 자체적으로 값을 갖고 있지 않지만 다른 값을 가져오거나 설정할 때 호출되는
                                  함수로 구성된 프로퍼티(getter, setter)

```jsx
const jiMin = {
    name : '지민',
    year : 1995,
};

console.log(Object.getOwnPropertyDescriptor(jiMin, 'name'));
console.log(Object.getOwnPropertyDescriptor(jiMin, 'year'));
```

```jsx
{ value: '지민', writable: true, enumerable: true, configurable: true }
{ value: 1995, writable: true, enumerable: true, configurable: true }
```

```jsx
const jiMin = {
    name : '지민',
    year : 1995,
};

console.log(Object.getOwnPropertyDescriptor(jiMin, 'name'));
console.log(Object.getOwnPropertyDescriptor(jiMin, 'year'));
console.log();
console.log(Object.getOwnPropertyDescriptors(jiMin));
```

```jsx
{ value: '지민', writable: true, enumerable: true, configurable: true }
{ value: 1995, writable: true, enumerable: true, configurable: true }

{
  name: { value: '지민', writable: true, enumerable: true, configurable: true },
  year: { value: 1995, writable: true, enumerable: true, configurable: true }
}
```

value : property의 값

writable : 값을 수정할 수 있는 여부. false로 설정하면 프로퍼티 값을 수정 할 수 없다.

enumerable : 열거가 가능한지 여부. for…in 루프 등을 사용 할 수 있으면 true를 반환한다.

configurable : 
property_attribute의 재정의가 가능한지 여부를 판단한다.
false인 경우 property 삭제나 attribute 변경이 금지된다. 단, writable이 true인 경우 값 변경과
writable을 변경하는 것은  가능하다.

```jsx
const jiMin = {
    // 데이터 프로퍼티
    name : '지민',
    year : 1995,

    // 엑세스 프로퍼티
    get age(){
        return new Date().getFullYear() - this.year;
    },

    set age(age){
        this.year = new Date().getFullYear() - age;
    }
};

console.log(jiMin);
console.log('jiMin.age = ',jiMin.age);

```

```jsx
{ name: '지민', year: 1995, age: [Getter/Setter] }
jiMin.age =  29
```

```jsx
const jiMin = {
    // 데이터 프로퍼티
    name : '지민',
    year : 1995,

    // 엑세스 프로퍼티
    get age(){
        return new Date().getFullYear() - this.year;
    },

    set age(age){
        this.year = new Date().getFullYear() - age;
    }
};

console.log('<데이터 프로퍼티>');
console.log(jiMin);
console.log('jiMin.age = ',jiMin.age);
console.log('jiMin.year = ',jiMin.year);

console.log();

console.log('<엑세스 프로퍼티>');
console.log(Object.getOwnPropertyDescriptor(jiMin, 'age'));
```

```jsx
<데이터 프로퍼티>
{ name: '지민', year: 1995, age: [Getter/Setter] }
jiMin.age =  29
jiMin.year =  1995

<엑세스 프로퍼티>
{
  get: [Function: get age],
  set: [Function: set age],
  enumerable: true,
  configurable: true
}
```

엑세스 프로퍼티는 value라는  property attribute가 존재하지 않고 getter, setter property attribute가 존재한다. 

## Property Attribute재정의

```jsx
const jiMin = {
    // 데이터 프로퍼티
    name : '지민',
    year : 1995,

    // 엑세스 프로퍼티
    get age(){
        return new Date().getFullYear() - this.year;
    },

    set age(age){
        this.year = new Date().getFullYear() - age;
    }
};

//키값 추가
jiMin.height = 172;
jiMin['weight'] = 60;

console.log(jiMin);
console.log(Object.getOwnPropertyDescriptor(jiMin, 'height' ));
```

```jsx
{
  name: '지민',
  year: 1995,
  age: [Getter/Setter],
  height: 172,
  weight: 60
}
{ value: 172, writable: true, enumerable: true, configurable: true }
```

기본적으로 키 값을 추가하여 property attribure를 출력하면 위와 같다.

```jsx
const jiMin = {
    // 데이터 프로퍼티
    name : '지민',
    year : 1995,

    // 엑세스 프로퍼티
    get age(){
        return new Date().getFullYear() - this.year;
    },

    set age(age){
        this.year = new Date().getFullYear() - age;
    }
};

Object.defineProperty(jiMin, 'height', {
    value: 172,
    writable: true,
    enumerable: true,
    configurable: true,
});

console.log(jiMin);
console.log(Object.getOwnPropertyDescriptor(jiMin, 'height'));
```

```jsx
{ name: '지민', year: 1995, age: [Getter/Setter], height: 172 }
{ value: 172, writable: true, enumerable: true, configurable: true }
```

Object.defineProperty메소드를 사용하여 property attribute를 직접적으로 정의할 수 있다. 

```jsx
const jiMin = {
    // 데이터 프로퍼티
    name : '지민',
    year : 1995,

    // 엑세스 프로퍼티
    get age(){
        return new Date().getFullYear() - this.year;
    },

    set age(age){
        this.year = new Date().getFullYear() - age;
    }
};

Object.defineProperty(jiMin, 'height', {
    value: 172,
    writable: false,
    enumerable: false,
    configurable: false,
});

console.log(jiMin);
console.log(Object.getOwnPropertyDescriptor(jiMin, 'height'));
```

```jsx
{ name: '지민', year: 1995, age: [Getter/Setter] }
{ value: 172, writable: false, enumerable: false, configurable: false }
```

Object.defineProperty메소드를 사용하면 jiMin의 property attribute를 재정의 할 수 있다. 

```jsx
const jiMin = {
    // 데이터 프로퍼티
    name : '지민',
    year : 1995,

    // 엑세스 프로퍼티
    get age(){
        return new Date().getFullYear() - this.year;
    },

    set age(age){
        this.year = new Date().getFullYear() - age;
    }
};

Object.defineProperty(jiMin, 'height', {
    value: 172,
    // writable: true,
    // enumerable: true,
    // configurable: true,
});

console.log(jiMin);
console.log(Object.getOwnPropertyDescriptor(jiMin, 'height'));
```

```jsx
{ name: '지민', year: 1995, age: [Getter/Setter] }
{ value: 172, writable: false, enumerable: false, configurable: false }
```

기본 키 값을 추가하는 형태로 추가하면 property attribute는 모두 true값을 가지게 되는데

만약 property attribute를 선언하지 않으면 기본적으로 false값을 가지게 된다.

### writable

```jsx
const jiMin = {
    // 데이터 프로퍼티
    name : '지민',
    year : 1995,

    // 엑세스 프로퍼티
    get age(){
        return new Date().getFullYear() - this.year;
    },

    set age(age){
        this.year = new Date().getFullYear() - age;
    }
};

Object.defineProperty(jiMin, 'height', {
    value: 172,
    writable: true,
    enumerable: true,
    configurable: true,
});

console.log(jiMin);
console.log(Object.getOwnPropertyDescriptor(jiMin, 'height'));

console.log()

jiMin.height = 180;
console.log(jiMin);

Object.defineProperty(jiMin, 'height', {
    writable: false,
});
console.log(Object.getOwnPropertyDescriptor(jiMin, 'height'));
```

```jsx
{ name: '지민', year: 1995, age: [Getter/Setter], height: 172 }
{ value: 172, writable: true, enumerable: true, configurable: true }

{ name: '지민', year: 1995, age: [Getter/Setter], height: 180 }
{ value: 180, writable: false, enumerable: true, configurable: true }
```

Object.defineProperty을 수정한다면 전에 변경된 값은 그대로 유지되고  Object.defineProperty만 
변경된다.

```jsx
const jiMin = {
    // 데이터 프로퍼티
    name : '지민',
    year : 1995,

    // 엑세스 프로퍼티
    get age(){
        return new Date().getFullYear() - this.year;
    },

    set age(age){
        this.year = new Date().getFullYear() - age;
    }
};

Object.defineProperty(jiMin, 'height', {
    value: 172,
    writable: true,
    enumerable: true,
    configurable: true,
});

console.log(jiMin);
console.log(Object.getOwnPropertyDescriptor(jiMin, 'height'));

console.log()

jiMin.height = 180;
console.log(jiMin);

Object.defineProperty(jiMin, 'height', {
    writable: false,
});
console.log(Object.getOwnPropertyDescriptor(jiMin, 'height'));

console.log('-------------------------------');
jiMin.height = 172;
console.log(jiMin);
```

```jsx
{ name: '지민', year: 1995, age: [Getter/Setter], height: 172 }
{ value: 172, writable: true, enumerable: true, configurable: true }

{ name: '지민', year: 1995, age: [Getter/Setter], height: 180 }
{ value: 180, writable: false, enumerable: true, configurable: true }
-------------------------------
{ name: '지민', year: 1995, age: [Getter/Setter], height: 180 }
```

하지만 writable을 false로 수정한 다음 키 값을 변경하게 되면 에러는 나지 않지만  키 값이 변경되지
않는다.

### enumerable

```jsx
const jiMin = {
    // 데이터 프로퍼티
    name : '지민',
    year : 1995,

    // 엑세스 프로퍼티
    get age(){
        return new Date().getFullYear() - this.year;
    },

    set age(age){
        this.year = new Date().getFullYear() - age;
    }
};

Object.defineProperty(jiMin, 'height', {
    value: 172,
    writable: true,
    enumerable: true,
    configurable: true,
});

console.log(Object.keys(jiMin));
for(let key in jiMin){
    console.log(key);
}

Object.defineProperty(jiMin, 'name', {
    enumerable:false,
});

console.log(Object.getOwnPropertyDescriptor(jiMin, 'name'));
```

```jsx
[ 'name', 'year', 'age', 'height' ]
name
year
age
height
{ value: '지민', writable: true, enumerable: false, configurable: true }
```

```jsx
const jiMin = {
    // 데이터 프로퍼티
    name : '지민',
    year : 1995,

    // 엑세스 프로퍼티
    get age(){
        return new Date().getFullYear() - this.year;
    },

    set age(age){
        this.year = new Date().getFullYear() - age;
    }
};

Object.defineProperty(jiMin, 'height', {
    value: 172,
    writable: true,
    enumerable: true,
    configurable: true,
});

console.log(Object.keys(jiMin));
for(let key in jiMin){
    console.log(key);
}

console.log();

Object.defineProperty(jiMin, 'name', {
    enumerable:false,
});

console.log(Object.getOwnPropertyDescriptor(jiMin, 'name'));
console.log(Object.keys(jiMin));
for(let key in jiMin){
    console.log(key);
}

console.log();
console.log(jiMin.name);
```

```jsx
[ 'name', 'year', 'age', 'height' ]
name
year
age
height

{ value: '지민', writable: true, enumerable: false, configurable: true }
[ 'year', 'age', 'height' ]
year
age
height

지민
```

jiMin.name의 값은 그대로 가지고 있지만 name key의 enumerable값을 false로 변경하게 되면 열거를 할 수 없음으로 name key가 출력 되지 않는다. 

### configurable

```jsx
const jiMin = {
    // 데이터 프로퍼티
    name : '지민',
    year : 1995,

    // 엑세스 프로퍼티
    get age(){
        return new Date().getFullYear() - this.year;
    },

    set age(age){
        this.year = new Date().getFullYear() - age;
    }
};

Object.defineProperty(jiMin, 'height', {
    value: 172,
    writable: true,
    enumerable: true,
    configurable: true,
});

Object.defineProperty(jiMin, 'height', {
    configurable: false,
})
console.log(Object.getOwnPropertyDescriptor(jiMin, 'height'));
```

```
{ value: 172, writable: true, enumerable: true, configurable: false }
```

configurable을 false로 설정

```jsx
const jiMin = {
    // 데이터 프로퍼티
    name : '지민',
    year : 1995,

    // 엑세스 프로퍼티
    get age(){
        return new Date().getFullYear() - this.year;
    },

    set age(age){
        this.year = new Date().getFullYear() - age;
    }
};

Object.defineProperty(jiMin, 'height', {
    value: 172,
    writable: true,
    enumerable: true,
    configurable: true,
});

Object.defineProperty(jiMin, 'height', {
    configurable: false,
})
console.log(Object.getOwnPropertyDescriptor(jiMin, 'height'));

Object.defineProperty(jiMin, 'height', {
    enumerable: false,
})
```

```jsx
bject.defineProperty(jiMin, 'height', {
       ^

TypeError: Cannot redefine property: height
    at Function.defineProperty (<anonymous>)
    at Object.<anonymous> (c:\JavaScript\property_attribute.js:29:8)
    at Module._compile (node:internal/modules/cjs/loader:1368:14)
    at Module._extensions..js (node:internal/modules/cjs/loader:1426:10)
    at Module.load (node:internal/modules/cjs/loader:1205:32)
    at Module._load (node:internal/modules/cjs/loader:1021:12)
    at Function.executeUserEntryPoint [as runMain] (node:internal/modules/run_main:142:12)
    at node:internal/main/run_main_module:28:49
```

configurable을 false로 설정한 후에 enumerable의 값을 변경한다면 에러가 발생한다. 그 이유는 configurable을 false로 설정하였기 때문에 더 이상 enumerable을 포함한 모든 값을 변경할 수 없기
때문이다.

```jsx
const jiMin = {
    // 데이터 프로퍼티
    name : '지민',
    year : 1995,

    // 엑세스 프로퍼티
    get age(){
        return new Date().getFullYear() - this.year;
    },

    set age(age){
        this.year = new Date().getFullYear() - age;
    }
};

Object.defineProperty(jiMin, 'height', {
    value: 172,
    writable: true,
    enumerable: true,
    configurable: true,
});

Object.defineProperty(jiMin, 'height', {
    writable:true,
    configurable: false,
})
console.log(Object.getOwnPropertyDescriptor(jiMin, 'height'));

// Object.defineProperty(jiMin, 'height', {
//     enumerable: false,
// })

Object.defineProperty(jiMin, 'height', {
    value: 180,
})

console.log(Object.getOwnPropertyDescriptor(jiMin, 'height'));
```

```jsx
{ value: 172, writable: true, enumerable: true, configurable: false }
{ value: 180, writable: true, enumerable: true, configurable: false }
```

단 writable이 true일 경우 configurable이 false값이라도 value값은 바꿀 수 있다.

```jsx
const jiMin = {
    // 데이터 프로퍼티
    name : '지민',
    year : 1995,

    // 엑세스 프로퍼티
    get age(){
        return new Date().getFullYear() - this.year;
    },

    set age(age){
        this.year = new Date().getFullYear() - age;
    }
};

Object.defineProperty(jiMin, 'height', {
    value: 172,
    writable: true,
    enumerable: true,
    configurable: true,
});

Object.defineProperty(jiMin, 'height', {
    writable:true,
    configurable: false,
})
console.log(Object.getOwnPropertyDescriptor(jiMin, 'height'));

// Object.defineProperty(jiMin, 'height', {
//     enumerable: false,
// })

Object.defineProperty(jiMin, 'height', {
    value: 180,
})
console.log(Object.getOwnPropertyDescriptor(jiMin, 'height'));

Object.defineProperty(jiMin, 'height', {
    writable:false,
})

console.log(Object.getOwnPropertyDescriptor(jiMin, 'height'));
```

```jsx
{ value: 172, writable: true, enumerable: true, configurable: false }
{ value: 180, writable: true, enumerable: true, configurable: false }
{ value: 180, writable: false, enumerable: true, configurable: false }
```

configurable의 값이 false라도 writable의 property attribute의 값은 변경 가능하다.