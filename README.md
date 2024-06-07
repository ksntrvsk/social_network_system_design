# social_network_system_design

Проектирование социальной сети для путешественников в рамках курса ["System design"](https://balun.courses/courses/system_design).

#### Функциональные требования:

- [ ] регистрация по номеру телефона/почте: подтверждение через смс/код;
- [ ] онбординг при первом посещении: подсветка основных возможностей системы;
- [ ] аутентификация по номеру телефона/почте;
- [ ] редактирование ЛК: смена никнейма/аватарки;
- [ ] публикация изображений из путешествий;
- [ ] возможность добавить/отредактировать краткое описание под постом и указать точное место поездки;
- [ ] оценка постов;
- [ ] комментирование публикаций других пользователей;
- [ ] подписка на пользователей;
- [ ] возможность включить/выключить уведомления о новых публикациях пользователей, на которых есть подписка, для отслеживания их активности;
- [ ] поиск по геолокации с возможностью выбора страны/города и выдача постов на основе популярности (популярность измеряется в количестве набранных оценок под постом);
- [ ] возможность общения между пользователями в личном чате; 
- [ ] выдача постов в ленте пользователей, на которых есть подписка.

#### Нефункциональные требования:

- [ ] DAU: 10 000 000;
- [ ] регионы использования: страны СНГ;
- [ ] кроссплатформенность: мобильное приложение и веб-версия;
- [ ] сезонность: 
  - повышенная активность в периоды праздников, летних отпусков: 10 000 000;
  - остальное время: 6 000 000.
- [ ] хранение данных: данные активных пользователей хранятся всегда;
- [ ] доступность: 99,95%;
- [ ] время обслуживания пользователя:
  - загрузка ленты: < 3 секунд:
  - публикация поста: < 3 секунд;
  - загрузка поста для показа: < 3 секунд;
  - публикация комментария: < 2 секунд;
  - поиск места: < 10 секунд;
  - доставка сообщения от пользователя к пользователю: < 10 секунд.
- [ ] лимиты и ограничения:
  - фотографии: 5/публикация;
  - размер фотографии: 1 МБ;
  - посты: 5/день;
  - описание: 500 символов; 
  - подписчики/подписки: 10000;
  - комментарии: 30/день по 500 символов;
  - оценка публикаций других пользователей: 100/день;
  - личные сообщения (отправка): 1000 сообщений/день.
- [ ] среднее поведение пользователя:
  - публикация поста: 1/день по 3 фотографии (3 МБ) в посте (с описанием и геолокацией);
  - комментарии: 5/день;
  - оценка других пользователей: 10/день;
  - личные сообщения (запись): 300/день;
  - просмотр постов: 30/день;
  - личные сообщения (чтение): 500/день;
  - подписка на пользователей: 5/день;
  - поиск мест: 10/день.

### Расчет нагрузки
<hr>

`RPS` Посты:
```
RPS (чтение) = 10 000 000 * 30 / 86400 = 2 373
RPS (запись) = 10 000 000 * 1 / 86400 = 116
```
`RPS` Личные сообщения:
```
RPS (чтение) = 10 000 000 * 500 / 86400 = 57 870
RPS (запись) = 10 000 000 * 300 / 86400 = 34 722
```
`RPS` Поиск:
```
RPS (чтение) = 10 000 000 * 10 / 86400 = 1 157
```
`RPS` Комментарии:
```
RPS (запись) = 10 000 000 * 5 / 86400 = 579
```
`RPS` Оценка:
```
RPS (запись) = 10 000 000 * 10 / 86400 = 1 157
```
`RPS` Подписка:
```
RPS (запись) = 10 000 000 * 10 / 86400 = 1 157
```

`Трафик` Посты:
```
Чтение = 2 373 * 2 МБ = ~4.7 ГБ/секунду
Запись = 116 * 4 МБ = ~0.5 ГБ/секунду
```
`Трафик` Личные сообщения:
```
Запись = 34 722 * 1 МБ = ~35 ГБ/секунду
```
`Трафик` Комментарии:
```
Запись = 579 * 2 КБ = ~1 МБ/секунду
```
#### Одновременные соединения:
```
10 000 000 * 0.1 = 1 000 000
```