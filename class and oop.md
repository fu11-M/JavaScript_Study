# class and oop

### 클래스는 객체지향 프로그래밍에서 특정 객체(인스턴스)를 생성하기 위한
변수와 메소드(함수)를 정의하는 일종의 틀이다.

```jsx
class IdolModel{
    name = '안유진';
    year = 2003;
}

const yujin = new IdolModel();
console.log(yujin);
```

```jsx
IdolModel { name: '안유진', year: 2003 }
```

## constructor (생성자)

```jsx
class IdolModel{
    name;
    year;

    constructor(name, year){
        this.name = name;
        this.year = year;
    }
}

const yujin = new IdolModel('안유진', 2003);
const gaeul = new IdolModel('가을', 2002);
const ray = new IdolModel('레이', 2004);
const wonYoung = new IdolModel('장원영', 2004);
const liz = new IdolModel('리즈', 2004);
const eseo = new IdolModel('이서', 2007);

console.log(yujin);
console.log(gaeul);
console.log(ray);
console.log(wonYoung);
console.log(liz);
console.log(eseo);
```

```jsx
IdolModel { name: '안유진', year: 2003 }
IdolModel { name: '가을', year: 2002 }
IdolModel { name: '레이', year: 2004 }
IdolModel { name: '장원영', year: 2004 }
IdolModel { name: '리즈', year: 2004 }
IdolModel { name: '이서', year: 2007 }
```

### method (메소드)

```jsx
class IdolModel{
    //프로퍼티
    name;
    year;

    //생성자
    constructor(name, year){
        this.name = name;
        this.year = year;
    }

    //메서드
    sayName(){
        return `안녕하세요 ${this.name} 입니다.`;
    }
}

const yujin = new IdolModel('안유진', 2003);
const gaeul = new IdolModel('가을', 2002);
const ray = new IdolModel('레이', 2004);
const wonYoung = new IdolModel('장원영', 2004);
const liz = new IdolModel('리즈', 2004);
const eseo = new IdolModel('이서', 2007);

console.log(yujin);
console.log(yujin.sayName());
console.log();

console.log(gaeul);
console.log(gaeul.sayName());
console.log();

console.log(ray);
console.log(ray.sayName());
console.log();

console.log(wonYoung);
console.log(wonYoung.sayName());
console.log();

console.log(liz);
console.log(liz.sayName());
console.log();

console.log(eseo);
console.log(eseo.sayName());
console.log();
```

```jsx
IdolModel { name: '안유진', year: 2003 }
안녕하세요 안유진 입니다.

IdolModel { name: '가을', year: 2002 }
안녕하세요 가을 입니다.

IdolModel { name: '레이', year: 2004 }
안녕하세요 레이 입니다.

IdolModel { name: '장원영', year: 2004 }
안녕하세요 장원영 입니다.

IdolModel { name: '리즈', year: 2004 }
안녕하세요 리즈 입니다.

IdolModel { name: '이서', year: 2007 }
안녕하세요 이서 입니다.
```

```jsx
class IdolModel{
    //프로퍼티
    name;
    year;

    //생성자
    constructor(name, year){
        this.name = name;
        this.year = year;
    }

    //메서드
    sayName(){
        return `안녕하세요 ${this.name} 입니다.`;
    }
}

const yujin = new IdolModel('안유진', 2003);
const gaeul = new IdolModel('가을', 2002);
const ray = new IdolModel('레이', 2004);
const wonYoung = new IdolModel('장원영', 2004);
const liz = new IdolModel('리즈', 2004);
const eseo = new IdolModel('이서', 2007);

console.log(typeof IdolModel);
console.log(typeof yujin);
```

```jsx

function
object
```

## Getter Setter

Getter Setter는 데이터를 가공해서 새로운 데이터를 반환할 때, private한 값을 반환할 때 사용한다. 

```jsx
class IdolModel{
    //프로퍼티
    name;
    year;

    //생성자
    constructor(name, year){
        this.name = name;
        this.year = year;
    }

    //메서드
    sayName(){
        return `안녕하세요 ${this.name} 입니다.`;
    }

    //Getter, Setter
    get nameAndYear(){
        return `${this.name}-${this.year} `;
    }
}

const yujin = new IdolModel('안유진', 2003);
console.log(yujin);
console.log(yujin.nameAndYear);
```

