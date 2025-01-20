# try_catch

```jsx
function runner(){
}try{
    console.log('Hello');
    throw new Error('큰 문제가 생겼습니다.');
    console.log('Code Factory');
}catch(e){
    console.log('---catch---');
    console.log(e);
}

runner();
```

```jsx
Hello
---catch---
Error: 큰 문제가 생겼습니다.
    at Object.<anonymous> (c:\JavaScript\try_catch.js:4:11)
    at Module._compile (node:internal/modules/cjs/loader:1368:14)
    at Module._extensions..js (node:internal/modules/cjs/loader:1426:10)
    at Module.load (node:internal/modules/cjs/loader:1205:32)
    at Module._load (node:internal/modules/cjs/loader:1021:12)
    at Function.executeUserEntryPoint [as runMain] (node:internal/modules/run_main:142:12)
    at node:internal/main/run_main_module:28:49
```

에러가 발생 하면 함수는 에러가 발생하는 시점에서  종료되게 된다.
try_catch문은 try문에서 에러가 발생하면 catch문으로 이동한다. 

```jsx
function runner(){
}try{
    console.log('Hello');
    throw new Error('큰 문제가 생겼습니다.');
    console.log('Code Factory');

}catch(e){
    console.log('---catch---');
    console.log(e);

}finally{
    console.log('---finally---');
}

runner();
```

```jsx
Hello
---catch---
Error: 큰 문제가 생겼습니다.
    at Object.<anonymous> (c:\JavaScript\try_catch.js:4:11)
    at Module._compile (node:internal/modules/cjs/loader:1368:14)
    at Module._extensions..js (node:internal/modules/cjs/loader:1426:10)
    at Module.load (node:internal/modules/cjs/loader:1205:32)
    at Module._load (node:internal/modules/cjs/loader:1021:12)
    at Function.executeUserEntryPoint [as runMain] (node:internal/modules/run_main:142:12)
    at node:internal/main/run_main_module:28:49
---finally---
```

finally문은 어떤 상황이던 반드시 실행된다.