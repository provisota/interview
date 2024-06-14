<!-- TOC -->
* [Процессы в Python](#процессы-в-python)
  * [Введение](#введение)
  * [Модуль `multiprocessing`](#модуль-multiprocessing)
    * [Основные концепции](#основные-концепции)
    * [Простой пример использования](#простой-пример-использования)
  * [Создание и управление процессами](#создание-и-управление-процессами)
    * [Класс `Process`](#класс-process)
    * [Запуск и завершение процессов](#запуск-и-завершение-процессов)
  * [Межпроцессное взаимодействие](#межпроцессное-взаимодействие)
    * [Очереди (Queues)](#очереди-queues)
    * [Пайпы (Pipes)](#пайпы-pipes)
    * [Менеджеры (Managers)](#менеджеры-managers)
  * [Синхронизация процессов](#синхронизация-процессов)
    * [Блокировки (Locks)](#блокировки-locks)
    * [События (Events)](#события-events)
    * [Семафоры (Semaphores)](#семафоры-semaphores)
  * [Использование пула процессов](#использование-пула-процессов)
    * [Класс `Pool`](#класс-pool)
    * [Методы `apply`, `map`, `starmap`](#методы-apply-map-starmap)
  * [Полезные советы и практика](#полезные-советы-и-практика)
<!-- TOC -->

# Процессы в Python

## Введение
Процессы в Python позволяют выполнять параллельные вычисления, эффективно используя многозадачность и многопоточность. 
Для работы с процессами в Python используется модуль `multiprocessing`, который предоставляет инструменты для создания и управления процессами, а также межпроцессного взаимодействия и синхронизации.

## Модуль `multiprocessing`

### Основные концепции
Модуль `multiprocessing` предоставляет интерфейс, схожий с модулем `threading`, но с ключевым отличием: каждый процесс имеет собственное пространство памяти. 
Это позволяет избежать проблем, связанных с глобальной блокировкой интерпретатора (GIL) в многопоточном программировании Python.

### Простой пример использования
```python
from multiprocessing import Process

def worker():
    print("Рабочий процесс запущен")

if __name__ == "__main__":
    p = Process(target=worker)
    p.start()
    p.join()
```
В этом примере создается и запускается новый процесс, выполняющий функцию `worker`.

## Создание и управление процессами

### Класс `Process`
Класс `Process` используется для создания и управления процессами. 
Он принимает несколько параметров, включая `target` (функцию для выполнения) и `args` (аргументы для этой функции).

### Запуск и завершение процессов
Для запуска процесса используется метод `start()`, а для ожидания его завершения — метод `join()`.

```python
from multiprocessing import Process

def worker(number):
    print(f"Процесс {number} запущен")

if __name__ == "__main__":
    processes = []
    for i in range(5):
        p = Process(target=worker, args=(i,))
        processes.append(p)
        p.start()
    
    for p in processes:
        p.join()
```

## Межпроцессное взаимодействие

### Очереди (Queues)
Очереди позволяют обмениваться данными между процессами. Они обеспечивают безопасное и упорядоченное взаимодействие.

```python
from multiprocessing import Process, Queue

def worker(q):
    q.put("Привет из процесса")

if __name__ == "__main__":
    q = Queue()
    p = Process(target=worker, args=(q,))
    p.start()
    print(q.get())
    p.join()
```

### Пайпы (Pipes)
Пайпы предоставляют два конца для двустороннего обмена данными между процессами.

```python
from multiprocessing import Process, Pipe

def worker(conn):
    conn.send("Сообщение через пайп")
    conn.close()

if __name__ == "__main__":
    parent_conn, child_conn = Pipe()
    p = Process(target=worker, args=(child_conn,))
    p.start()
    print(parent_conn.recv())
    p.join()
```

### Менеджеры (Managers)
Менеджеры позволяют создавать объекты, доступные из нескольких процессов.

```python
from multiprocessing import Manager, Process

def worker(d, key, value):
    d[key] = value

if __name__ == "__main__":
    with Manager() as manager:
        d = manager.dict()
        p = Process(target=worker, args=(d, 'key', 'value'))
        p.start()
        p.join()
        print(d)
```

## Синхронизация процессов

### Блокировки (Locks)
Блокировки используются для предотвращения одновременного доступа к общим ресурсам.

```python
from multiprocessing import Process, Lock

def worker(lock, number):
    with lock:
        print(f"Процесс {number} запущен")

if __name__ == "__main__":
    lock = Lock()
    for i in range(5):
        p = Process(target=worker, args=(lock, i))
        p.start()
        p.join()
```

### События (Events)
События используются для сигнализации между процессами.

```python
from multiprocessing import Process, Event

def worker(event):
    print("Ждем сигнал...")
    event.wait()
    print("Сигнал получен!")

if __name__ == "__main__":
    event = Event()
    p = Process(target=worker, args=(event,))
    p.start()
    input("Нажмите Enter для отправки сигнала\n")
    event.set()
    p.join()
```

### Семафоры (Semaphores)
Семафоры ограничивают количество процессов, которые могут одновременно выполнять определенный участок кода.

```python
from multiprocessing import Process, Semaphore

def worker(semaphore, number):
    with semaphore:
        print(f"Процесс {number} запущен")
        time.sleep(2)

if __name__ == "__main__":
    semaphore = Semaphore(2)
    for i in range(5):
        p = Process(target=worker, args=(semaphore, i))
        p.start()
        p.join()
```

## Использование пула процессов

### Класс `Pool`
Класс `Pool` позволяет управлять пулом процессов, что упрощает выполнение параллельных задач.

```python
from multiprocessing import Pool

def worker(x):
    return x*x

if __name__ == "__main__":
    with Pool(4) as p:
        print(p.map(worker, range(10)))
```

### Методы `apply`, `map`, `starmap`
Эти методы позволяют выполнять функции в нескольких процессах.

```python
from multiprocessing import Pool

def worker(x):
    return x*x

if __name__ == "__main__":
    with Pool(4) as p:
        # apply
        result = p.apply(worker, (5,))
        print(result)

        # map
        results = p.map(worker, range(10))
        print(results)

        # starmap
        results = p.starmap(worker, [(i,) for i in range(10)])
        print(results)
```

## Полезные советы и практика
- Используйте `multiprocessing` для задач, которые могут быть разложены на независимые части.
- Внимательно следите за управлением ресурсами и синхронизацией для предотвращения состояний гонок.
- Тестируйте и профилируйте код для оптимизации производительности и выявления узких мест.

Эти знания помогут вам эффективно использовать процессы в Python для параллельных вычислений и выполнения задач, требующих высокой производительности.