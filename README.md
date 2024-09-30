# Задание 1

## Проектирование

Команда работает с React и Vue. Поскольку задачи использовать разные фреймворки в Mesto нет, то оставляем React.
Один js-framework + разницы особой между WMF и SSPA нет. Берем Webpack Module Federation.

Вижу здесь 4 модуля + хост:
1. Auth - авторизация, регистрация.
2. Profile - профиль пользователя.
3. Gallery - лента с превью карточек, деталка карточки, добавление/удаление.
4. Common - базовые механики, общие компоненты.
5. Host - основное приложение.

Третью часть не сделал. Начал, но времени нет на это.

# Задание 2
https://drive.google.com/file/d/1ftCPTFU1XoZqy-aDDMlEtQqNpMTrEyfX/view?usp=sharing

## Целевые микросервисы

1) Auth
Отвечает за регистрацию, авторизацию, проверку токена, присвоение ролей.
Передача события успешная регистрация в шину. 
По такому же флоу пойдут события: вход с нового устройства, N неудачных попыток входа, сброс пароля и т.п.

2) Users
Хранит перс. данные и позволяет пользователям редактировать их. То же самое касается торговых площадок, но у них
регистрация дольше - она проходит валидацию у модераторов.

3) Services
CRUD по сущности услуга. Поиск, фильтрация и сортировка поддерживаются. 

4) Goods
CRUD по сущности товар. Поиск, фильтрация и сортировка поддерживаются.

5) Auctions
CRUD по сущностям аукцион и ставка. 
События "появилась ставка выше вашей", "вы победили на аукционе", "к сожалению, ваша ставка не выиграла" - уходят в шину

6) Orders
CRUD по сущности заказ. Событие смены статуса - уходит в шину

7) Payments
Обеспечивает проведение оплаты пользователем. Умеет работать с рядом внешних платежных систем.
Хранит все транзакции.

8) Notifications
Обеспечивает рассылку нотификаций пользователей (sms, push, email, etc..)

9) Support
Интегрирован с ITSM-системой и КЦ. Позволяет обрабатывать заявки от пользователей о тех. проблемах.

10) Admin
Для администраторов - обрабатывают заявки на проведение аукционов, рассматривают апелляции и заявки на 
регистрацию от торговых площадок, а также могут выгрузить отчет об активности пользователей.

11) Reports
Генерация отчетов. Аналитика по заказам и по продажам для пользователей, по поведению пользователей для администраторов

12) Шина данных (Kafka / RabbitMQ)
Для обеспечения событийного взаимодействия. Отчеты готовятся не сразу, сервис нотификаций имеет мн-во триггеров и т.д.
