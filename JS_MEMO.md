### node js 확인
    node -v

### node 실행
    node 파일명

### Expression
    표현식은 값을 만들어내기 때문에 함수의 인자로 사용할 수 있다.

### Statement
1. 하나 혹은 여러개의 표현식이 모여 문장을 이룬다.
2. 모든 표현식은 문장이 될 수 있다.
3. 문장의 끝에는 세미콜론을 붙인다.
4. 한 줄에 여러 문장을 적을 경우, 세미 콜론으로 문장을 구분한다.
5. 마지막 문장은 세미 콜론을 붙이지 않아도 문제가 없다.
6. 마지막 문장의 결과가 반환 된다.

### Identifier (식별자)
    코드 내의 변수, 함수, 혹은 속성을 식별하는 문자열
    ex) var name = 'Mark';
        function hello() {}
        var person = {name: 'Mark', age: 37};
    대소문자를 구분한다.

### 변수와 상수
    상수 = const
    변수 = let
        기본적으로 const를 사용하되, 재할당이 필요한 경우에 let을 사용한다.

### 자바스크립트의 this
```this!
```

### scope (변수의 유효 범위)

> Global Scope
>
``` G S

```
> Function Scope
>
``` F S

```
> Block Scope
> 
```B S

```

```
const value = "hello"; // global Scope
function myFnc() {
  console.log("myFnc : ");
  console.log(value); // global Scope 'hello'
}
function otherFnc() {
  console.log("otherFnc : ");
  const value = "bye"; // function Scope
  console.log(value); 'bye'
}
console.log("globval scope : ");
console.log(value); // global Scope  'hello'
```

### Hoisting (호이스팅)
    호이스팅, 아래의 함수를 바로 위에서 호출 할 수 있는 현상 (아래 있는 선언(만)을 끌어 올린다. )
    var는 호이스팅이 발생한다, let과 const는 호이스팅이 발생하지 않는다.

    > 함수먼저
    function hello() {
        console.log('hi');
    }
    hello();
    > 함수의 호출을 먼저 
    hello2();
    function hello2() {
        console.log(hello2);
    }

    > 호이스팅 예제
    age = 6;
    age++;
    console.log(age);
    var age;

    > 호이스팅 예제2
    console.log(name); // undefined
    name = 'Mark';
    console.log(name); // Mark
    var name;
    > 호이스팅 예제2-1
    console.log(name); // undefined
    name = 'Mark';
    console.log(name); // Mark
    var name = '하이';

    > 호이스팅 예제3
    console.log(name); // not defined --> ERROR
    name = 'MARK';
    console.log(name);
    let name;

### 템플릿 스트링 es6
    const a = `${변수} 스트링`;
    -- Symbol 고유한 값
    const a = Symbol();
    const b = Symbol(33);
    const c = Symbol('Mark');
    const d = Symbol('Mark');
    console.log (c==b) // false (typeOf -> Symbol)

### 논리 연산자
    && -> and 
    || -> or
    ! -> not (반대)

### for of // for in
    for of -> iterable (배열 등)
    for in -> 모든 프로퍼티

### arrow function (es 6)
    () => {} 
    const hello1 = () => { console.log("arrow function"); };

    const hello2 = (name) => { console.log(name); };
    const hello2 = name => { console.log(name); }; --> 매개변수가 한개면 괄호 생략 가능

    const hello3 = (name, age) => { console.log(name, age) };

    const hello4 = name => { return `hello4 ${name}` };

    arrow function 에서는 this가 생기지 않는다.
    따라서 arrow function은 생성자로 사용하는것이 불가하다.

### prototype (프로토타입)
    쉽게 생각해서 객체에 내장된 기능이라 이해하면 될 것 같다.

### class (클래스)
    > 선언적 방식
    class A {}
    > class 표현식을 변수에 할당
    const B = class {};
    > 선언적 방식이지만 호이스팅은 일어나지 않는다.
    new C();
    class C {} -> C is not defined

### constructor (생성자)
    class A {
        constructor() {
            console.log("생성자");
        }
    }
    class B {
        constructor(name, age){
            console.log("호출", name, age);
        }
    }
    console.log(new B("덕배",29)); // 호출, 덕배, 29
    console.log(new B()); // 호출, undefinded, undefined