```jsx
IdolModel { name: '안유진', year: 2003 }
안유진-2003 
```

Getter는 함수로 정의하지만 get키워드를 사용하면 키 값처럼 사용할 수 있기 때문에 출력할 때 ( )를 
포함하지 않는다.

```jsx
class IdolModel{
    //프로퍼티
    name;
    year;

    //생성자
    constructor(name, year){
        this.name = name;
        this.year = year;
    }

    //메서드
    sayName(){
        return `안녕하세요 ${this.name} 입니다.`;
    }

    //Getter, Setter
    get nameAndYear(){
        return `${this.name}-${this.year} `;
    }

    set setName(name) {
        this.name = name;
    }
}

const yujin = new IdolModel('안유진', 2003);
console.log(yujin);
console.log(yujin.nameAndYear);

yujin.setName = '장원영';
console.log(yujin);
```

```jsx
IdolModel { name: '안유진', year: 2003 }
안유진-2003 
IdolModel { name: '장원영', year: 2003 }
```

```jsx
class IdolModel{
    //프로퍼티
    #name;
    year;

    //생성자
    constructor(name, year){
        this.#name = name;
        this.year = year;
    }

    //메서드
    sayName(){
        return `안녕하세요 ${this.name} 입니다.`;
    }

    //Getter, Setter
    get name(){
        return this.#name;
    }
}

const yujin = new IdolModel('안유진', 2003);
console.log(yujin);
console.log(yujin.name);

```

```jsx
IdolModel { year: 2003 }
안유진
```

```jsx
class IdolModel{
    //프로퍼티
    #name;
    year;

    //생성자
    constructor(name, year){
        this.#name = name;
        this.year = year;
    }

    //메서드
    sayName(){
        return `안녕하세요 ${this.name} 입니다.`;
    }

    //Getter, Setter
    get name(){
        return this.#name;
    }

    set name(name){
        this.#name = name;
    }
}

const yujin = new IdolModel('안유진', 2003);
console.log(yujin);
console.log(yujin.name);

yujin.name = '코드팩토리'; // set name
console.log(yujin.name); // get name
```

```jsx
IdolModel { year: 2003 }
안유진
코드팩토리
```

## Static Keyword

```jsx
class IdolModel{
    //프로퍼티
    name;
    year;
    static groupName = '아이브';

    //생성자
    constructor(name, year, groupName){
        this.name = name;
        this.year = year;
    }

    static returnGroupName(){
        return '아이브';
    }
}

const yujin = new IdolModel('안유진', 2003);
console.log(yujin);

console.log(IdolModel.groupName);
console.log(IdolModel.returnGroupName());
```

```jsx
IdolModel { name: '안유진', year: 2003 }
아이브
아이브
```

static 키워드는 객체를 생성하지 않고 클래스를 사용해서 데이터를 저장하고 사용할 수 있다.

```jsx
class IdolModel{
    name;
    year;
    
    constructor(name, year){
        this.name = name;
        this.year = year;
    }

    //factory constructor
    static fromObject(Object){
        return new IdolModel(
            Object.name,
            Object.year,
        );
    }
}

const yujin2 = IdolModel.fromObject({
    name : '안유진',
    year : 2003,
});

console.log(yujin2);
```

```jsx
IdolModel { name: '안유진', year: 2003 }
```

static 키워드는 대부분 factory constructor를 구현하기 위해서 사용된다.

```jsx
class IdolModel{
    name;
    year;
    
    constructor(name, year){
        this.name = name;
        this.year = year;
    }

    //factory constructor
    static fromObject(Object){
        return new IdolModel(
            Object.name,
            Object.year,
        );
    }

    static fromList(list){
        return new IdolModel(
           list[0],
           list[1],
        );
    }
}

const yuJin2 = IdolModel.fromObject({
    name: '안유진',
    year: 2003,
});

console.log(yuJin2);

const wonYoung = IdolModel.fromList(
    [
        '장원영',
        2003,
]
);

console.log(wonYoung);
```

```jsx
IdolModel { name: '안유진', year: 2003 }
IdolModel { name: '장원영', year: 2003 }
```

factory constructor를 사용하면 미리 어떤 데이터를 입력 받아서 생성자를 만들지 결정 할 수 있다.