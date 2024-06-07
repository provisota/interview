<!-- TOC -->
* [Basic](#basic)
  * [1. Что такое ORM и для чего она предназначена?](#1-что-такое-orm-и-для-чего-она-предназначена)
  * [2. Как использовать ORM с новой базой данных?](#2-как-использовать-orm-с-новой-базой-данных)
  * [3. Как использовать ORM с существующей базой данных?](#3-как-использовать-orm-с-существующей-базой-данных)
* [Regular](#regular)
  * [4. Какие существуют соображения по производительности при использовании ORM?](#4-какие-существуют-соображения-по-производительности-при-использовании-orm)
  * [5. Каковы типичные случаи использования ORM? Почему?](#5-каковы-типичные-случаи-использования-orm-почему)
  * [6. Когда лучше не использовать ORM? Почему?](#6-когда-лучше-не-использовать-orm-почему)
<!-- TOC -->

# Basic

## 1. Что такое ORM и для чего она предназначена?
**Вопрос:**  
Что такое ORM и для чего она предназначена?

**Ответ:**  
ORM (Object-Relational Mapping) — это методология программирования, которая связывает объекты в коде с записями в базе данных. Основная цель ORM — упростить взаимодействие между объектно-ориентированным кодом и реляционной базой данных, устраняя необходимость написания сложных SQL-запросов.

ORM позволяет разработчикам работать с данными на уровне объектов, что упрощает чтение и поддержку кода. Примеры популярных ORM-библиотек для Python включают SQLAlchemy, Django ORM и Peewee.

Пример использования SQLAlchemy:
```python
from sqlalchemy import create_engine, Column, Integer, String, Sequence
from sqlalchemy.ext.declarative import declarative_base
from sqlalchemy.orm import sessionmaker

Base = declarative_base()

class User(Base):
    __tablename__ = 'users'
    id = Column(Integer, Sequence('user_id_seq'), primary_key=True)
    name = Column(String(50))
    fullname = Column(String(50))
    nickname = Column(String(50))

engine = create_engine('sqlite:///:memory:')
Base.metadata.create_all(engine)

Session = sessionmaker(bind=engine)
session = Session()

new_user = User(name='John', fullname='John Doe', nickname='johnny')
session.add(new_user)
session.commit()
```

## 2. Как использовать ORM с новой базой данных?
**Вопрос:**  
Как использовать ORM с новой базой данных?

**Ответ:**  
Для использования ORM с новой базой данных, вам нужно выполнить следующие шаги:

1. Установить необходимую ORM-библиотеку (например, SQLAlchemy).
2. Определить модели, которые будут соответствовать таблицам в базе данных.
3. Создать таблицы в базе данных на основе этих моделей.
4. Создать сессию для взаимодействия с базой данных.

Пример использования SQLAlchemy с новой базой данных:
```python
from sqlalchemy import create_engine, Column, Integer, String, Sequence
from sqlalchemy.ext.declarative import declarative_base
from sqlalchemy.orm import sessionmaker

# Определение базы данных и модели
Base = declarative_base()

class User(Base):
    __tablename__ = 'users'
    id = Column(Integer, Sequence('user_id_seq'), primary_key=True)
    name = Column(String(50))
    fullname = Column(String(50))
    nickname = Column(String(50))

# Создание новой базы данных
engine = create_engine('sqlite:///new_database.db')
Base.metadata.create_all(engine)

# Создание сессии
Session = sessionmaker(bind=engine)
session = Session()

# Добавление нового пользователя
new_user = User(name='John', fullname='John Doe', nickname='johnny')
session.add(new_user)
session.commit()
```

## 3. Как использовать ORM с существующей базой данных?
**Вопрос:**  
Как использовать ORM с существующей базой данных?

**Ответ:**  
Для использования ORM с существующей базой данных, необходимо выполнить следующие шаги:

1. Установить необходимую ORM-библиотеку.
2. Определить модели, соответствующие существующим таблицам в базе данных, указав явные связи с этими таблицами.
3. Создать сессию для взаимодействия с базой данных.

Пример использования SQLAlchemy с существующей базой данных:
```python
from sqlalchemy import create_engine, Column, Integer, String
from sqlalchemy.ext.declarative import declarative_base
from sqlalchemy.orm import sessionmaker

# Определение базы данных и модели, соответствующей существующей таблице
Base = declarative_base()

class User(Base):
    __tablename__ = 'users'
    id = Column(Integer, primary_key=True)
    name = Column(String(50))
    fullname = Column(String(50))
    nickname = Column(String(50))

# Подключение к существующей базе данных
engine = create_engine('sqlite:///existing_database.db')
Base.metadata.bind = engine

# Создание сессии
Session = sessionmaker(bind=engine)
session = Session()

# Получение данных из существующей таблицы
users = session.query(User).all()
for user in users:
    print(user.name, user.fullname, user.nickname)
```

# Regular

## 4. Какие существуют соображения по производительности при использовании ORM?
**Вопрос:**  
Какие существуют соображения по производительности при использовании ORM?

**Ответ:**  
При использовании ORM существуют несколько соображений по производительности:

1. **Нагрузочное тестирование**: ORM может генерировать неэффективные SQL-запросы, что может привести к увеличению времени выполнения операций.
2. **Кеширование**: Некоторые ORM поддерживают кеширование запросов, что может значительно улучшить производительность.
3. **Ленивые и жадные загрузки**: Правильная настройка ленивых (lazy) и жадных (eager) загрузок данных может уменьшить количество запросов к базе данных.
4. **Профилирование запросов**: Анализ и оптимизация генерируемых SQL-запросов помогут избежать избыточных запросов и повысить производительность.
5. **Пакетные операции**: Использование пакетных операций для массового обновления или вставки данных может снизить нагрузку на базу данных.

Пример профилирования запросов в SQLAlchemy:
```python
from sqlalchemy import create_engine, event
from sqlalchemy.orm import sessionmaker

engine = create_engine('sqlite:///existing_database.db')

@event.listens_for(engine, "before_cursor_execute")
def before_cursor_execute(conn, cursor, statement, parameters, context, executemany):
    print("Query:", statement)

Session = sessionmaker(bind=engine)
session = Session()

# Выполнение запроса
users = session.query(User).all()
```

## 5. Каковы типичные случаи использования ORM? Почему?
**Вопрос:**  
Каковы типичные случаи использования ORM? Почему?

**Ответ:**  
Типичные случаи использования ORM включают:

1. **CRUD-операции**: ORM упрощает создание, чтение, обновление и удаление записей в базе данных без написания сложных SQL-запросов.
2. **Миграции схемы**: ORM часто включает инструменты для управления миграциями базы данных, что упрощает поддержку и обновление структуры базы данных.
3. **Связи между таблицами**: ORM обеспечивает удобный механизм для определения и управления связями между таблицами (один-к-одному, один-ко-многим, многие-ко-многим).
4. **Валидация данных**: ORM может включать механизмы валидации данных перед их сохранением в базу данных, что улучшает целостность данных.

Пример использования ORM для CRUD-операций:
```python
# Создание нового пользователя
new_user = User(name='Jane', fullname='Jane Doe', nickname='janie')
session.add(new_user)
session.commit()

# Чтение данных
user = session.query(User).filter_by(name='Jane').first()
print(user.fullname)

# Обновление данных
user.nickname = 'janed'
session.commit()

# Удаление данных
session.delete(user)
session.commit()
```

## 6. Когда лучше не использовать ORM? Почему?
**Вопрос:**  
Когда лучше не использовать ORM? Почему?

**Ответ:**  
Существуют ситуации, когда использование ORM может быть нецелесообразным:

1. **Высокие требования к производительности**: В некоторых случаях ORM может генерировать неэффективные SQL-запросы, что может негативно сказаться на производительности приложения.
2. **Сложные запросы**: Если приложение требует выполнения сложных и оптимизированных SQL-запросов, использование ORM может усложнить этот процесс.
3. **Легаси-системы**: В системах с устаревшими базами данных или нестандартными структурами использование ORM может быть затруднительным.
4. **Контроль над SQL**: Если разработчикам необходимо полный контроль над SQL-запросами, использование ORM может быть ограничением.

В таких случаях можно комбинировать использование ORM и чистого SQL для достижения наилучших результатов.

Пример использования чистого SQL вместе с ORM в SQLAlchemy:
```python
from sqlalchemy import text

# Выполнение чистого SQL-запроса
result = session.execute