### 멤버변수
    class A {
        constructor(name, age){
            this.name = name;
            this.age = age;
        }
    }
    console.log(new A("덕배", 27)); // A { name : '덕배', age : 27 }

    class B {
        name;
        age;
    } // X

    class C {
        name;
        age;
        constructor(name, age){
            this.name = name;
            this.age = age;
        }
    } // O

### Promise  (ES6)
> 비동기 작업이 맞이할 미래의 완료 또는 실패와 그 결과 값을 나타낸다. (MDN)
> 
```
> 생성자를 통해서 프로미스 객체를 만들 수 있다.
> 생성자의 인자로 executor 라는 함수를 이용한다.
> executor 함수는 resolve 와 reject를 인자로 가진다.
    (resolve, reject) => { ... }
        > resolve와 reject는 함수이다.
            resolve(), reject()
> 생성자를 통해서 프로미스 객체를 만드는 순간 pending (대기) 상태에 돌입한다.
    new Promise((resolve, reject) => {} ); // pending 
> executor 함수 인자 중 하나인 resolve 함수를 실행하면, fulfilled (이행) 상태가 된다.
    new Promise((resolve, reject) => {
        // pending..
        // 비동기....
        resolve(); // fulfilled (이행)
    })
> excutor 함수 인자 중 하나인 reject 함수를 실행하면, rejected (거부) 상태가 된다.
    new Promise((resolve, reject) => {
        reject(); // rejected
    })
> p라는 프로미스 객체는 1000ms 후에 fulfilled 됩니다.
    const p = new Promise((resolve, reject) => {
        /* pending */
        setTimeout(() => {
            resolve();
        }, 1000);
    });
    // resolve 이후에 실행. (위 예시로는 1초 뒤 실행 된다.)
    p.then(( /* callback */) => {
        console.log('1000ms 후에 실행 fulfilled.');
    });
> 프로미스 객체가 rejected 되는 시점에 p.catch 안에 설정한 callback 함수가 실행된다.
    const p = new Promise((resolve, reject) => {
        /* pending */
        setTimeout(() => {
            reject(); /* rejected */
        }, 1000);
    });
    p()
    .then(( /* callback */) => {
        console.log('1000ms 후에 실행 fulfilled.');
    }).catch(() => {
        console.log('1000ms 후에 rejected.')
    });
> executor의 resolve 함수를 실행할 때 인자를 넣어 실행하면, then의 callback 함수의 인자로 받을 수 있다.
    resolve('hello');
    then((nessage) => {...});
> 마찬가지로 executor의 reject 함수를 실행할 때 인자를 넣어 실행하면, catch의 callback 함수의 인자로 받을 수 있다.
    reject('error');
    then((reason) => {...});
    > 보통 reject 함수를 실행하며 rejected 되는 이유를 넘기는데, 표준 내장 객체인 Error의 생성자를 이용하여 Error 객체를 만들어 사용.
        reject(new Error('bad'));
            > Error: bad
                at Timeout._onTimeout (/Users/kimmoonkyung/Desktop/javascript/chap1/promise.js:5:28)
                at listOnTimeout (internal/timers.js:554:17)
                at processTimers (internal/timers.js:497:7)
> fulfilled 되거나 rejected 된 후에 최종적으로 실행할 것이 있다면, .finally()를 설정하고, 함수를 인자로 넣는다.
    .then(() => {...})
    .catch(() => {...})
    .finally(() => {...})
> 보통 비동기 작업을 할 때, callback 함수를 인자로 넣어 로직이 끝나면 callback 함수를 호출한다.
    이런 경우 함수가 아래로 진행되지 않고, callback 함수 안으로 진행 된다.
        function c(callback) {
            setTimeout(() => {
                callback();
            }, 1000);
        }
> then 함수에서 다시 프로미스 객체를 리턴하는 방법을 통해 체이닝하면, 비동기 작업을 순차적으로 아래로 표현할 수 있다.
    then에 함수를 넣는 여러 방법
        function p() {
            return new Promise((resolve, reject) => {
                setTimeout(() => {
                    resolve();
                }, 1000);
            });
        }
        p().then(() => {
            return p();
        })
        .then(() => p())
        .then(p)
        .then(() => {
            console.log('4000ms 후에 실행');
        })
> value 가 프로미스 객체인지 아닌지 알 수 없는 경우, 사용하면 연결 된 then 메소드를 실행한다.
    value 가 프로미스 객체면, resolve 된 then 메소드를 실행한다.
    value 가 프로미스 객체가 아니면, value 를 인자로 보내면서 then 메소드를 실행한다.
        Promise.resolve( /* value */ );
        Promise.resolve(new Promise((resolve, reject) => {
            setTimeout(() => {
                resolve('려1차');
            }, 1000);
        })).then((data) => {
            console.log('프로미스 객체인 경우, resolve 된 결과를 받아 then 이 실행', data);
        });
        Promise.resolve('9ood').then(data => {
            console.log('then 메소드가 없는 경우, fullfilled 된다.', data);
        })
> Promise.reject를 사용하면, catch 로 연결 된 rejected 상태로 변경.
    Promise.reject( /* value */ );
    Promise.reject(new Error('reason'))
        .then(error => {})
        .catch(error => {
            console.log(error);
        });
> 프로미스 객체 여러개를 생성하여, 배열로 만들어 인자로 넣고 Promise.all 을 실행하면, 배열의 모든 프로미스 객체들이 fulfilled 되었을 때, then의 함수가 실행된다.
    then 의 함수의 인자로 프로미스 객체들의 resolve 인자 값을 배열로 돌려준다.
        function p(ms) {
            return new Promise((resolve, reject) => {
                setTimeout(() => {
                    resolve(ms);
                }, ms);
            })
        }
        Promise.all([p(1000), p(2000), p(3000)]).then((messages) => {
            console.log('모두 fulfilled 된 이후에 실행 된다.', messages);
        }); // result -> [1000, 2000, 3000]
> 프로미스 객체 여러개를 생성하여, 배열로 만들어 인자로 넣고 Promise.race 을 실행하면, 프로미스 객체들중 가장 먼저 fulfilled 된 것으로 then의 함수가 실행된다.
    then 의 함수의 인자로 프로미스 객체들의 resolve 인자 값을 배열로 돌려준다.
    Promise.race([프로미스 객체들]);
        function p(ms) {
            return new Promise((resolve, reject) => {
                setTimeout(() => {
                    resolve(ms);
                }, ms);
            })
        }
        Promise.race([p(1000), p(2000), p(3000)]).then((message) => {
            console.log('가장 빠른 하나가 fulfilled 된 이후에 실행된다.', message);
        }); // result -> 1000
``` 
## async function과 await
> async function 선언은 AsyncFunction 객체를 반환 하는 하나의 비동기 함수를 정의한다.

