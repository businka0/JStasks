# Задание 3. Задачи на JavaScript

## Задачи
### 2. Ключи и свойства

Реализуйте функцию, которая получает на вход объект, а возвращает объект, в котором в качестве ключей указаны типы, встречающиеся в исходном объекте, а в качестве значений - как часто они встречались.

Пример:

```js
const initialObj = {
    a: 'some string 1',
    b: 42,
    c: { c1: 'some string 2' },
    d: [],
    e: 123,
};

const resultObj = solutionFn(initialObject);

console.log(resultObj);
/**
 * {
 *   string: 1,
 *   number: 2,
 *   object: 2
 * } 
 */

```

Примечание: в решении достаточно использовать оператор `typeof`.

### Решение 

```js
/*массив типов значений*/
const typeOfinitialObj = [];
function CountTypeOfObj(initialObj){
    for (key in initialObj) {
        typeOfinitialObj.push(typeof initialObj[key])/*добавить тип значения в массив*/
                            }
    return typeOfinitialObj.reduce((prev, curr) => (prev[curr] = ++prev[curr] || 1, prev), {})/*вернуть тип объекта и как часто встречался*/
    }


CountTypeOfObj(initialObj_test);
```

### 3. Больше никаких шуток про 1 + '1' === '11'

В JavaScript оператор "+" помимо сложения чисел может выполнять роль конкатенации.
Если один из операндов - строка, то второй автоматически преобразуется к строке, и они конкатенируются.

Иногда это может привести к неожиданных последствиям...

```js
console.log(('b' + 'a' + + 'a' + 'a').toLowerCase()); // 'banana'
```

Напишите функцию `sum`, которая:
* Принимает два значения
* Проверяет, является ли каждый из них числом
* Если они оба числа, то возвращается их сумма
* Если левый операнд не является числом, то выкидывается ошибка "The left operand is not number"
* Если правый операнд не является числом, то выкидывается ошибка "The right operand is not number"
* Если оба операнда не являются числами, то выкидывается ошибка "Operands are not numbers"

### Решение 

```js
function sum(left_value, right_value){
    try {
        if (typeof left_value === "number" && typeof right_value === "number"){
            return left_value + right_value;
        } else if(typeof left_value !== "number" && typeof right_value === "number"){
            throw "The left operand is not number";
        } else if(typeof left_value === "number" && typeof right_value !== "number"){
            throw "The right operand is not number";    
        } else {
            throw "Operands are not numbers"; 
        }
    }
    catch(err) {
        console.log("Error: " + err + ".");
      }
    }

/*Тесты и результаты:*/

sum(5, 16) // 21
sum('55', 22) // Error: The left operand is not number.
sum(22, []) // Error: The right operand is not number.
sum('55', []) // Error: Operands are not numbers.
```

### 6. Hit Or Run

Вы пишите искусственный интеллект (ИИ) для одной пошаговой стратегии. 
ИИ в один момент времени может либо бить `hit`, либо бежать `run`.

Напишите функцию `hitOrRun`, которая:
* Принимает на вход два натуральных числа `a` и `b` (`a < b`)
* Генерирует рандомное число в промежутке `[a, b]`
* Проверяет, является ли оно простым
* Если является, то возвращает строку `run`
* Если не является, то возвращает строку `hit`

### Решение 

```js
/*Проверка является ли число простым*/
function isPrime(num) {
    if (num <= 1) return false;
    if (num=== 2) return true;
    let num2 = Math.sqrt(num);
    for (let i= 2; i <= num2; i++) { 
     if (num2 % i === 0) {
     return false;
      }
    }
     return true;
    }
/*Функция hitOrRun*/
function hitOrRun(a, b){
    const random_number = Math.floor(Math.random() * (b - a + 1)) + a;

    console.log(random_number);

    if (isPrime(random_number) == true){
        return 'Run';
    }
    else {
        return 'hit';
    }

  
}

hitOrRun(555555, 937738363555);
```
### 7. Case Converter

