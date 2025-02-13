# avito-qa-test-tasks
# Репозиторий с решениями тестовых заданий для QA-intern в Avito.
# Задание 1
Решение находится в файле [TASK_1](TASK_1.md)

# Задание 2.1

### Для выполнения данного задания я решил воспользоваться возможностями автоматизации Postman, вот [список тест-кейсов](./TESTCASES.md), вот  [коллекция Postman с автотестами](./TASK_2.1_SKOROV.json).

## Инструкция по запуску коллекции Postman

Эта инструкция поможет вам запустить коллекцию Postman, которая находится тут [Скачать коллекцию Postman](./TASK_2.1_SKOROV.json). Вы можете запускать всю коллекцию с помощью Postman Runner или (при необходимости) отдельные запросы.

## Предварительные требования

1. **Импортируйте коллекцию**:
    - Откройте Postman.
    - Нажмите на кнопку "Import" в верхнем левом углу.
    - Выберите файл `Anatoly-QA-internship.postman_collection.json` и нажмите "Import".

## Настройка переменных окружения

1. **Создайте новое окружение**:
    - В Postman нажмите на значок глаза в верхнем правом углу и выберите "Manage Environments".
    - Нажмите "Add" для создания нового окружения.
    - Назовите окружение, например, `QA Internship`.
    - Добавьте переменную `baseUrl` и вставьте хост `https://qa-internship.avito.com`.
    - Сохраните окружение.
2. **Выберите окружение**:
    - В выпадающем списке окружений выберите только что созданное окружение `QA Internship`.

## Запуск всей коллекции с помощью Postman Runner (рекомендуется этот способ, он является автоматизированным)

1. **Откройте Postman Runner**:
    - В меню Postman нажмите на значок "Runner". Кнопка располагается либо слева вверху, либо справа внизу (зависит от вашей версии postman). 

2. **Выберите коллекцию**:
    - В открывшемся окне Runner выберите коллекцию `Anatoly-QA-internship`.
    - Убедитесь, что выбрано правильное окружение (например, `QA Internship`).

3. **Настройте параметры запуска**:
    - Вы можете указать количество итераций (например, 1 для однократного запуска).

4. **Запустите коллекцию**:
    - Нажмите кнопку "Run Anatoly-QA-internship".
    - Postman начнет выполнение всех запросов в коллекции по очереди.
    - Результаты выполнения каждого запроса будут отображаться в реальном времени.

5. **Просмотр результатов**:
    - После завершения выполнения коллекции вы увидите сводку результатов.
    - Вы можете просмотреть детали каждого запроса, включая статус код, время выполнения и результаты тестов.

## Тут можно посмотреть [список обнаруженных багов](./BUGS.md)

## Запуск отдельных запросов

1. **Откройте коллекцию**:
    - В левой панели Postman найдите импортированную коллекцию `Anatoly-QA-internship`.
    - Разверните коллекцию, чтобы увидеть все запросы.

2. **Запустите тесты**:
    - Выберите запрос, который хотите протестировать.
    - Нажмите кнопку "Send" для отправки запроса.
    - Результаты тестов будут отображены в нижней части интерфейса Postman.

## Примечание

В коллекции используются сниппеты postman для автоматизации проверок. Вот основное, что применял:

### 1. **Проверка статус-кода**
- В каждом тесте используется сниппет для проверки, что статус-код ответа соответствует ожидаемому. Например:
  ```javascript
  pm.test("Статус код 200", function () {
      pm.response.to.have.status(200);
  });
  ```
- Этот код проверяет, что статус-код ответа равен `200`. Если код отличается, тест будет провален.

### 2. **Чтение данных из ответа и сохранение в переменную**
- В некоторых запросах используется сниппет для извлечения данных из ответа и сохранения их в переменные окружения. Например:
  ```javascript
  const responseData = pm.response.json();
  if (responseData.status) {
      const uuid = responseData.status.split(" - ")[1];
      if (uuid) {
          pm.environment.set("id", uuid);
          console.log("UUID сохранен в переменную id:", uuid);
      }
  }
  ```
- Этот код:
    - Парсит JSON-ответ.
    - Извлекает UUID из поля `status`.
    - Сохраняет UUID в переменную окружения `id`, которая может быть использована в последующих запросах.
