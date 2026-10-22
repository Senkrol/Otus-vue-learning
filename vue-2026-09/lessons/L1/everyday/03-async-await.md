# Async / await

## Кратко
Синтаксический сахар над промисами. Позволяет писать асинхронный код так, будто он синхронный.

## Правила
- `async` перед функцией → функция **всегда возвращает промис**.
- `await` можно использовать **только внутри `async`**-функции (или на верхнем уровне модуля ESM).
- `await` «замораживает» выполнение функции до результата промиса.

```js
async function loadUser() {
  const response = await fetch('/api/user'); // ждём
  const user = await response.json();        // ждём
  return user;                               // вернётся как Promise
}

loadUser().then(user => console.log(user));
```

## Обработка ошибок — `try/catch`

```js
async function loadUser() {
  try {
    const response = await fetch('/api/user');
    if (!response.ok) throw new Error(`HTTP ${response.status}`);
    return await response.json();
  } catch (error) {
    console.error('Не удалось загрузить:', error);
  } finally {
    console.log('запрос завершён');
  }
}
```

## Последовательно vs параллельно

```js
// ❌ медленно: ждём по очереди
const a = await fetchA();
const b = await fetchB();

// ✅ быстро: запускаем параллельно
const [a, b] = await Promise.all([fetchA(), fetchB()]);
```

> `await` в цикле `for` тоже идёт последовательно. Если запросы независимы — используйте `Promise.all`.

## Во Vue

```vue
<script setup>
import { ref, onMounted } from 'vue';

const users = ref([]);
const loading = ref(false);

const loadUsers = async () => {
  loading.value = true;
  try {
    const res = await fetch('/api/users');
    users.value = await res.json();
  } catch (e) {
    console.error(e);
  } finally {
    loading.value = false;
  }
};

onMounted(loadUsers);
</script>
```