> 비동기 함수는 이벤트 루프를 통해 비동기적으로 작동하는 함수로, 암시적으로 Promise를 사용하여 결과를 반환한다.
 
> 그러나 비동기 함수를 사용하는 코드의 구문과 구조는, 표준 동기 함수를 사용하는 것과 많이 비슷하다. (MDN)
```
> async function 함수이름(){}
> const 함수이름 = async() => {}
> 1. Promise 객체를 리턴하는 함수
    function p(ms) {
        return new Promise((resolve, reject) => {
            setTimeout(() => {
                resolve(ms);
            }, ms);
        })
    }
> 2. Promise 객체를 이용해서 비동기 로직을 수행할 때
    p(1000).then((ms) => {
        console.log(`${ms} ms후에 실행 된다.`);
    });
> 3. Promise 객체를 리턴하는 함수를 await 로 호출하는 방법
    const ms = await p(1000);
    console.log(`${ms} ms후에 실행 된다.`);
> 4. 3번의 과정에서 await는 async function 안에서만 유효 하다는 에러가 발생한다. (전역 공간에서 사용했음)
> 5. await를 사용 하는 경우, 항상 async 함수 안에서 사용 되어야 한다.
    function p(ms) {
        return new Promise((resolve, reject) => {
            setTimeout(() => {
                resolve(ms);
            }, ms);
        })
    }
    async function main() {
        const ms = await p(1000);
        console.log(`${ms} ms후에 실행 된다.`);
    }
    main();
> 6. Promise 객체가 rejected 된 경우의 처리를 위해 try catch 를 이용한다.
    function p(ms) {
        return new Promise((resolve, reject) => {
            setTimeout(() => {
                //resolve(ms);
                reject(new Error('reason'));
            }, ms);
        })
    }
    (async function main() {
        try {
            const ms = await p(1000);
            //
        } catch (error) {
            console.log(error);
        }
    })();
> async function 에서 return 되는 값은 Promise.resolve 함수로 감싸서 리턴된다.
    function p(ms) {
        return new Promise((resolve, reject) => {
            setTimeout(() => {
                //resolve(ms);
                reject(new Error('reason'));
            }, ms);
        })
    }
    async function asyncP() {
        const ms = await p(1000);
        return 'im 9ood';
    }
    (async function main() {
        try {
            const name = await asyncP();
            console.log(name);
        } catch (error) {
            console.log(error);
        }
    })();
```

