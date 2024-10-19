## AIS24
### Домашнее задание 1 по дисциплине "Архитектура информационных систем"

Разработать три http  сервиса (у каждого по одному  http роуту), эмулирующие идентификацию пользователя
- Сервис score. На вход поступает строковый логин. В ответе — оценка «хорошести» пользователя (float).
- Сервис auth. На вход поступают логин и пароль (string). В ответе — можно ли войти в учетную запись (boolean).
- Сервис composition. На вход поступают логин и пароль (string). В ответе — можно ли войти в учетную запись (boolean).

Сначала composition идет в score, потом в auth.
Если ответ сервиса score ниже порога, то авторизация сразу запрещается, в auth идти смысла нет. Если выше или равно, то идет в auth.
Пороговое значение конфигурируется через dotenv.
Если сервис score ответил ошибкой, то считается, что у пользователя хороший скоринг.
Запросы и ответы форматируются как JSON.

Для эмуляции авторизации можно в самом сервисе сделать словарь/мапу с реквизитами для входа (логин и пароль).
Механизм скоринга может быть любой, хоть случайное число.


## Решение

Проект состоит из трёх HTTP-сервисов:

1. **Score Service** — рассчитывает оценку "хорошести" пользователя.
2. **Auth Service** — проверяет, может ли пользователь войти в учётную запись.
3. **Composition Service** — сначала обращается к Score, а затем к Auth для проверки входа на основании оценки пользователя.


### Структура проекта:
```
DZ1/
├── score/
│   ├── score_service.py
│   ├── requirements.txt
├── auth/
│   ├── auth_service.py
│   ├── requirements.txt
├── composition/
│   ├── composition_service.py
│   ├── requirements.txt
│   └── .env
└── README.md
 ```


## Установка и запуск

1. **Установка зависимостей для каждого сервиса:**

   Перейдите в каждую папку сервиса и установите зависимости:

   - Для `score` сервиса:
     ```bash
     cd score
     pip install -r requirements.txt
     ```

   - Для `auth` сервиса:
     ```bash
     cd auth
     pip install -r requirements.txt
     ```

   - Для `composition` сервиса:
     ```bash
     cd composition
     pip install -r requirements.txt
     ```

2. **Запуск сервисов:**

   В отдельных терминалах запустите каждый сервис:

   - Запуск `score` сервиса:
     ```bash
     python score_service.py
     ```

   - Запуск `auth` сервиса:
     ```bash
     python auth_service.py
     ```

   - Запуск `composition` сервиса:
     ```bash
     python composition_service.py
     ```

3. **Примеры запросов:**

Для bash
   - Для `score` сервиса:
     curl -X POST http://localhost:5001/score -H "Content-Type: application/json" -d '{"login": "user1"}'

   - Для `auth` сервиса:
     curl -X POST http://localhost:5002/auth -H "Content-Type: application/json" -d '{"login": "user1", "password": "password1"}'

   - Для `composition` сервиса:
     curl -X POST http://localhost:5003/composition -H "Content-Type: application/json" -d '{"login": "user1", "password": "password1"}'


Для powershell
   - Для `score` сервиса:
     Invoke-RestMethod -Uri http://localhost:5001/score -Method POST -Headers @{"Content-Type"="application/json"} -Body '{"login": "user1"}'

   - Для `auth` сервиса:
     Invoke-RestMethod -Uri http://localhost:5002/auth -Method POST -Headers @{"Content-Type"="application/json"} -Body '{"login": "user1", "password": "password1"}'
  
   - Для `composition` сервиса:
	 Invoke-RestMethod -Uri http://localhost:5003/composition -Method POST -Headers @{"Content-Type"="application/json"} -Body '{"login": "user1", "password": "password1"}'
