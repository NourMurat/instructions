Архитектура взаимодействия между микросервисами

1. nginx (Роутинг и балансировка нагрузки):
	Получает запросы от браузера.
	Направляет запросы на микросервис аутентификации на основе URL маршрута.

2. Микросервис аутентификации:
	Обрабатывает запросы на аутентификацию.
	Проверяет учетные данные пользователя.
	При успешной аутентификации генерирует JWT (JSON Web Token).
	Обновляет информацию в микросервисе базы данных.
	Возвращает ответ в nginx для передачи браузеру.

3. Микросервис базы данных:
	Управляет пользователями и их данными.
	Обрабатывает запросы на добавление, обновление и получение данных.
	Обеспечивает хранение хешированных паролей и другой конфиденциальной информации.

Взаимодействие между микросервисами (пошагово):

Запрос на аутентификацию от браузера:
	Браузер отправляет запрос на аутентификацию (например, POST /login) на nginx.
	nginx перенаправляет запрос в микросервис аутентификации.

Обработка запроса на аутентификацию:
	Микросервис аутентификации получает запрос.
	Проверяет учетные данные пользователя.
	Если данные верны, микросервис аутентификации генерирует JWT и направляет запрос в микросервис базы данных для обновления информации (например, времени последнего входа).

Обновление базы данных:
	Микросервис базы данных получает запрос от микросервиса аутентификации, обновляет необходимые данные и возвращает ответ.

Ответ пользователю:
	Микросервис аутентификации получает ответ от микросервиса базы данных.
	Микросервис аутентификации формирует ответ, включая JWT, и отправляет его обратно в nginx.
	nginx передает ответ браузеру.



Обоснование:
	Разделение обязанностей: Каждый микросервис отвечает за свою часть логики, что упрощает обслуживание и масштабирование.
	Безопасность: Использование JWT для аутентификации обеспечивает безопасную передачу данных между клиентом и сервером.
	Масштабируемость: nginx обеспечивает балансировку нагрузки и маршрутизацию запросов, что позволяет легко добавлять новые микросервисы и масштабировать существующие.

Эта архитектура обеспечит надежное и безопасное взаимодействие между микросервисами, отвечая требованиям  проекта ft_transcendence.