В одном веб-приложении весь код бэкенда пишется в [snake_case](https://developer.mozilla.org/en-US/docs/Glossary/Snake_case) (все слова в нижнем регистре и разделяются нижним подчёркиванием), а фронтенд - в [camelCase](https://developer.mozilla.org/en-US/docs/Glossary/Camel_case) (слова не разделяются, первое слово пишется в нижнем регистре, у каждого следующего слова первая буква в верхнем регистре, остальные - в нижнем).

Чтобы обеспечить корректную передачу данных с бэкенда на фронтенд необходимо написать функцию, которая принимает на вход строку в `snake_case` и превращает её в строку в `camelCase`.

Пример:

```js
const snakeData = 'data_in_snake_case';

const result = solutionFn(snakeData);
console.log(result); // "dataInSnakeCase"
```

Подсказка: при решении используйте встроенные [методы строк](https://developer.mozilla.org/ru/docs/Web/JavaScript/Reference/Global_Objects/String) (так быстрее и проще).

### Решение 

```js
function case_converter(snake_case) {
    let myStringToArray = []
    let firstLetter = []
    let remainingLetters = []
    
    myStringToArray = snake_case.split('_');
    console.log(myStringToArray);
    for (i in myStringToArray) {
        if (i != 0){
            firstLetter.push(myStringToArray[i].charAt(0).toUpperCase())
            remainingLetters.push(myStringToArray[i].slice(1))
        }
        else {
            firstLetter.push(myStringToArray[i].charAt(0))
            remainingLetters.push(myStringToArray[i].slice(1))
        }

    }
    
    var c = firstLetter.map(function (d, i) {
        return d + String(remainingLetters[i])
    })

    return c.join('')

}


/*Тесты и результаты:*/
case_converter('some_extremely_useful_function') //someExtremelyUsefulFunction
```

### 8. Антиспам

Одной из важных составляющих многих почтовых антиспам-систем является анализ текста письма.
В частности, если в нём содержатся определённые ключевые слова, фразы и обороты, то с высокой долей вероятности он будет отнесён к спаму.

Реализуйте функцию простейшей проверки текста на спам. Она должна иметь следующий формат:

```js
/**
 * Принимает на вход текст письма и массив ключевых слов и проверяет,
 * содержится ли хотя бы одно из ключевых слов в этом тексте
 * 
 * @param {String} text - текст, проверяемый на спам
 * @param {String[]} keywords - массив ключевых слов
 * @returns {Boolean}
 */
function isSpam(text, keywords) {
    // ваш код здесь
}
```

### Решение 

```js
function case_converter(snake_case) {
    let myStringToArray = []
    let firstLetter = []
    let remainingLetters = []
    
    myStringToArray = snake_case.split('_');
    console.log(myStringToArray);
    for (i in myStringToArray) {
        if (i != 0){
            firstLetter.push(myStringToArray[i].charAt(0).toUpperCase())
            remainingLetters.push(myStringToArray[i].slice(1))
        }
        else {
            firstLetter.push(myStringToArray[i].charAt(0))
            remainingLetters.push(myStringToArray[i].slice(1))
        }

    }
    
    var c = firstLetter.map(function (d, i) {
        return d + String(remainingLetters[i])
    })

    return c.join('')

}


/*Тесты и результаты:*/
case_converter('some_extremely_useful_function') //someExtremelyUsefulFunction
```

### 9. The World!

Один из способов заставить страницу зависнуть - вызвать внутри функции бесконечный цикл.
Такая функция никогда не покинет стек вызовов, из-за чего браузер никогда не сможет вызвать функцию перерисовки страницы (или любую другую).

Но иногда такую функцию можно использовать и на благо, например, замораживать выполнение кода внутри функции на определённое время.

Напишите функцию, которая останавливает время и выводит в консоль сообщение о том, сколько осталось секунд до возобновления.
Она должна иметь следующий формат:

```js
/**
 * Останавливает время на определённое количество миллисекунд
 * 
 * @param {Number} ms - количество миллисекунд, на которое необходимо остановить время
 */
function theWorld(ms) {
    // ваш код здесь,
    // включая вывод в консоль сообщения "Time will continue running in <remaining_seconds_number>"
}
```

Подсказка: задачу можно решить с помощью асинхронности, либо c помощью объекта `Date`. Тестировать решение можно прямо в консоли браузера (только стоит быть аккуратнее, иначе зависнет не только страница, но и весь браузер 🙃).

Пример:

```js
console.log('Выведется до остановки времени');

theWorld(3000); // или await theWorld(3000), если решать через асинхронность

// Выведется в консоли:
// "Time will continue running in 3"
// "Time will continue running in 2"
// "Time will continue running in 1"
// "Time will continue running in 0"

console.log('Выведется после того, как время продолжит ход');
```


### Решение 

```js
/**
 * Останавливает время на определённое количество миллисекунд
 * 
 * @param {Number} ms - количество миллисекунд, на которое необходимо остановить время
 */
function theWorld(ms) {
    (function doStuff() {
      
      if (ms >= 0) {
        setTimeout(doStuff, 1000);
        console.log("Time will continue running in "  + ms +  " seconds");
        ms -= 1;
      }
      else {
        console.log("Time started again");
    }

      

    }());
  }
  
  theWorld(10);
```

### 10. Задача с собеседования

Первой задачей на алгоритмическом собеседовании на должность фронтенд-разработчика обычно дают что-то несложное, для разминки.

Например, напишите функцию, которая:
* Получает на вход натуральное число
* Перемножает все цифры числа, до тех пор, пока оно не станет одноразрядным
* Возвращает итоговое одноразрядное число

Пример:

```js
console.log(solutionFn(4));     // возвращает 4, так как уже одноразрядное
console.log(solutionFn(42));    // возвращает 8, так как 4 * 2 = 8
console.log(solutionFn(999));   // возвращает 2, так как 9 * 9 * 9 = 729, 7 * 2 * 9 = 126, 1 * 2 * 6 = 12, и наконец 1 * 2 = 2 
```

Попробуйте написать такую функцию.

### Решение 

```js
function oneFigureNumber(number){
    let splitStringW = '';

    function prep_function(numberToString) {
        numberToString = numberToString.toString();
        var splitString = numberToString.split("");
        return splitString;
    }
    
    function multiply_function(arrayToMultily) {
        const res = arrayToMultily.reduce((acc, rec) => acc * rec);
        return res;
    }

    splitStringW = prep_function(number);
    do {
        result = multiply_function(splitStringW);
        splitStringW = prep_function(result);
    }
    while (splitStringW.length > 1);

    return Number(splitStringW[0]);
}

oneFigureNumber(11)

/*Тесты: */ 
oneFigureNumber(1234) // 8
oneFigureNumber(12346) //6
```