## axios
```axios

```


## DOMContentLoaded
> 최초 HTML 문서가 완전히 로드 및 파싱되었을때 발생되고, 스타일시트나 이미지 및 서브프레임 로드가 끝나기를 기다리지 않는다.

> load 이벤트는 오직 모든 페이지가 완전히 로드되었을때 사용해야한다. DOMContentLoaded를 쓰는 것이 더 적당한 곳에 load를 사용하는 것은 상당히 일반적인 실수. (MDN)

## localStorage
```
읽기 전용 localStorage 속성은 사용자 로컬의 Storage 객체에 접근하게 해준다.
localStorage는 sessionStorage와 비슷하다.
유일한 차이점은 localStorage에 저장 된 데이터는 만료기간이 없지만, 
sessionStorage에 저장된 데이터는 세션이 끝나면(브라우저 종료) 지워 진다는 것.
모든 key 와 value 는 항상 string 으로 저장 된다. (object와 integer 들은 string으로 자동 변환) (MDN)
    > 크롬 개발자 도구 -> Application  -> Storage -> Local Storage -> url -> Key -> token -> Value -> localStorage.getItem();
```

## 비구조 할당 (es6) === 객체 구조 분해
```
const functionName = (parameter) => { retrun `${parameter.value} ${parameter.value1} ${parameter.value2}` };
    > const functionName = (parameter) => { 
   /* const functionName = ({parameter}) => { 로도 사용 가능하다. */
                                            const { value, value1, value2 } = parameter; 
                                            return `${value} ${value1}`;
                                        }
```
```
const { key } = parameter;
    > EX) const dog = { name:'승래', age:28 } 을
        const { name } = dog;
        console.log(name); // 승래
        로도 사용이 가능 하다.
```
```
    > 다른 예제 (btn 클릭)
    const number = document.getElementById("number");
    // const increase = document.getElementById("increase");
    // const decrease = document.getElementById("decrease");
    // 를 비구조화 하여
    const buttons = document.querySelectorAll("button");
    const [increase, decrease] = buttons;
    // 로 사용 할 수도 있다.
    console.log(buttos);
        > NodeList {0: HTMLButtonElement, 1: HTMLButtonElement, entries: ƒ entries(), keys: ƒ keys(), values: ƒ values()…}
    increase.onclick = () => { 
        const current = parseInt(number.innerText, 10);
        number.innerText = current + 1;
    };
    decrease.onclick = () => {
        const current = parseInt(number.innerText, 10);
    n   umber.innerText = current - 1;
    };
```


--------------------------------------------
### promise! (vlpt)
 
> 비동기 작업을 좀 더 편하게 사용할 수 있도록 es6 에 도입 된 것.

