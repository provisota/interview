<!-- TOC -->
* [Authentication and Authorization](#authentication-and-authorization)
  * [Аутентификация](#аутентификация)
      * [Факторы аутентификации](#факторы-аутентификации)
  * [Авторизация](#авторизация)
  * [Заключение](#заключение)
  * [OAuth 2.0](#oauth-20)
      * [Чем отличаются OpenID и OAuth](#чем-отличаются-openid-и-oauth)
      * [Как работает OAuth 2.0](#как-работает-oauth-20)
      * [Авторизация для приложений, имеющих серверную часть](#авторизация-для-приложений-имеющих-серверную-часть)
      * [Пример](#пример)
      * [Авторизация полностью клиентских приложений](#авторизация-полностью-клиентских-приложений)
      * [Пример](#пример-1)
      * [Минусы OAuth 2.0](#минусы-oauth-20)
      * [Заключение](#заключение-1)
  * [Полезные ссылки](#полезные-ссылки)
<!-- TOC -->

# Authentication and Authorization

Аутентификация и авторизация – две ключевые функции сервисной инфраструктуры для защиты конфиденциальных данных и операций от несанкционированного доступа со 
стороны злоумышленников.

**Aутентификация – это то, кем вы являетесь, авторизация – это то, к чему вы можете получить доступ**.

Хотя эти два термина используются в одном контексте, они представляют собой принципиально разные понятия, поскольку осуществляют защиту взаимодополняющими способами.

## Аутентификация

Аутентификация используется для подтверждения личности зарегистрированного пользователя. Проверка подлинности – это процесс проверки учетных данных: 
идентификатора пользователя (имени, адреса электронной почты, номера телефона) и пароля.

Если идентификатор и пароль совпадают с записями, хранящимися в базе данных системы, пользователю предоставляется доступ. В случае неправильного ввода данных 
программа вызывает предупреждение безопасности и блокирует вход. Если неудачных попыток будет несколько, система заблокирует саму учетную запись.

#### Факторы аутентификации

Метод стандартной аутентификации не может обеспечить абсолютную безопасность при входе пользователя в систему. Для создания более надежной защиты используются 
дополнительные категории учетных данных (факторов).

- `Однофакторная аутентификация` (`SFA`) – базовый, традиционный метод проверки подлинности с использованием только одной категории. Наиболее распространенным 
примером `SFA` являются учетные данные, связанные с введением имени пользователя и обычного пароля.
- `Двухфакторная аутентификация` (`2FA`) – двухступенчатый процесс проверки, который учитывает два разных типа пользовательских данных. Помимо логина и пароля, 
для обеспечения дополнительного уровня защиты, система может запросить особый код, присланный в `SMS` сообщении или в письме электронной почты.
- `Многофакторная аутентификация` (`MFA`) – самый современный метод проверки подлинности, который использует два, три (или больше) уровня безопасности. 
Категории всех уровней должны быть независимыми друг от друга, чтобы устранить любую уязвимость в системе. Финансовые организации, банки, правоохранительные 
органы пользуются многофакторной аутентификацией для защиты своих данных от потенциальных угроз.
Примером `MFA` является использование банковских карт. Наличие карты – первый фактор защиты, введение пин-кода – второй.

## Авторизация

Происходит после того, как личность пользователя успешно аутентифицируется системой. Процесс авторизации определяет, имеет ли прошедший проверку человек доступ 
к определенным ресурсам: информации, файлам, базе данных. Факторы проверки подлинности, необходимые для авторизации, могут различаться в зависимости от уровня 
безопасности.

Например, процесс проверки и подтверждения идентификаторов сотрудников и паролей в организации называется аутентификацией, но определение того, какой сотрудник 
имеет доступ к определенным ресурсам, называется авторизацией. Предположим, что вы путешествуете и собираетесь сесть на самолет. Когда вы предъявляете свой 
билет и удостоверение личности перед регистрацией, то получаете посадочный талон, который подтверждает, что администрация аэропорта удостоверила вашу личность. 
Но это не все. Чтобы получить доступ к внутренней части самолета и его ресурсам, вам необходимо получить разрешение бортпроводника на посадку.

## Заключение

Доступ к системе защищен как аутентификацией, так и авторизацией. 
Любая попытка доступа аутентифицируется путем ввода учетных данных, и только после успешной аутентификации система проверяет авторизован ли 
пользователь для использования определённых ресурсов. 
Если же попытка доступа аутентифицирована, но не авторизована, система **запретит** доступ неавторизованным ресурсам.

## OAuth 2.0

`OAuth 2.0` — протокол авторизации, позволяющий выдать одному сервису (приложению) права на доступ к ресурсам пользователя на другом сервисе. Протокол 
избавляет от необходимости доверять приложению логин и пароль, а также позволяет выдавать ограниченный набор прав, а не все сразу.

#### Чем отличаются OpenID и OAuth

`OpenID` предназначен для аутентификации — то есть для того, чтобы понять, что этот конкретный пользователь является тем, кем представляется. Например, с 
помощью `OpenID` некий сервис `Ололо` может понять, что зашедший туда пользователь, это именно `Рома Новиков` с `Mail.Ru`. При следующей аутентификации `Ололо` 
сможет его опять узнать и понять, что, это тот же Рома, что и в прошлый раз.

`OAuth` же является протоколом авторизации, то есть позволяет выдать права на действия, которые сам `Ололо` сможет производить в `Mail.Ru` от лица `Ромы`. При 
этом Рома после авторизации может вообще не участвовать в процессе выполнения действий, например, `Ололо` сможет самостоятельно заливать фотографии на Ромин 
аккаунт.

#### Как работает OAuth 2.0

Как и первая версия, `OAuth 2.0` основан на использовании базовых веб-технологий: `HTTP`-запросах, редиректах и т. п. Поэтому использование `OAuth` возможно на 
любой платформе с доступом к интернету и браузеру: на сайтах, в мобильных и desktop-приложениях, плагинах для браузеров…

Ключевое отличие от `OAuth 1.0` — простота. В новой версии нет громоздких схем подписи, сокращено количество запросов, необходимых для авторизации.

Общая схема работы приложения, использующего `OAuth`, такова:
- получение авторизации
- обращение к защищенным ресурсам

Результатом авторизации является `access token` — некий ключ (обычно просто набор символов), предъявление которого является пропуском к защищенным ресурсам. 
Обращение к ним в самом простом случае происходит по `HTTPS` с указанием в заголовках или в качестве одного из параметров полученного `access token`'а.

В протоколе описано несколько вариантов авторизации, подходящих для различных ситуаций:
- авторизация для приложений, имеющих серверную часть (чаще всего, это сайты и веб-приложения)
- авторизация для полностью клиентских приложений (мобильные и desktop-приложения)
- авторизация по логину и паролю
- восстановление предыдущей авторизации

#### Авторизация для приложений, имеющих серверную часть

![Screenshot](../../resources/oauth2_1.png)

1. Редирект на страницу авторизации
2. На странице авторизации у пользователя запрашивается подтверждение выдачи прав
3. В случае согласия пользователя, браузер редиректится на `URL`, указанный при открытии страницы авторизации, с добавлением в `GET`-параметры специального 
ключа — `authorization code`
4. Сервер приложения выполняет `POST`-запрос с полученным `authorization code` в качестве параметра. В результате этого запроса возвращается `access token`.

Это самый сложный вариант авторизации, но только он позволяет сервису однозначно установить приложение, обращающееся за авторизацией (это происходит при 
коммуникации между серверами на последнем шаге). Во всех остальных вариантах авторизация происходит полностью на клиенте и по понятным причинам возможна 
маскировка одного приложения под другое. Это стоит учитывать при внедрении `OAuth`-аутентификации в `API` сервисов.

#### Пример

Здесь и далее примеры приводятся для `API Mail.Ru`, но логика одинаковая для всех сервисов, меняются только адреса страниц авторизации. Обратите внимание, что 
запросы надо делать по `HTTPS`.

Редиректим браузер пользователя на страницу авторизации:

```
> GET /oauth/authorize?response_type=code&client_id=464119&redirect_uri=http%3A%2F%2Fexample.com%2Fcb%2F123 HTTP/1.1
> Host: connect.mail.ru
```

Здесь и далее, `client_id` и `client_secret` — значения, полученные при регистрации приложения на платформе.

После того, как пользователь выдаст права, происходит редирект на указанный `redirect_uri`:

```
< HTTP/1.1 302 Found
< Location: http://example.com/cb/123?code=DoRieb0y
```

Обратите внимание, если вы реализуете логин на сайте с помощью `OAuth`, то рекомендуется в `redirect_uri` добавлять уникальный для каждого пользователя 
идентификатор для предотвращения `CSRF`-атак (в примере это 123). При получении кода надо проверить, что этот идентификатор не изменился и соответствует 
текущему пользователю.

Используем полученный `code` для получения `access_token`, выполняя запрос с сервера:

```
> POST /oauth/token HTTP/1.1
> Host: connect.mail.ru
> Content-Type: application/x-www-form-urlencoded
> 
> grant_type=authorization_code&client_id=464119&client_secret=deadbeef&code=DoRieb0y&redirect_uri=http%3A%2F%2Fexample.com%2Fcb%2F123

< HTTP/1.1 200 OK
< Content-Type: application/json
<
< {
<    "access_token":"SlAV32hkKG",
<    "token_type":"bearer",
<    "expires_in":86400,
<    "refresh_token":"8xLOxBtZp8",
< }
```

Обратите внимание, что в последнем запросе используется `client_secret`, который в данном случае хранится на сервере приложения, и подтверждает, что запрос не 
подделан.

В результате последнего запроса получаем сам ключ доступа (`access_token`), время его «протухания» (`expires_in`), тип ключа, определяющий как его надо 
использовать, (`token_type`) и `refresh_token` о котором будет подробнее сказано ниже. Дальше, полученные данные можно использовать для доступа к защищенным 
ресурсам, например, `API Mail.Ru`:

```
> GET /platform/api?oauth_token=SlAV32hkKG&client_id=464119&format=json&method=users.getInfo&
      sig=... HTTP/1.1
> Host: appsmail.ru
```

#### Авторизация полностью клиентских приложений

![Screenshot](../../resources/oauth2_1.png)

1. Открытие встроенного браузера со страницей авторизации
2. У пользователя запрашивается подтверждение выдачи прав
3. В случае согласия пользователя, браузер редиректится на страницу-заглушку во фрагменте (после #) `URL` которой добавляется `access token`
4. Приложение перехватывает редирект и получает `access token` из адреса страницы

Этот вариант требует поднятия в приложении окна браузера, но не требует серверной части и дополнительного вызова сервер-сервер для обмена `authorization code` 
на `access token`.

#### Пример

Открываем браузер со страницей авторизации:

```
> GET /oauth/authorize?response_type=token&client_id=464119 HTTP/1.1
> Host: connect.mail.ru
```

После того, как пользователь выдаст права, происходит редирект на стандартную страницу-заглушку, для `Mail.Ru` это `connect.mail.ru/oauth/success.html`:

```
< HTTP/1.1 302 Found
< Location: http://connect.mail.ru/oauth/success.html#access_token=FJQbwq9&token_type=bearer&expires_in=86400&refresh_token=yaeFa0gu
```

Приложение должно перехватить последний редирект, получить из адреса acess_token и использовать его для обращения к защищенным ресурсам.

#### Минусы OAuth 2.0

Во всей этой красоте есть и ложка дегтя, куда без нее?

`OAuth 2.0` — развивающийся стандарт. Это значит, что спецификация еще не устоялась и постоянно меняется, иногда довольно заметно. Так, что если вы решили 
поддержать стандарт прямо сейчас, приготовьтесь к тому, что его поддержку придется подпиливать по мере изменения спецификации. С другой стороны, это также 
значит, что вы можете поучаствовать в процессе написания стандарта и внести в него свои идеи.

Безопасность `OAuth 2.0` во многом основана на `SSL`. Это сильно упрощает жизнь разработчикам, но требует дополнительных вычислительных ресурсов и 
администрирования. Это может быть существенным вопросом в высоко нагруженных проектах.

#### Заключение

`OAuth` — простой стандарт авторизации, основанный на базовых принципах интернета, что делает возможным применение авторизации практически на любой платформе. 
Стандарт имеет поддержку крупнейших площадок и очевидно, что его популярность будет только расти. Если вы задумались об `API` для вашего сервиса, то 
авторизация с использованием `OAuth 2.0` — хороший выбор.

## Полезные ссылки

[В чем состоит разница между аутентификацией и авторизацией - artismedia.by](https://artismedia.by/blog/difference-between-authentication-and-authorization/)

[OAuth 2.0 простым и понятным языком - habr](https://habr.com/ru/company/mailru/blog/115163/#:~:text=OAuth%202.0%20%E2%80%94%20%D0%BF%D1%80%D0%BE%D1%82%D0%BE%D0%BA%D0%BE%D0%BB%20%D0%B0%D0%B2%D1%82%D0%BE%D1%80%D0%B8%D0%B7%D0%B0%D1%86%D0%B8%D0%B8%2C%20%D0%BF%D0%BE%D0%B7%D0%B2%D0%BE%D0%BB%D1%8F%D1%8E%D1%89%D0%B8%D0%B9,%D0%BF%D1%80%D0%B0%D0%B2%2C%20%D0%B0%20%D0%BD%D0%B5%20%D0%B2%D1%81%D0%B5%20%D1%81%D1%80%D0%B0%D0%B7%D1%83.)
