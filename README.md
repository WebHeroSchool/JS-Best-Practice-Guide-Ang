# JavaScript Best Practice Guide

### 1. Повторяющийся код
Если в коде проходится часто копировать и вставлять блок кода, это признак того, что данный блок можно выделить в отдельную функцию.
```
const exampleArray = [ [ [ 'value' ] ] ];

exampleArray.forEach((arr1) => {
  arr1.forEach((arr2) => {
    arr2.forEach((el) => {
      console.log(el)
    })
  })
})
```
Будет гораздо лучше выделить его в отдельную функцию и управлять логикой иначе, с меньшим количеством повторов:
```
const exampleArray = [ [ [ 'value' ] ] ];

const retrieveFinalValue = (element) => {
  if(Array.isArray(element)) {
    return fetchValue(element[0]);
  }

  return element;
}
```
В этом случае, при необходимости внести изменения, не нужно искать повторяющиеся куски кода во всем файле, что, вероянее всего приведет к возникновению ошибок, достаточно внести измения один раз в функцию.

### 2. Имена переменных
Camel case («верблюжий регистр») в JavaScript используется практически всегда. Это стандарт для написания имен переменных и функций. Суть его в том, что в имени первое слово должно начинаться со строчной буквы (нижний регистр), а все первые буквы последующих слов должны быть заглавными (верхний регистр). Вот несколько примеров:
```
thisIsARandomCamelCaseName, camelCase, exampleFunctionName. 
```
Такой стандарт значительно улучшает читаемость и понимание кода.

### 3. Использование подходящих по смыслу наименований
getUserData и getUserInfo — довольно нечеткие имена. О каких данных и какой информации идет речь? Важно, чтобы имена наших функций, методов и переменных выражали их точное значение. GetUserPost — куда лучшее имя, поскольку здесь мы точно понимаем, что извлекаем.
Имя функции должно быть глаголом или фразой, содержащей глагол, и должно сообщать о том, что эта функция делает. При этом следует быть последовательным. Т.е., для извлечения данных всегда использовать get, а не get, retrieve, return и десять тысяч других слов.

Хороший пример
```
getUserPosts, getUsers, 
```
Плохой пример
```
returnUsers, retrieveUsers.
```

### 4. Использование точки с запятой
Плохой пример
```
var someItem = 'some string'  
function doSomething() {  
  return 'something'  
} 
```
Хороший пример
```
var someItem = 'some string';  
function doSomething() {  
  return 'something';  
}
```
При компиляции точки с запятой будут расставлены автоматически, но возможно совсем не тех местах, где нужно, что привет к большим проблемам.

### 5. Глобальные переменные
Глобальные переменные и имена функций - невероятно плохая идея. Причина в том, что каждый файл JavaScript, включенный в страницу, работает в той же области. Если в коде есть глобальные переменные или функции, скрипты, повторяющиеся в разных скриптах, они будут перезаписывать друг друга.

Плохой пример
```
let current = null;
function init() {
	…
}
function change() {
	…
}
function verify() {
	…
}
```
Хороший пример
```
let myNameSpace = {
	current:null,
	init:function() {
		…
	},
	change:function() {
		…
	},
	verify:function() {
		…
	}
}
```

### 6. Использование === вместо ==
В JavaScript существует два разных типа операций сравния: === / !== и == / !=. Считается хорошим тоном всегда использовать первую пару для сравнения.
```
0 == "";    // true  
0 === "";   // false
```

### 7. Использование комментариев умеренно
Это кажется излишним в начале, но когда вы вернетесь к проекту через несколько месяцев, это поможет понять, что делает тот или иной кусок кода. Комментируйте важные части кода.
```
// Cycle through array and echo out each name.   
for(var i = 0, len = array.length; i < len; i++) {  
   console.log(array[i]);  
}  
```

### 8. Использование фигурных скобок для блоков кода
Технически можно писать код без фигурных скобок и точек с запятой, но в следующем примере браузер по разному вопримет код с использованием фигурных скобок и без:
```
if(someVariableExists)  
   x = false  
   anotherFunctionCall(); 
```
```
if(someVariableExists) {  
   x = false;  
   anotherFunctionCall();  
}  
```

### 9. Использование пробелов
Для отступа используйте 2 пробела. Помимо перевода строки, горизонтальный символ пробела (0x20) ASCII это единственный пробельный символ, используемый в файле исходного кода. Это означает, что символы табуляции не используются для отступов.

Плохой пример
```
function bar() {
∙let name;
}
```
Хорощий пример
```
function baz() {
∙∙let name;
}
```

### 10. Использование let и const
Для объявления переменных необходимо использовать let, а для объявления констант используйте const. От использования var нужно отказаться, но такое объявления еще может встречаться в старом коде.

Плохой пример
```
var example = 42;
```
Хороший пример
```
let example = 42;
```
