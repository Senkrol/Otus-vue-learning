# Arrow Functions (стрелочные функции)

## Кратко
Компактный синтаксис функций из ES6. Не имеют собственных `this`, `arguments`, `super` и не могут вызываться через `new`.

## Синтаксис

```js
// Обычная функция
function sum(a, b) {
  return a + b;
}

// Стрелочная функция
const sum = (a, b) => a + b; // если тело — одно выражение, return не нужен

// Один аргумент — скобки можно опустить
const double = n => n * 2;

// Нет аргументов
const getDate = () => new Date();

// Многострочное тело — нужны фигурные скобки и явный return
const calc = (a, b) => {
  const result = a * b;
  return result;
};

// Возврат объекта — оборачиваем в круглые скобки
const makeUser = (name) => ({ name, active: true });
```

## Ключевое: `this`
Стрелочная функция **не создаёт свой `this`** — берёт его из внешнего (лексического) контекста.

```js
const counter = {
  value: 0,
  // ❌ не сработает: this будет внешним (window/undefined)
  broken: () => this.value++,

  // ✅ обычный метод
  increment() { this.value++; },

  // ✅ стрелка внутри метода сохраняет this класса counter
  good() {
    [1, 2, 3].forEach(() => this.value++);
  },
};
```

## Когда использовать
- Колбэки (`map`, `filter`, `forEach`, `setTimeout`, обработчики).
- Методы внутри `setup()` во Vue (там `this` не нужен).
- Короткие функции в одну строку.

## Когда НЕ использовать
- Как методы объекта, которым нужен собственный `this`.
- Как функции-конструкторы (`new`).
- Когда нужен объект `arguments` (используйте rest `...args`).

## Во Vue
```vue
<script setup>
import { ref } from 'vue';

const count = ref(0);
const increment = () => count.value++;       // обработчик события
const items = ref([1, 2, 3]);
const doubled = items.value.map(n => n * 2); // колбэк
</script>
```