#### 기본 사용법
```
const myPromise = new Promise((resolve, reject) => { ... })
    > resolve 는 성공시 호출, reject 는 실패시 호출
```
```
> 예제
function sleep(ms) {
    return new Promise((resolve) => setTimeout(resolve, ms));
}


const getDog = async () => {
    await sleep(1000);
    return "짐승내";
};

const getBeast = async () => {
    await sleep(3000);
    return "짐승균";
};

async function process() {
    // const dog = await getDog();
    // console.log(dog);
    // const beast = await getBeast();
    // console.log(beast);
    // 를 한 번에 처리하기

    // const results = await Promise.all([getDog(), getBeast()]);
    // const dog = results[0];
    // const beast = results[1];
    // 를 비구조화 할당
    // const [dog, beast] = await Promise.all([getDog(), getBeast()]);
    // console.log(dog);
    // console.log(beast);

    // race
    // const first = await Promise.race([getDog(), getBeast()]);
    // console.log(first); // 짐승내
}
```

# 배열 내장 함수
```
const obj = [
    {
        id : 1,
        name : '승레',
        done : true
    },
    {
        id : 2,
        name : '짐승래',
        done : false
    }
]
```
## 배열 내장 함수 map
    사용법 > 배열.map((요소, 인덱스, 배열) => { return 요소 });
```
const mapTest = obj.map(item => item.name);
console.log(mapTest);
// ['승래', '짐승래'];
```

## 배열 내장 함수 filter
    const filterTest = obj.filter(item => !item.done);
    console.log(filterTest);
    // (1) [Object]
        > 새로운 배열을 만들어낸다.

## 배열 내장 함수 find (findIndex)
    const findTest = obj.find(item => item.id === 2);
    console.log(findTest); 
        // {id: 2, name: "짐승래", done: false}

    const findTest2 = obj.find(item => item.id !== 2);
    console.log(findTest2); 
        // {id: 1, name: "승레", done: true}

    const findTest3 = obj.find(item => !item.done);
    console.log(findTest3);
        // {id: 2, name: "짐승래", done: false}

    const findIndexTest = obj.findIndex(item => item.id === 2);
    console.log(findIndexTest);
        // 1

## 배열 내장 함수 splice / slice
    const arr = [1,2,3,4,5];
        const spliced = arr.splice(2, 1);
            > console.log(spliced); // [3]
            > console.log(arr); // [1,2,4,5]
        const sliced = arr.slice(3, 5);
            > console.log(slice) // [4,5]
            > console.log(arr) // [1,2,3,4,5]
> splice -> 기존의 배열을 건듬, arr.splice(자를 인덱스, 자를 인덱스 부터 몇개)

> slice -> 기존의 배열을 건들지 않음, arr.slice(자를 인덱스, 기존 인덱스부터 몇개)


## 배열 내장 함수 shift / pop / unshift / push (모두 기존의 배열을 건듬)
> shift는 맨 앞에서 원소를 배열에서 추출한다. (기존의 배열을 수정한다.)
> 
    const numbers = [10, 20, 30, 40];
    const value = numbers.shift();
    console.log(value);
        // [10]
    console.log(numbers);
        // [20, 30, 40]
> 이 상태에서 shift() 를 또 해주면 수정된 배열의 첫번째가 추출 되고 numbers의 결과는 [30, 40] 이 된다. (그리고 호이스팅이 일어나는것 같다.)


### pop은 맨 뒤에서 추출한다. (기존의 배열 수정).
```
```
### unshift는 맨 앞 부분에 배열을 추가한다.
    numbers.unshift(50);
    console.log(numbers);
        // [50, 10, 20, 30, 40];

### push는 맨 뒤에 배열을 추가한다.
```
```
##  배열 내장 함수 concat (기존의 배열을 건들지 않음)
> concat은 배열을 합친다.
> 
    const arr1 = [1,2,3];
    const arr2 = [4,5,6];
    const concated = arr1.concat(arr2);
    console.log(concated);
        // [1,2,3,4,5,6]
        > ES6 연산자 스프레드
            > const concated = [...arr1, ...arr2];
                > 동일한 결과

### 배열 내장 함수 join
> 배열의 내용물을 문자열 형태로 합칠 때 사용 한다.
> 
    const arr = [1,2,3,4,5,6];
    console.log(arr.join());
        // 1,2,3,4,5,6
    console.log(arr.join(' '));
        // 1 2 3 4 5 6

