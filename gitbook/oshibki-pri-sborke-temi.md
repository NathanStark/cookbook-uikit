# Как обнаружить ошибку ?

Если во время сборке, есть похожий текст, это значит что есть критическая ошибка, из-за которой тема не будет  собрана.

```js
(node:12467) UnhandledPromiseRejectionWarning
(node:12467) UnhandledPromiseRejectionWarning: Unhandled promise rejection. This error originated either by throwing inside of an async function without a catch block, or by rejecting a promise which was not handled with .catch(). (rejection id: 1)
(node:12467) [DEP0018] DeprecationWarning: Unhandled promise rejections are deprecated. In the future, promise rejections that are not handled will terminate the Node.js process with a non-zero exit code.
```

## Основные причины

1. Последовательность компонента была нарушена
2. Не указаны перемены в less необходимые для работы
3. Не подключены критически важные компоненты



