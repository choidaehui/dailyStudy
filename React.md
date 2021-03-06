
# DO it! 리액트 프로그래밍 정석 정리  
      -> 리액트는 화면 출력에 특화된 프레임워크 이다.
      -> 리액트는 컴포넌트(component)라는 작고 독립적인 코드 블록을 조합하여 빠르고 효율적으로 화면을 구성
      -> 자바스크립트에는 제이쿼리, 핸들바라는 라이브러리가 있음
      -> 자바스크립트 라이브러리는 화면의 일부분만 수정되어도 화면 전체를 다시 그려야 함
      -> 노드 패키지 매니저(npm)라는 프로그램으로 자바스크립트 라이브러리를 관리
      -> npm을 개선한 것이 yarn
      -> 웹팩은 프로젝트에 사용된 파일을 분석하여 기존 웹 문서 파일로 변환하는 도구
      -> 웹 브라우저가 해석할 수 없는 .hbs, .cjs, sass 등의 파일을 웹팩이 분석하여 .js, .css 등의 파일로 변환
      -> 노드제이에스는 구글에서 공개한 소프트웨어로 V8엔진을 기반으로 만든 자바스크립트 런타임 도구이다
      -> NVM은 노드제이에스를 설치하거나 관리해주는 프로그램
      
## 리액트 ES6문법 
      1. 템플릿 문자열
        -> 문자열 안에 변수와 연산식을 혼합하여 사용
        -> 작은 따옴표(')대신 백틱(`)으로 문자열을 표현
        -> 특수기호 $를 사용하여 변수 또는 식을 포함
        
``` javascript 
      var string1 = '안녕하세요';
      var string2 = '반갑습니다';
      var greeting = `${string1} ${string2}`;
      var product = { name: '도서', price: '4200원' };
      var message = `제품 ${product.name}의 가격은 ${product.price}입니다.`;
      // $기호를 사용하여 변수를 포함
      var multiLine = `문자열1
      문자열2`;
      // 템플릿 문자열은 엔터를 눌러 줄 바꿈을 허용
      // 이스케이프 시퀀스(\n)를 사용하지 않아도 됨
      var value = 1;
      var value = 2;
      var boolValue = false;
      var operator1 = `곱셈값은 ${value1 * value2}입니다.`;
      var operator2 = `${boolValue ? '참' : '거짓'}입니다.`;
      // $기호를 사용하여 연산을 포함
      
      var cart = { name: '도서', price: '1500원'};
      var getTotal = function(cart) {
        return `${cart.price}원`;
        };
      var myCart = `장바구니에 ${cart.name}가 있습니다. 총 금액은 ${getTotal(cart)}입니다.`;  
```

    2. 전개 연산자
      -> 나열형 자료를 추출하거나 연결할 때 사용
      -> 배열이나, 객체, 함수 인자 표현식([],{},())안에서만 사용 
      -> 배열이나 객체, 변수명 앞에 마침표 세 개(...)를 입력
      
``` javascript 
       var array1 = ['one', 'two'];
       var array2 = ['three', 'four'];
       const combined = [...array1, ...array2];
       // 두 배열 항목을 전개 연산자로 합함
       // 결과: combined = ['one', 'two', 'three', 'four'];
       const [first, second, three = 'empty', ...others] = array1;
       // 결과: first = 'one', second = 'two', three = 'empty', others = []
       // 올바르지 못한 예
       // var wrongArr = ...array1;
       // 전개 연산자를 배열 표현식 없이 사용한 잘못된 예
       
       function func(...args) { var[first, ...others] = args; }
       // 함수 인자 배열을 args변수에 할당
       
       var objectOne = { one: 1, two: 2, other: 0 };
       var objectTwo = { three: 3, four: 4, other: -1 };
       var combined = {
         one: objectOne.one,
         two: objectOne.two,
         three: objectTwo.three,
         four: objectTwo.four,
         };
         //키에 해당하는 값을 추출
         
       var combined = Object.assign({}, objectOne, objectTwo);
       // 결과: combined = { one: 1, two: 2, three: 3, four: 4, other: -1 }
       // 객체 내장 함수 assign()을 사용하여 두 객체를 병합
       // assign()의 첫 번째 인자는 결과로 반환할 객체({}), 나머지 인자는 병합할 객체임
       // 병합할 객체는 앞에 있는 객체부터 덮어 씀
       
       var combined = Object.assign({}, objectTwo, objectOne);
       // 결과: combined = { one: 1, two: 2, three: 3, four: 4, other: 0 }
       // 중복되는 키값이 있으면 이후에 전달된 객체(objectOne)의 값으로 덮어 씀
       
       var others = Object.assign({}, combined);
       delete others.other;
       // 결과: others = { one: 1, two: 2, three: 3, four: 4 }
       
    =  var objectOne = { one: 1, two: 2, other: 0 };
       var objectTwo = { three: 3, four: 4, other: -1 };
       var combined = {
         ...objectOne,
         ...objectTwo,
         };
       // 결과: combined = { one: 1, two: 2, three: 3, four: 4, other: -1 }
       
       var combined = { 
         ...objectTwo,
         ...objectOne,
         };
       // 결과: combined = { one: 1, two: 2, three: 3, four: 4, other: 0 } 
       
       var { other, ...others } = combined;
       // 결과: others = { one: 1, two:2, three: 3, four: 4 }
       // 객체에서 특정 값을 추출할 때는 추출하려는 키 이름(other)을 맞추고, 나머지는 전개 연산자로 선언된 변수(others)에 할당 함       
```
    3. 가변 변수와 불변 변수
      -> let은 값을 수정할 수 있는 가변 변수
      -> const은 값을 수정할 수 없는 불변 변수
      -> 불변 변수는 값을 다시 할당할 수 없는 것이지 값을 변경할 수 있음
      
``` javascript 
        const arr2 = [];
        arr2.push(1);
        // 결과: arr2 = [1]
        arr2.splice(0, 0, 0);
        // 결과: arr2 = [0. 1]
        arr2.pop();
        // 결과: arr2 = [1]
        const obj2 = {};
        obj2['name'] = '내이름'; 
        // 결과: obj2 = { name: '내이름' }
        Object.assign(obj2, { name: '새이름' });
        // 결과: obj2 = { name: '새이름' }
        delete obj2.name;
        // obj2 = {}
        // 불변 변수에 새값을 할당하는 방법으로 새로 정의하여 무결성 
        
        const num1 = 1;
        const num2 = num1 * 3;
        // num2 = 3
        const str1 = '문자';
        const str2 = str1 + '추가';
        // str2 = '문자추가'
        const arr3 = [];
        const arr4 = arr3.concat(1);
        // arr4 = [1]
        const arr5 = [...arr4, 2, 3];
        // arr5 = [1, 2, 3]
        const arr6 = arr5.slice(0, 1);
        // arr6 =[1], arr5 = [1, 2, 3]
        const [first, ...arr7] = arr5;
        // arr7 = [2, 3], first = 1
        const obj3 = { name: '내이름', age: 20 };
        const objValue = { name: '새이름', age: obj3.age };
        const obj4 = {...obj3, name: '새이름' };
        // obj4 = { name: '새이름', age: 20 }
        const { name, ...obj5 } = obj4;
        // obj5 = { age: 20 }
```
    4. 클래스
``` javascript
       function Shape (x, y) {
         this.name = 'Shape';
         this.move(x, y);
         }
         // static 함수를 선언
       Shape.create = function(x, y) { return new Shape(x, y); };
        // 인스턴스 함수를 선언
        
       Shape.prototype.move = function(x, y) {
         this.x = x;
         this.y = y;
         }
       Shape.prototype.area = function() {
         return 0;
         };
     = Shape.prototype = {
         move: function(x, y) {
           this.x = x;
           this.y = y;
           },
         area: function() {
           return 0;
           }
         };
         
       var s = new Shape(0, 0);
       s.area();
       // 0
       
       function Circle(x, y, radius) {
         Shape.call(this, x, y);
         this.name = 'Circle';
         this.radius = radius;
         }
       Object.assign(Circle.prototype, Shape.prototype, {
         area: function() {
           return this.radius * this.radius;
         }
       });
       var c = new Circle(0, 0, 10);
       c.area();
       //100
       
       // 앞의 코드를 ES6 클래스 표현식으로 변환
       class Shape {
         static create(x, y) { return new Shape(x, y); }
         name = 'Shape'; // this.name = 'Shape';
         constructor (x, y) {
           this.move(x, y);
           }
         move(x, y) {
           this.x = x;
           this.y = y;
           }
         area() {
           return 0
           }
         }
         var s = new Shape(0, 0);
         s.area(); 
         //0
         // 생성자, 클래스 변수, 클래스 함수 정의에는 변수 선언을 위한 키워드(var, let, const,...)를 사용하지 않음
         
         class Circle extends Shape {
           constructor(x, y, radius) {
             super(x, y);
             this.radius = radius;
             }
             area() {
               if (this.radius === 0) return super.area();
               return this.radius * this.radius;
               }
             }
           var c = new Circle(0, 0, 10);
           c.area();
           //100      
``` 
    5. 화살표 함수
    -> 화살표 기호 =>로 함수 선언
    
``` javascript 
        var add = function(first, second) {
          return first + second;
          };
        
        // 화살표 함수 사용하여 표현
        var add = (first, second) => {
          return first + second;
          };
        var add = (first, second) => first + second;
        
        var addAndMultiple = (first, second) => ({ add: first + second, multiply: first * second });
        //반환값이 객체라면 괄호로 결과값을 감싸 간결하게 표현
        
        function addNumber(num) {
          return function(value) {
            return num + value;
            };
          }
        var addNumber = num => value => num + value;
        
        class Myclass {
          value = 10;
          constructor() {
            var addThis2 = function(first, second) {
              return this.value + first + second;
              }.bind(this);
          = var addThis3 = (first, second) => this.value + first + second;
          }
        }
        // 화살표 함수는 콜백 함수의 this 범위로 생기는 오류를 피하기 위해 bind() 함수를 사용하여 this객체를 전달
        // addThis2() 함수는 this를 bind() 함수에 전달하여 this의 범위를 유지
        // addThis3() 함수의 경우 화살표 함수이므로 이 과정이 생략 됨      
``` 
    6. 객체 확장 표현식과 구조 분해 할당
``` javascript 
       var x = 0;
       var y = 0;
       var obj = { x: x, y: y };
       var randomKeyString = 'other';
       var combined = {};
       combined['one' + randomKeyString] = 'some value';
       // 연산 결과로 키값을 대입할 때는 키값을 지정할 코드를 추가로 작성
       var obj2 = {
         x: x,
         methodA: function() { console.log('method A'); },
         methodB: function() { return 0; },
       };
       //객체에 함수를 추가할 때는 변수에 함수를 할당
        
    =  var x = 0;
       var y = 0;
       var obj = { x, y};
       // 키값을 생략하면 자동으로 키의 이름으로 키값을 지정
       var randomKeyString = 'other';
       var combined = {
         ['one' + randomKeyString]: 'some value',
         };
         // 추가하여 계산된 키값을 생성
       var obj2 = {
         x,
         methodA() { console.log('method A');},
         methodB() { return 0; },
         };
         
       var list = [0, 1];
       var [
         item1,
         item2,
         item3 = -1,
         ] = list;
       // var item1 = list[0];
       // var item2 = list[1];
       // var item3 = list[2] || -1;
       var temp = item2;
       item2 = item1;
       item1 = temp;
       // [item2, item1] = [item2, item2];
       var obj = {
         key1: 'one',
         key2: 'two',
         };
       var {
         key1: newKey1,
         key2,
         key3 = 'default key3 value',
         } = obj;
       // var key1 = 'one';
       // var key2 = 'two';
       // var key3 = obj.key3 || 'default key3 value';
       // var newKey1 = 'one';
       
       var [item1, ...otherItems] = [0, 1, 2];
       // otherItems = [1, 2]
       var {key1, ...others} = { key1: 'one', key2: 'two' };
       // others = { key2: 'two' }         
```
    7. 라이브러리 의존성 관리
``` javascript 
       import MyModule from './MyModule.js';
       // import 구문을 사용해 지정된 파일(MyModule.js)의 기본(default)으로 공유하는 모듈을 불러옴
       import { ModuleName } from './MyModule.js';
       // 이름을 맞춰 모듈 안의 특정 함수 혹은 변수를 참조
       import { ModuleName as RenamedModuleName } from './MyModule.js';
       // 특정 모듈을 가져올 때 이름이 충돌할 경우 다른 이름으로 변경하여 불러올 수 있음
       function Func() {
         MyModule();
         }
       export const CONST_VALUE = 0;
       export class MyClass {}
       // 변수나 클래스의 이름을 다른 파일에서 따로 참조할 수 있도록 정의
       export default new Func();
       // 현재 파일이 다른 파일에서 기본(default)으로 참조하게 되는 항목을 정의       
```  
    8. 배열함수
      ㄱ. forEach()함수
``` javascript 
      function parse(qs) {
       var queryString = qs.substr(1);
       // 쿼리 스트링(Query String)은 '웹 주소에 포함시키는 문자열'을 의미
       // queryString = 'banana=10&apple=20&orange=30'
       // substr(start, length) 함수는 파라미터로 입력받은 start index부터 length 길이만큼 string을 잘라내어 반환함
       // 첫 번째 글자의 index는 0에서 시작
       var chunks = qs.split('&');
       var result = {};
       for(var i = 0; i < chunks.length; i++) {
         var parts = chunks[i].split('=');
         // i = 0일 때
         var key = parts[0];
         // key = 'banana'
         var value = parts[1];
         // value = '10'
         result[key] = value;
         // result = {banana: '10'}
         }
         return result;
         // result = {banana: '10', apple: '20', orange: '30'} 각 요소 값들이 순환해서 리턴 됨
       }
       // var value = Number.isNaN(Number(parts[1])) ? parts[1] : Number(parts[1]);
       // result[key] = value;
       // result = {banana: 10}
       // 10을 문자열이 아닌 숫자로 변환
       
       설명) forEach()함수는 세 개의 인수(요소 값, 요소 인덱스, 순회 중인 배열)를 가진다.
             const array1 = ['a', 'b', 'c'];
             array1.forEach(element => console.log(element));
             // "a"
             // "b"
             // "c"
             
             for 반복문을 forEach()로 바꾸기
             const items = ['item1', 'item2', 'item3'];
             const copy = [];
             
             for(let i = 0; i < items.length; i++) {
               copy.push(items[i]);
               }
          =  items.forEach(function(item) {
               copy.push(item);
               });
         
        사용 예) 
             chunks.forEach((chunk) => {
               const parts = chunk.split('=');
               // 처음 요소 값부터 진행
               // chunk = 'banana=10', parts = ['banana', '10']
               const key = parts[0];
               // key = 'banana'
               const value = Number.isNaN(Number(parts[1])) ? parts[1] : Number(parts[1]);
               // value = 10
               result[key] = value
               // result = { banana: 10 }
               });
               
            =  chunks.forEach((chunk) => {
                 const [key, value] = chunk.split('=');
                 // key = 'banana', value = '10'
                 result[key] = value;
                 // result = { banana: '10' }
                 });      
``` 
       ㄴ. map()함수 
          -> 불변 변수(const)만을 사용
          -> 배열을 가공하여 새 배열을 만드는 함수
``` javascript 
         function parse(qs) {
           const queryString = qs.substr(1);
           // queryString = 'banana=10&apple=20&orange=30'
           const chunks = qs.split('&');
           // chunks = ['banana=10', 'apple=20', 'orange=30']
           const result = chunks.map((chunk) => {
             const [key, value] = chunk.split('=');
             // key = 'banana', value = '10'
             return { key: key, value: value };
             //{ key: 'banana', value: '10' }
             });
           return result;
         }
         // result = [ { key: 'banana', value: '10' }, { key: 'apple', value: '20' }, { key: 'orange', value: '30' } ];
         
        ㄷ. reduce()함수
           -> 배열을 객체로 변환
           function sum(numbers) {
             return numbers.reduce((total, num) => total + num, 0);
             }
           sum([1, 2, 3, 4, 5, 6, 7, 8, 9, 10]);
           // 55
           // reduce() 함수는 첫 번째 인자를 변환 함수, 두 번째 인자를 초기값 0으로 전달
           // 변환함수의 첫 번째 인자를 이전 결과값, 두 번째 인자를 배열의 각 요소 값
           // 초기값 0은 이전 결과값인 total에 할당
           // 순환 1회차 total: 0 num: 1
           // 순환 2회차 total: 0 + 1  num: 2
           // 순환 3회차 total: 0 + 1 +2 num: 3
           // ...
           // 순환 10회차 total: 0 + 1 + 2 + 3 + 4 + 5 + 6 + 7 + 8 + 9 num: 10
           // 최종 반환값 total: 0 + 1 + 2 + 3 + 4 + 5 + 6 + 7 + 8 + 9 + 10 num:55
           // 배열이 숫자로 변환
           
           function parse(qs) {
             const queryString = qs.substr(1); 
             // queryString = 'banana=10&apple=20&orange=30'
             const chunks = qs.split('&');
             // chunks = ['banana=10', 'apple=20', 'ornage=30']
             return chunks
               .map((chunks) => {
                 const [ key, value ] = chunks.split('=');
                 // key = 'banana', value = '10'
                 return { key, value };
                 // { key: 'banana', value: '10' }
                 })
               .reduce((result, item) => {
               // result = {}, item = { key: 'banana', value: '10' }
                 result[item.key] = item.value;
                 // result = { banana: '10' }
                 return result;
                 }, {});
                 // 초기값에 빈 객체 {}를 입력 
                 // 순환 1회차 result: {} item: { key: 'banana', value: '10' }
                 // 순환 2회차 result: {banana: '10'} item: {key: 'apple', value: '20'}
                 // ...
                 // 최종 반환 값 result: {banana: '10', app;e: '20', orange: '30'}
                    
```  

        9. 비동기 함수(콜백, 프로미스)
            -> 콜백함수: 전달해 준 함수를 나중에 불러옴
            -> 호이스팅(hoisting): 함수, 변수 등 코드가 나타나는 순서대로 자동적으로 실행
``` javascript 
              'use strict';
               
               console.log('1');
               setTimeout(function() {
                 console.log('2');
                 }, 1000);
                 // 1초가 지난 다음 console.log('2')실행
               console.log('3);
               // 1
               // 3
               // 1초가 지난 후
               // 2
               
            ㄱ. synchronous callback
            -> 즉각적으로 동기적으로 콜백함수 실행
                function printImmediately(print) { //print는 콜백
                  print();  //콜백 실행
                  }
                printImmediately( () => console.log('hello') );  
              
             ㄴ. Asynchronous callback
             -> 나중에 언제 콜백함수가 실행될 지 모름
                function printWithDelay(print, timeout) {
                  setTimeout(print, timeout);
                  }
                printWithDelay( () => console.log('async callback', 2000));
```                
             ㄷ. 콜백지옥 코드
``` javascript             
                class UserStorage {
                  loginUser(id, password, onSuccess, onError) {
                    setTimeout( () => {
                      if(
                         (id === 'ellie' && password === 'dream') || 
                         (id === 'coder' && password === 'academy')
                        ) {
                          onSuccess(id);
                          }
                          else {
                          onError(new Error ('not found'));
                          }
                        }, 2000);
                      }
                    getRoles(user, onSuccess, onError) {
                      setTimeout( () => {
                        if(user === 'ellie') {
                          onSuccess( {name: 'ellie', role: 'admin'} );
                          }
                          else {
                          onError( new Error('no access'));
                          }
                        }, 1000);
                      }
                    }
                    
                  const userStorage = new UserStorage();
                  const id = prompt('enter your ID');
                  const password = prompt('enter your password');
                  
                  userStorage.loginUser(
                    id,
                    passward,
                    user => { userStorage.getRoles(user, 
                                                   userWithRole => {
                                                     alert(
                                                       `Hello ${userWithRole.name}, you have a ${userWithRole.role} role`
                                                       );
                                                     },
                                                    error => {
                                                      console.log(error);
                                                      }
                                                    );
                                                  },
                     error => {
                       console.log(error);
                       }
                   );
                   
                   // 위 코드들의 문제점
                   // 1. 가독성이 떨어짐
                   // 2. 에러 발생 시 디버깅이 어려움
                   // 3. 유지보수 어려움
```               
              ㄹ. promise
              -> 비동기 처리 방식
              -> 네트워크 통신, 파일 읽어오기 등에 사용
              -> state: 프로미스 상태
                 pending: 프로미스 진행 중
                 fulfilled: 프로미스 완료
                 rejected: 파일을 찾을 수 없거나, 네트워크에 문제
                 producer: 원하는 기능을 수행하여 해당하는 데이터를 만들어 냄
                 consumer: 만들어 낸 데이터를 소비
``` javascript                 
                 a. producer
                 const promise = new Promise((resolve, reject) => {
                   console.log('doing something...');
                   // 새로운 프로미스가 생성됐을때 executor가 자동적으로 실행됨
                   });
                   settimeout( () => {
                     resolve('ellie');
                     // 성공적으로 데이터를 받아왔을때 resolve 콜백 함수를 호출하여 'ellie'라는 값을 전달함
                     }, 2000);
                     // reject(new Error( 'no network' ));
                 b. consumers: then(), catch(), finally()
                    promise.then((value) => {
                      -> 프로미스 값이 정상적으로 수행된다면 value값을 받아옴.
                      -> value는 'ellie' 이다
                      -> 프로미스가 성공적인 경우
                             console.log(value);
                             // 2초 후 'ellie' 콘솔 창에 수행
                           .catch(error => { 
                             // 프로미스 실패한 경우
                             console.log(error);
                           .finally( () => {
                            -> 프로미스 성공, 실패와 관계없이 무조건 실행
                             console.log('finally');    
                    });
```                   
               ㅁ.  promise 연결하기
``` javascript 
                  const fetchNumber = new Promise( (resolve, reject) => {
                    setTimeout( () => resolve(1), 1000);
                    });
                  fetchNumber
                    .then(num => num * 2) // 2
                    .then(num => num * 3) // 6
                    .then(num => {
                      return new Promise( (resolve, reject) => {
                        setTimeout( () => resolve(num - 1), 1000);
                        }); 
                      })
                    .then(num => console.log(num))
                    // 5
                    // 프로미스 전달 가능
                    // 2초 후 실행
```              
               ㅂ. promise 오류 처리
``` javascript 
                 const getHen = () => 
                   new Promise( (resolve, reject) => {
                     setTimeout( () => resolve('닭'), 1000 );
                     });
                 const getEgg = hen =>
                   new Promise( (resolve, reject) => {
                     setTimeout( () => resolve( `${hen} => 계란` ), 1000);
                     });
                 const cook = egg =>
                   new Promise( (resolve, reject) => {
                     setTimeout( () => resolve(`${egg} => 프라이`), 1000);
                     });
                 getHen()
                   .then(hen => getEgg(hen))
                   .then(egg => cook(egg))
                   .then(meal => console.log(meal));
                   // 결과) 닭 => 계란 => 프라이
                   
              =  getHen() // -> 코드 한 줄씩 작성되어 정리
                   .then(getEgg)
                   .then(cook)
                   .then(console.log);
                   
                 const getEgg = hen =>
                   new Promise((resolve, reject) => {
                     setTimeout( () => reject( new Error(`error! ${hen} => 계란`)), 1000);
                     });
                 getHen() //
                   .then(getEgg)
                   .catch(error => {
                     return '식용유';
                     })
                   .then(cook)
                   .then(console.log);                   
                   // 결과) 식용유 => 프라이
``` 
               ㅅ. 콜백 지옥 코드를 프로미스 코드로 바꿈
``` javascript 
                 class UserStorage {
                   loginUser(id, password) {
                     return new Promise((resolve, reject) => {
                       setTimeout( () => {
                         if(
                           (id === 'ellie' && password === 'dream') ||
                           (id === 'coder' && password === 'academy')
                           ){
                             resolve(id);
                            }
                         else{
                             reject(new Error('not found'));
                             }
                           }, 2000);
                         });
                       };
                     }
                    getRoles(user) {
                      return new Promise((resolve, reject) => {
                        setTimeout( () => {
                          if(user === 'ellie') {
                            resolve( {name: 'ellie', role: 'admin'} );
                            }
                          else {
                            reject( new Error('no access'));
                            }
                          }, 1000);
                        });
                      };
                      
                  const userStorage = new UserStorage();
                  const id = prompt('enter your id');
                  const password = prompt('enter your password');
                  userStorage.loginUser(id, password)
                    .then(userStorage.getRoles)
                    .then(user => alert(
                      `Hello ${user.name}, you have a ${user.role} role`
                      ))
                    .catch(console.log);  
```               
               
                            
        
        
        
          
         
      
      

   
    
      
      
      
      
