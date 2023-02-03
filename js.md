# JS questions

## Strict / non-strict comparison

Что выведется на экран; почему?
Как именно происходит преобразование типов?

```js
console.log(1 == "1");
console.log(1 === "1");
```

## var/let/const

В чём отличие трёх объявлений переменных?
Какие есть нюансы в каждом случае?
Что будет, если попытаться вывести в консоль значение каждой переменной выше объявления?

```js
function main() {
  var x = 1;
  let y = 2;
  const z = 3;
}
```

## Value/reference

Что выведется на экран? Почему?

```js
function setToOne(v) {
  v = 1;
}

function setToTwo(v) {
  v.x = 2;
}

const x = 42;
setToOne(x);
console.log(`Should be set to 1: ${x}`);

const o = { x: 42 };
setToTwo(o);
console.log(`Should be set to 2: ${o.x}`);
```

## Iteration, floats

Написать функцию, подсчитывающую общую стоимость товаров в корзине `cart`, отталкиваясь от цен в объекте `prices`.
Усложнения (после написания функции):
1. Добавить в `cart` объект с `id`, для которого нет цены в `prices`. Какой будет результат выполнения? Как починить?
2. Оставить в `cart` только одно яблоко и один апельсин. Какой будет результат выполнения? Почему так?

```js
const prices = {
  apple: 0.1,
  orange: 0.2,
  kiwi: 0.3,
};

const cart = [
  { id: "apple", amount: 1 },
  { id: "orange", amount: 1 },
  { id: "kiwi", amount: 42 },
];

function calculateTotalPrice(prices, cart) {
  // TODO
}

console.log("Total price:", calculateTotalPrice(prices, cart));
```

## Closure

Что произойдёт при запуске и как это работает?

```js
function add(x) {
  const z = 4;
  return function (y) {
    return x + y + z;
  };
}

const sum = add(2)(3);
console.log(sum);
```

## Context

Что выведется в консоль при запуске? Почему?

```js
const box = {
  data: 42,

  log1: function () {
    console.log("log1", this.data);
  },

  log2: () => {
    console.log("log2", this.data);
  },
};

box.log1();
box.log2();
```

Применить функцию `box.log1` в контексте объекта `miniBox`, не модифицируя объект `miniBox`:

```js
const miniBox = {
  data: -3,
};

// TODO
```

## Async

В каком порядке выведутся числа в консоль? Почему?

```js
console.log(1);
setTimeout(() => console.log(2), 0);
console.log(3);
```

## Async: coding

Написать функцию паузы, которая "подождёт" примерно три секунды в коде, приведённом ниже:

```js
function pause(seconds) {
  // TODO
}

async function main() {
  console.log(`${new Date()}: start`);
  await pause(3);
  console.log(`${new Date()}: finish`);
}

main();
```

## Implement Function.prototype.bind(context, ...args)

Имплементировать полифилл `bind` (можно использовать любые другие возможности языка):

```js
function objXPlusYPlusZ(y, z) {
  return this.x + y + z;
}

const add5 = objXPlusYPlusZ.bind({ x: 2 }, 3);
const result = add5(4);

console.log(result);
```

(Ответ) пример имплементации:

```js
Function.prototype.bind = function (context, ...args) {
  return (...rest) => this.apply(context, [...args, ...rest]);
};
```

## Code review

Сделать code review функции:

```js
function b(l, a) {
  if (!a) return false;
  if (~l.indexOf(a)) l.push(a);

  return a;
}
```

(Ответ) примеры проблемных моментов:
- the function returns a different type of value
- do not use '!a' empty value checking
- change a list by reference (no side effects)
- the function name is not readable
- documentation is empty
- arguments name are not readable
- `if` expression better use with brackets
- a bad condition of checking including an element to list
