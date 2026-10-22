# Proxies (Proxy и Reflect)

## Кратко
`Proxy` — обёртка над объектом, которая **перехватывает** операции (чтение, запись, удаление, вызов и т. д.). В паре с ним обычно используют `Reflect` — он выполняет «настоящую» операцию.

```js
const target = { name: 'Ann' };

const proxy = new Proxy(target, {
  get(obj, key) {
    console.log(`читаем ${key}`);
    return Reflect.get(obj, key);   // выполнить реальное чтение
  },
  set(obj, key, value) {
    console.log(`пишем ${key} = ${value}`);
    return Reflect.set(obj, key, value); // вернуть true при успехе
  },
});

proxy.name;        // лог: читаем name → 'Ann'
proxy.name = 'Bob'; // лог: пишем name = Bob
```

## Ловушки (traps)

| Ловушка | Перехватывает |
|---------|---------------|
| `get` | чтение свойства |
| `set` | запись свойства |
| `has` | оператор `in` |
| `deleteProperty` | `delete obj.key` |
| `ownKeys` | `Object.keys`, `for...in` |
| `apply` | вызов функции |
| `construct` | `new Proxy(...)` |

## Зачем нужен
- **Реактивность** (Vue 3): на `get` — собрать зависимости, на `set` — сообщить об изменении.
- Валидация и контроль доступа к объекту.
- Логирование и отладка обращений.
- Отрицательные индексы массивов и другие «магические» поведения.

## Мини-пример реактивности

```js
function reactive(target, onChange) {
  return new Proxy(target, {
    get(obj, key) { return Reflect.get(obj, key); },
    set(obj, key, value) {
      const old = obj[key];
      const ok = Reflect.set(obj, key, value);
      if (old !== value) onChange(key, value); // уведомляем подписчиков
      return ok;
    },
  });
}

const state = reactive({ count: 0 }, (k, v) => console.log(`${k} → ${v}`));
state.count++; // count → 1, и любой подписчик мог бы обновить UI
```

## Proxy vs Object.defineProperty
- `defineProperty` (Vue 2) перехватывает только **уже известные** ключи и не видит добавление/удаление свойств и индексы массивов.
- `Proxy` (Vue 3) перехватывает **любые** операции — это одно из главных улучшений реактивности Vue 3.
