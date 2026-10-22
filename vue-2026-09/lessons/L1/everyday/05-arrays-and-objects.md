# Работа с массивами и объектами

## Массивы: методы (не мутируют исходный массив)

```js
const nums = [1, 2, 3, 4, 5];

nums.map(n => n * 2);            // [2, 4, 6, 8, 10] — преобразовать
nums.filter(n => n % 2 === 0);   // [2, 4]          — отобрать
nums.reduce((acc, n) => acc + n, 0); // 15         — свернуть в одно
nums.find(n => n > 3);           // 4               — первый подходящий
nums.findIndex(n => n > 3);      // 3
nums.some(n => n > 4);           // true            — есть ли хоть один
nums.every(n => n > 0);          // true            — все ли подходят
nums.includes(3);                // true
nums.flat();                     // разворачивает вложенные массивы
```

## Массивы: мутирующие методы

```js
const arr = [1, 2, 3];
arr.push(4);        // [1,2,3,4] — в конец
arr.pop();          // убрать последний
arr.unshift(0);     // добавить в начало
arr.shift();        // убрать первый
arr.splice(1, 1);   // убрать/вставить с позиции
arr.sort((a, b) => a - b); // сортировка (ПО УМОЛЧАНИЮ — по строке!)
arr.reverse();
```

> `sort()` без компаратора сортирует как строки: `[10, 2, 1]` → `[1, 10, 2]`.

## Деструктуризация

```js
const [first, , third] = [1, 2, 3];       // first=1, third=3
const [a = 0, b = 0] = [5];               // значения по умолчанию
const { name, age, city = '—' } = user;   // объект
const { name: userName } = user;          // переименование
```

## Объекты: полезные приёмы

```js
const user = { name: 'Ann', age: 25 };

Object.keys(user);    // ['name', 'age']
Object.values(user);  // ['Ann', 25]
Object.entries(user); // [['name','Ann'], ['age',25]]

// Spread — поверхностное копирование / объединение
const copy = { ...user, age: 26 };
const merged = { ...obj1, ...obj2 }; // правые ключи побеждают

// Проверка наличия ключа
'name' in user; // true
user.name ?? 'нет'; // nullish-оператор
```

## Optional chaining `?.` и `??`

```js
user?.address?.city;         // не упадёт, если address === undefined
const value = data ?? 'default'; // ?? только для null/undefined
```

## Во Vue

```js
// v-for по массиву объектов
items.filter(i => i.active).map(i => i.name);

// реактивные объекты — всегда создавайте НОВЫЙ объект, а не мутируйте
state.user = { ...state.user, name: 'Bob' };
```
