# social_network_system_design

Проектирование социальной сети для путешественников в рамках курса ["System design"](https://balun.courses/courses/system_design).

#### Функциональные требования:

- [ ] регистрация по номеру телефона/почте: подтверждение через смс/код;
- [ ] онбординг при первом посещении: подсветка основных возможностей системы;
- [ ] авторизация по номеру телефона/почте;
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
  - публикация поста: < 7 секунд;
  - загрузка поста для показа: < 3 секунд;
  - публикация комментария: < 5 секунд;
  - поиск места: < 10 секунд;
  - доставка сообщения от пользователя к пользователю: < 10 секунд.
- [ ] лимиты и ограничения:
  - фотографии: 5/публикация;
  - размер фотографии: 1 МБ;
  - посты: 5/день;
  - описание: 500 символов; 
  - подписчики: 10000;
  - подписки: 10000;
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

#### RPS:
```
                         (посты +  лс + поиск)
RPS (чтение) = 10 000 000 * (30 + 500 + 10) / 86400 = 62 500
```
```
                 (пост + комментарии + оценка + лс + прдписка)
RPS (запись) = 10 000 000 * (1 + 5 + 10 + 300 + 10) / 86400 = 37 700
```
#### Трафик:
```
Чтение = 62 500 * 2 МБ = 122 ГБ/секунду
```
```
Запись = 37 700 * 4 МБ = 147,3 ГБ/секунду
```
#### Одновременные соединения:
```
10 000 000 * 0.1 = 1 000 000
```