## 배열 내장 함수 reduce
> 참고) https://www.zerocho.com/category/JavaScript/post/5acafb05f24445001b8d796d

> 사용법 > 배열.reduce((누적값, 현잿값, 인덱스, 요소) => { return 결과 }, 초깃값);

    const numbers = [10, 20, 30, 40];
    let sum = 0;
    numbers.forEach(n => {
    sum += n;
    });
    console.log(sum);
        // 100
    const reduceSum = numbers.reduce((accumulator, current) => accumulator + current, 0);
    console.log(reduceSum);
        // 100

평균 구하기
```
const reduceAvg = numbers.reduce((accumulator, current, idx, arr) => {
if (idx === arr.length - 1) {
    // 인덱스는 0 부터고 위의 예제로는 배열의 길이가 4까지 있기 때문에 -1 해준다.
    return (accumulator + current) / arr.length;
}
return accumulator + current;
}, 0);
console.log(reduceAvg);
    // 25
```
> reduce 다른 예제

    const alphabets = ["a", "a", "a", "b", "c", "c", "d", "e"];
    const counts = alphabets.reduce((acc, cur) => {
    if(acc[cur]){
        acc[cur] += 1;
    } else {
        acc[cur] = 1;
    }
    return acc;
    }, {});
    console.log(counts);
    //{a: 3, b: 1, c: 2, d: 1, e: 1}
  
#### 배열 문제
> 숫자 배열이 주어졌을 때 10보다 큰 숫자의 갯수를 반환하는 함수를 만드세요.
> 
1. filter 활용
```
function constBiggerThanTen(numbers) {
    const result = numbers.filter(item => item > 10);
    return result.length;
    >> return numbers.filter((item) => item > 10).length; 로 줄일 수 있다.
}
const count = constBiggerThanTen([1, 2, 3, 5, 10, 20, 30, 40, 50, 60]);
    console.log(count); // 5
```
2. map 활용
```
function constBiggerThanTen(numbers) {
    let count = 0;
    numbers.map((item) => {
        if (item > 10) {count++;}
    });
    return count;
}
const count = constBiggerThanTen([1, 2, 3, 5, 10, 20, 30, 40, 50, 60]);
    console.log(count); // 5
```
3. reduce 활용
```
function countBiggerThanTen(numbers) {
    return numbers.reduce((acc, current) => {
        if (current > 10) {
            return acc + 1;
        } else {
            return acc;
        }
    }, 0);
}
```

### 객체, 생성자, 프로토타입
```
function Beast(type, name, sound) {
  this.type = type;
  this.name = name;
  this.sound = sound;
  // this.say = function () {
  //   console.log(this.sound);
  // };
}

Beast.prototype.say = function () {
  console.log(this.sound);
};
```

### 생성자
```
function Dog(type, name, sound) {
  Beast.call(this, type, name, sound);
}
Dog.prototype.say = Beast.prototype.say;

const dog = new Dog("짐승", "승내", "닥쳐!!!");
console.log(dog); 
//Dog {type: "짐승", name: "승내", sound: "닥쳐!!!", say: ƒ (), constructor: Object}

dog.say();
````

### 클래스 문법 (ES6)
> 자바와 비슷하다.
```
class Beast {
  constructor(type, name, sound) {
    this.type = type;
    this.name = name;
    this.sound = sound;
  }

  say() {
    console.log(this.sound);
  }
}
//console.log(Beast.prototype.say);

class Dog extends Beast {
  constructor(name, sound) {
    super("짐승", name, sound);
    // 상속 받은 클래스의 생성자를 호출한다.
  }
}

const dog = new Dog("숭내", "닥쳐!!!!");
dog.say();
------ 연습
class Food {
  constructor(name) {
    this.name = name;
    this.brands = [];
  }

  addBrand(brand) {
    this.brands.push(brand);
  }

  print() {
    console.log(`${this.name}을(를) 파는 음식점들: `);
    console.log(this.brands.join(", "));
  }
}

const pizza = new Food("핏짜");
pizza.addBrand("휫자스꾸");
pizza.addBrand("피자스쿨");

const chicken = new Food("치킨");
chicken.addBrand("BHC");

