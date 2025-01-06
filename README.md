# Лабораторная работа 1 — Wget на минималках

**СТУДЕНТ**: Фам Ань Ту  
**ГРУППА**: 932101  

## REQUIRES:

### Структура:

1. `manifest.json`, `service-worker.js`, icons
2. `index.html` (скрипт: `client.js`)

### Установка WPA:

1. Кнопка **Install** (будет скрыта, если приложение уже установлено, обрабатывается через событие `beforeInstallPrompt`).
2. Оффлайн-режим с использованием кеширования.

### Использование хранилища:

1. **IndexedDB**.

### Данные и операции:

1. Создание домена.
2. Удаление домена (вместе с профилями внутри домена).
3. Создание профиля (с авто-сгенерированным паролем).
4. Редактирование пароля профиля.
5. Показ информации о пароле профиля (с предыдущими паролями до редактирования).
6. Удаление профиля.

## РЕЗУЛЬТАТ:

- Для запуска программы используйте команду `npx serve .`, чтобы **Service Worker** мог работать, или откройте файл `index.html` в браузере (без функции **INSTALL**).

---

## Объяснение файла `client.js`

Файл `client.js` предоставляет класс `PasswordManagerApplication`, который реализует все методы, работающие с **IndexedDB**.

### Основные моменты:

#### Метод `displayList()`:

- Отображает список доменов и профилей на странице `index.html` с использованием строки **JSX**.
- Каждый раз, когда вызывается `displayList()`, программа сначала выполняет `document.removeEventListener`, чтобы удалить все предыдущие обработчики событий.
- После этого заново добавляются обработчики событий с помощью `document.addEventListener`. Это предотвращает конфликты и нежелательное поведение приложения, вызванное старыми обработчиками.

Такой подход гарантирует, что приложение работает корректно и без ошибок, даже при динамическом изменении DOM-элементов.

---

## Структура IndexedDB

**IndexedDB** сохраняет две таблицы (ObjectStore):

1. **domains**:  
   - `id`: уникальный идентификатор (тип данных `number`, автоинкремент).
   - `name`: название домена (тип данных `string`, уникальное значение).

2. **profiles**:  
   - `id`: уникальный идентификатор (тип данных `number`, автоинкремент).
   - `username`: имя пользователя (тип данных `string`).
   - `password`: пароль (тип данных `string`).
   - `oldPassword`: массив объектов, содержащих старые пароли.
     - Каждый объект имеет структуру: 
       - `password`: старый пароль (тип данных `string`).
       - `savedAt`: временная метка сохранения старого пароля (тип данных `timestamp`).
   - `updatedAt`: временная метка последнего обновления (тип данных `timestamp`).

