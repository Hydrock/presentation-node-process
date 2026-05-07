# Слайд 11: Пример Worker Threads (main.js)

Этот слайд демонстрирует основной код для запуска Worker Threads.

Пример main.js:
```javascript
const { Worker } = require('worker_threads');
const worker = new Worker('./worker.js');

worker.postMessage(1000000);
worker.on('message', (result) => {
  console.log('Результат:', result);
});

worker.on('error', (error) => {
  console.error('Ошибка:', error);
});

worker.on('exit', (code) => {
  if (code !== 0) {
    console.error('Worker завершился с кодом', code);
  }
});
```

Ключевые аспекты управления Worker Threads:
1. Создание нового экземпляра Worker
2. Передача данных через postMessage
3. Обработка результатов через событие 'message'
4. Обработка ошибок через 'error'
5. Отслеживание завершения через 'exit'

Важные моменты:
- Worker создается как отдельный процесс
- Передача данных между потоками требует сериализации
- Работа с памятью изолирована между потоками
- Ошибки в Worker не влияют на основной поток
- Необходимо корректно завершать Worker для освобождения ресурсов

Оптимизация:
- Используйте пул Worker для повторного использования
- Ограничивайте количество одновременных Worker
- Мониторьте использование памяти