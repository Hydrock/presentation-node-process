# Слайд 10: Практические примеры Worker Threads

Этот слайд демонстрирует практическое применение Worker Threads в Node.js.

Пример worker.js:
```javascript
const { parentPort } = require('worker_threads');

parentPort.on('message', (data) => {
  // CPU-intensive задача
  const result = heavyCalculation(data);
  parentPort.postMessage(result);
});

function heavyCalculation(input) {
  let sum = 0;
  for (let i = 0; i < input; i++) {
    sum += i * i;
  }
  return sum;
}
```

Ключевые особенности Worker Threads:
- Создание нового процесса с собственной памятью
- Отдельный Event Loop
- Возможность параллельного выполнения
- Синхронизация через postMessage
- Ограничение на передачу объектов (не все типы данных поддерживаются)

Преимущества:
- Изоляция от основного потока
- Параллельное выполнение CPU-интенсивных задач
- Безопасность (ошибки в воркере не ломают основное приложение)
- Возможность масштабирования

Сравнение с Libuv:
- Worker Threads для CPU задач
- Libuv для I/O задач