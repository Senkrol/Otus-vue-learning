# ES Modules (модули ES6)

## Кратко
Стандартный механизм модулей в JavaScript: одни файлы экспортируют значения, другие их импортируют. Каждый модуль имеет свою область видимости.

## Именованный экспорт / импорт

```js
// utils.js
export const PI = 3.14;
export function sum(a, b) { return a + b; }
export class Api {}

// main.js
import { PI, sum } from './utils.js';
import { sum as add } from './utils.js';   // переименование
import * as utils from './utils.js';        // весь модуль
import './styles.css';                      // импорт ради побочного эффекта
```

## Экспорт по умолчанию (default)

```js
// Button.vue
export default { name: 'Button' };

// main.js
import Button from './Button.vue'; // имя любое, без {}
```

## Правила
- Экспортов **default** — максимум один на файл; именованных — сколько угодно.
- `import` поднимается в начало модуля (hoisting).
- Импорты **read-only**: переприсвоить импортированную переменную нельзя.
- Живые привязки: модуль видит актуальное значение экспортированного `let`.

## Динамический импорт (ленивая загрузка)

```js
const { heavyFn } = await import('./heavy.js'); // возвращает Promise
```

## Во Vue / Vite

```js
// main.js
import { createApp } from 'vue';
import App from './App.vue';
import router from './router';

createApp(App).use(router).mount('#app');
```

```js
// Ленивая загрузка маршрута
const routes = [
  { path: '/about', component: () => import('@/views/About.vue') },
];
```

Псевдоним `@` (алиас `src`) настраивается в `vite.config.js` / `jsconfig.json` — это тоже часть модульной системы сборки.
