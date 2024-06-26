<!-- TOC -->
  * [1. Как Golang управляет своими зависимостями?](#1-как-golang-управляет-своими-зависимостями)
  * [2. Какие нативные инструменты Golang вы знаете? (get, build, format, test и т.д.)](#2-какие-нативные-инструменты-golang-вы-знаете-get-build-format-test-и-тд)
  * [3. Как разместить стороннюю библиотеку локально (для отладки или разработки)?](#3-как-разместить-стороннюю-библиотеку-локально-для-отладки-или-разработки)
  * [4. Какие типы импортов вы знаете?](#4-какие-типы-импортов-вы-знаете)
  * [5. Какие инструменты статического анализа кода для Golang вы знаете? В чем их различия?](#5-какие-инструменты-статического-анализа-кода-для-golang-вы-знаете-в-чем-их-различия)
  * [6. Какие флаги сборки вы знаете?](#6-какие-флаги-сборки-вы-знаете)
  * [7. Для чего используются профилирование и трассировка? Как работать с pprof?](#7-для-чего-используются-профилирование-и-трассировка-как-работать-с-pprof)
  * [8. Опишите структуру проекта, которую вы бы использовали для библиотеки/сервиса/приложения. Опишите плюсы и минусы.](#8-опишите-структуру-проекта-которую-вы-бы-использовали-для-библиотекисервисаприложения-опишите-плюсы-и-минусы)
  * [9. Для чего используются GOPROXY, GOPRIVATE и GOSUMDB?](#9-для-чего-используются-goproxy-goprivate-и-gosumdb)
<!-- TOC -->

## 1. Как Golang управляет своими зависимостями?

**Ответ:**
Golang управляет зависимостями с помощью встроенного инструмента `go mod`. Этот инструмент позволяет создавать, обновлять и проверять модули, что делает управление зависимостями более простым и эффективным. Основные команды для работы с зависимостями:

- `go mod init`: инициализирует новый модуль в текущей директории.
- `go mod tidy`: удаляет неиспользуемые зависимости и добавляет недостающие.
- `go mod vendor`: создает директорию `vendor` с копиями всех зависимостей.
- `go get`: загружает и устанавливает указанные пакеты.

Зависимости управляются файлом `go.mod`, который содержит информацию о модуле и его зависимостях, а также файлом `go.sum`, который содержит контрольные суммы для обеспечения целостности зависимостей.

## 2. Какие нативные инструменты Golang вы знаете? (get, build, format, test и т.д.)

**Ответ:**
Golang предоставляет несколько нативных инструментов для управления проектами и их сборки:

- `go get`: загружает и устанавливает пакеты и их зависимости.
- `go build`: компилирует пакеты и их зависимости, создавая исполняемые файлы.
- `go run`: компилирует и запускает Go программы.
- `go test`: запускает тесты, написанные для пакетов.
- `go fmt`: форматирует исходный код в соответствии со стандартами Go.
- `go vet`: проводит статический анализ кода для выявления потенциальных ошибок.
- `go mod`: управляет зависимостями и модулями.
- `go install`: компилирует и устанавливает пакеты и зависимости.
- `go doc`: показывает документацию для пакетов и символов.
- `go clean`: удаляет объектные файлы и кэшированные данные.

## 3. Как разместить стороннюю библиотеку локально (для отладки или разработки)?

**Ответ:**
Для размещения сторонней библиотеки локально можно использовать директорию `replace` в файле `go.mod`. Это позволяет переопределить местоположение библиотеки на локальную директорию. Пример использования:

```go
module your/module

replace example.com/somelib => ../path/to/local/somelib

require example.com/somelib v1.0.0
```

Здесь `example.com/somelib` заменяется на локальный путь `../path/to/local/somelib`. Это позволяет вам работать с локальной копией библиотеки для отладки или разработки.

## 4. Какие типы импортов вы знаете?

**Ответ:**
В Go существует несколько типов импортов:

- Обычные импорты: используются для импорта пакетов, которые будут использоваться в коде.
  ```go
  import "fmt"
  ```

- Импорты с псевдонимами: позволяют задать альтернативное имя для импортируемого пакета.
  ```go
  import f "fmt"
  ```

- Пустые импорты: используются для выполнения инициализаций в пакете без явного использования его символов.
  ```go
  import _ "net/http/pprof"
  ```

- Групповые импорты: позволяют сгруппировать несколько импортов.
  ```go
  import (
      "fmt"
      "net/http"
  )
  ```

## 5. Какие инструменты статического анализа кода для Golang вы знаете? В чем их различия?

**Ответ:**
В Golang существует несколько популярных инструментов статического анализа:

- `go vet`: встроенный инструмент для анализа кода на наличие ошибок.
- `golint`: анализирует стиль кода и рекомендует улучшения.
- `staticcheck`: расширенный инструмент, который проверяет код на наличие ошибок, потенциальных проблем и улучшений стиля.
- `gosimple`: находит простые конструкции кода, которые могут быть упрощены.
- `errcheck`: проверяет, что все ошибки обработаны.
- `megacheck`: объединяет `staticcheck`, `gosimple` и `unused` в один инструмент.

Различия между ними в основном заключаются в объеме проверок и их специализации. `go vet` фокусируется на ошибках, которые могут привести к неправильному поведению программы, `golint` — на стиле кода, а `staticcheck` — на комплексных проверках кода.

## 6. Какие флаги сборки вы знаете?

**Ответ:**
Golang поддерживает несколько флагов сборки, которые могут быть использованы для настройки процесса компиляции:

- `-o`: задает имя выходного файла.
  ```bash
  go build -o outputfile
  ```

- `-a`: перекомпилирует все зависимости.
  ```bash
  go build -a
  ```

- `-x`: выводит команды компиляции.
  ```bash
  go build -x
  ```

- `-v`: выводит имена пакетов во время сборки.
  ```bash
  go build -v
  ```

- `-race`: включает детектор гонок данных.
  ```bash
  go build -race
  ```

- `-tags`: задает дополнительные теги сборки.
  ```bash
  go build -tags "mytag"
  ```

- `-ldflags`: задает флаги для компоновщика.
  ```bash
  go build -ldflags "-s -w"
  ```

## 7. Для чего используются профилирование и трассировка? Как работать с pprof?

**Ответ:**
Профилирование и трассировка используются для анализа производительности и поведения приложений. Профилирование позволяет определить узкие места в производительности, а трассировка помогает понять порядок выполнения кода и задержки.

Инструмент `pprof` в Go используется для профилирования CPU, памяти, блокировок и других параметров. Для работы с `pprof`:

1. Импортируйте пакет `net/http/pprof` в ваше приложение:
   ```go
   import _ "net/http/pprof"
   ```

2. Запустите HTTP-сервер:
   ```go
   go func() {
       log.Println(http.ListenAndServe("localhost:6060", nil))
   }()
   ```

3. Соберите и запустите ваше приложение. Откройте браузер и перейдите по адресу `http://localhost:6060/debug/pprof/`.

4. Для анализа используйте команду `go tool pprof`:
   ```bash
   go tool pprof http://localhost:6060/debug/pprof/profile
   ```

5. Исследуйте профиль, используя команды интерактивного интерфейса `pprof`.

## 8. Опишите структуру проекта, которую вы бы использовали для библиотеки/сервиса/приложения. Опишите плюсы и минусы.

**Ответ:**
Структура проекта зависит от его типа и масштаба. Вот пример структуры для веб-сервиса:

```
/project
    /cmd
        /app
            main.go
    /pkg
        /api
        /models
        /services
        /utils
    /internal
        /config
        /db
        /middleware
    /configs
    /scripts
    /docs
    /tests
    go.mod
    go.sum
```

Плюсы:
- Четкое

разделение кода по функциональным областям.
- Легко поддерживать и расширять проект.
- Четко определенные точки входа в приложение.

Минусы:
- Для маленьких проектов может быть избыточной.
- Требует дисциплины при организации и поддержке структуры.

## 9. Для чего используются GOPROXY, GOPRIVATE и GOSUMDB?

**Ответ:**

- `GOPROXY`: переменная окружения, которая указывает прокси-сервер для загрузки модулей. Это ускоряет загрузку и увеличивает надежность.
  ```bash
  export GOPROXY=https://proxy.golang.org
  ```

- `GOPRIVATE`: переменная окружения, которая определяет приватные модули, чтобы избежать их проверки через публичные прокси и хранилища.
  ```bash
  export GOPRIVATE=your.private.repo.com
  ```

- `GOSUMDB`: переменная окружения, которая указывает сервер контрольных сумм для проверки целостности модулей.
  ```bash
  export GOSUMDB=sum.golang.org
  ```

Эти инструменты используются для управления загрузкой и проверкой модулей, обеспечения безопасности и повышения производительности.