pizza.print();
// 핏짜을(를) 파는 음식점들:
// 휫자스꾸, 피자스쿨
chicken.print();
// 치킨을(를) 파는 음식점들:
// BHC
```


### Truthy, Falsy
    Falsy 한 값
    !undefined / !null / !0 / !'' / !NaN / !false
    > true
    를 제외한 값들은 Truthy 한 값이다.
    
    ex)
    !3 / !'hello' / !['arr'] / ![] / !{}
    > false

### 단축 평가 논리 계산법
    > &&
    true && 'hello' // hello
    false && 'hi' // false

    true면 우측 값이 return
    falsy한 값은 좌측 값이 return 된다.
        > ||
    true || 'helo' // true 
    false || 'good' // good 

    truthy면 좌측 값이 return 되고
    falsy한 값은 우측 값이 return.

    > 조건문 등 리팩토링 시 유용하게 사용할 수 있을 것 같다.

### 함수의 기본 파라미터
    파라미터에 = 을 사용하여 기본 값을 넣어 줄 수 있다.
    ex) function exam (a = 1){ ... }

### includes
    array.includes(text);
        > array에 text 가 존재하면 true, 아니면 false를 리턴.

### 스프레드 spread
    const people = {
    name: "승래"
    };
    const beastPeople = {
    ...people,
    // name: "승래"
    attribute: "짐승"
    };
    const gayPeople = {
    ...beastPeople,
    // name: "승래"
    attribute: "게이"
    };
> ... 연산자는 객체의 속성을 복붙한다.

### 레스트 rest
    const people = {
    name: "승래",
    attribute: "짐승",
    color: "purple"
    };
    const { attribute, ...rest } = people;
    console.log(attribute); // 짐승
    console.log(rest); // {name: "승래", color: "purple"}}
> spread는 퍼뜨려주고, rest는 모아준다.
```
// function sum(a, b, c, d, e, f, g) {
//   return a+b+c;
// }
// 이런코드를
function sum(...rest) {
  return rest.reduce((acc, cur) => acc + cur, 0);
}
console.log(sum(1,2,3,4,5));
// 이렇게 
  // sum(...array); 로도 사용이 가능하다.
```
```
// 함수에 n개의숫자들이 파라미터로 주어졌을 때, 그 중 가장 큰 값을 알아내자.
    > forEach
function max(...rest) {
  let maxCnt = 0;
  rest.forEach((num) => {
    if(num > maxCnt){ maxCnt = num; }
  });
  return maxCnt;
}
const result = max(1, 2, 3, 4, 10, 5, 6, 7);
console.log(result); // 10
```
> reduce 풀이
```
function max(...numbers) {
    return numbers.reduce(
    // acc 이 current 보다 크면 결과값을 current 로 하고
    // 그렇지 않으면 acc 가 결과값
    (acc, current) => (current > acc ? current : acc),numbers[0]
    );
}
```

### 모달 modal 예제
> js
```
    const open = document.getElementById("open");
    const close = document.getElementById("close");
    const modal = document.querySelector(".modal-wrapper");
    open.onclick = () => {
        modal.style.display = "flex";
    };
    close.onclick = () => {
        modal.style.display = "none";
    };
```
> HTML
```
    <button id="open">모달</button>
    <div class="modal-wrapper" style="display: none;">
      <div class="modal">
        <div class="modal-title">짐승내다!</div>
        <p>짐승내와 짐승균은 커플입니다.</p>
        <div class="close-wrapper">
          <button id="close">닫기</button>
        </div>
      </div>
    </div>
```
> css
```
    .modal-wrapper {
        position: fixed;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        background: rgba(0, 0, 0, 0.5);
        display: flex;
        align-items: center;
        justify-content: center;
    }

    .modal {
        background: white;
        padding: 24px 16px;
        border-radius: 4px;
        width: 320px;
    }

    .modal-title {
        font-size: 24px;
        font-weight: bold;
    }

    .close-wrapper {
        text-align: right;
    }
```

#### 기타
```
프로토타입, [for in / for of], this, scope, promise, axios 내용 정리 필, 배열 내장 함수 reduce.. 대충 알아먹었는데 한 번더 공부하자.
```