# L1 — База JavaScript для Vue

Краткие шпаргалки по темам, которые нужны для повседневной работы с Vue и для понимания его реактивности.

## 📌 Для повседневной работы
Основы синтаксиса и приёмов, которые используются в каждом компоненте.

| # | Тема | Файл |
|---|------|------|
| 1 | Arrow Functions | [everyday/01-arrow-functions.md](everyday/01-arrow-functions.md) |
| 2 | Promises | [everyday/02-promises.md](everyday/02-promises.md) |
| 3 | Async/await | [everyday/03-async-await.md](everyday/03-async-await.md) |
| 4 | ES modules | [everyday/04-es-modules.md](everyday/04-es-modules.md) |
| 5 | Работа с массивами и объектами | [everyday/05-arrays-and-objects.md](everyday/05-arrays-and-objects.md) |

## 🔄 Для понимания реактивности
Внутренние механизмы, на которых построена реактивность Vue 3.

| # | Тема | Файл |
|---|------|------|
| 1 | Set | [reactivity/01-set.md](reactivity/01-set.md) |
| 2 | Map | [reactivity/02-map.md](reactivity/02-map.md) |
| 3 | WeakMap | [reactivity/03-weakmap.md](reactivity/03-weakmap.md) |
| 4 | Proxies | [reactivity/04-proxies.md](reactivity/04-proxies.md) |

---

### Зачем это всё во Vue?
- **Arrow functions + `async/await`** — обработчики событий и запросы к API в `methods` / `setup`.
- **ES modules** — синтаксис `import` / `export` в `*.vue`-файлах и `.js`-модулях.
- **Массивы и объекты** — рендеринг списков (`v-for`) и работа со `state`.
- **`Proxy` + `Reflect`** — ядро реактивности Vue 3 (то, что делает `ref` / `reactive` «живыми»).
- **`Set` / `Map` / `WeakMap`** — используются внутри Vue (`Map` для зависимостей, `WeakMap` для кэшей и хранения связей) и часто нужны в прикладном коде.
